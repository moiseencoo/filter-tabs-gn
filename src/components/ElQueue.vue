<template>
  <div v-if="getElQDate">
    <div class="available-dates-wrapper">
      <div class="date-and-time">
        <div class="date-and-time-title">
          <span
            v-if="electronQueu.available_dates_index > 0"
            @click="electronQueu.available_dates_index--"
            class="previous-day"
          ></span>
          {{ getElQDate }}
          <span
            v-if="electronQueu.available_dates_index < 2"
            @click="electronQueu.available_dates_index++"
            class="next-day"
          ></span>
        </div>
        <hooper
          @slide="updateCarousel"
          :vertical="true"
          :touchDrag="false"
          style="height: 150px"
          :itemsToShow="3"
          :centerMode="true"
          :transition="200"
        >
          <slide v-for="(item, index) in getElQTimes" :key="index">
            <span :class="{ not_available: item.available == 0 }">{{
              item.time
            }}</span>
          </slide>
          <hooper-navigation slot="hooper-addons"></hooper-navigation>
        </hooper>
      </div>
      <input type="text" :value="choosenElQ" readonly />
    </div>
  </div>
</template>

<script>
import { Hooper, Slide, Navigation as HooperNavigation } from "hooper";
import "hooper/dist/hooper.css";

export default {
  components: {
    Hooper,
    Slide,
    HooperNavigation,
  },
  data: () => ({
    electronQueu: {
      available_dates_index: 0,
      available_time: [
        {
          date: "11.01.2021",
          values: [
            {
              time: "16:00",
              available: 1,
              regionId: 28,
              officeId: 4,
              date: "11.01.2021",
              dateTime: "11.01.2021 16:00:00",
            },
            {
              time: "16:30",
              available: 1,
              regionId: 28,
              officeId: 4,
              date: "11.01.2021",
              dateTime: "11.01.2021 16:30:00",
            },
            {
              time: "17:00",
              available: 0,
              regionId: 28,
              officeId: 4,
              date: "11.01.2021",
              dateTime: "11.01.2021 17:00:00",
            },
            {
              time: "17:30",
              available: 1,
              regionId: 28,
              officeId: 4,
              date: "11.01.2021",
              dateTime: "11.01.2021 17:30:00",
            },
          ],
        },
        {
          date: "12.01.2021",
          values: [
            {
              time: "09:00",
              available: 1,
              regionId: 28,
              officeId: 4,
              date: "12.01.2021",
              dateTime: "12.01.2021 09:00:00",
            },
            {
              time: "09:30",
              available: 0,
              regionId: 28,
              officeId: 4,
              date: "12.01.2021",
              dateTime: "12.01.2021 09:30:00",
            },
            {
              time: "10:00",
              available: 1,
              regionId: 28,
              officeId: 4,
              date: "12.01.2021",
              dateTime: "12.01.2021 10:00:00",
            },
            {
              time: "10:30",
              available: 1,
              regionId: 28,
              officeId: 4,
              date: "12.01.2021",
              dateTime: "12.01.2021 10:30:00",
            },
            {
              time: "11:00",
              available: 1,
              regionId: 28,
              officeId: 4,
              date: "12.01.2021",
              dateTime: "12.01.2021 11:00:00",
            },
            {
              time: "11:30",
              available: 0,
              regionId: 28,
              officeId: 4,
              date: "12.01.2021",
              dateTime: "12.01.2021 11:30:00",
            },
            {
              time: "12:00",
              available: 1,
              regionId: 28,
              officeId: 4,
              date: "12.01.2021",
              dateTime: "12.01.2021 12:00:00",
            },
            {
              time: "12:30",
              available: 1,
              regionId: 28,
              officeId: 4,
              date: "12.01.2021",
              dateTime: "12.01.2021 12:30:00",
            },
          ],
        },
      ],
      available_time_index: 0,
      choosenDate: "",
      choosenTime: "",
      unavailable: false,
    },
  }),
  methods: {
    updateCarousel(payload) {
      if (this.getElQTimes[payload.currentSlide].available != 0) {
        this.electronQueu.choosenTime = this.getElQTimes[
          payload.currentSlide
        ].time;
        this.electronQueu.unavailable = false;
      } else {
        this.electronQueu.unavailable = true;
      }
    },
  },
  computed: {
    getElQDate() {
      if (this.electronQueu.available_time.length > 0) {
        return this.electronQueu.available_time[
          this.electronQueu.available_dates_index
        ].date;
      }
      return false
    },

    getElQTimes() {
      return this.electronQueu.available_time[
        this.electronQueu.available_dates_index
      ].values;
    },

    choosenElQ() {
      let time = !this.electronQueu.unavailable
        ? this.electronQueu.choosenTime
        : "";
      if (this.getElQDate) {
        if (time != "") {
          this.$emit("validQueueDate", this.getElQDate + " " + time);
          return this.getElQDate + " " + time;
        } else {
          return "Данное время недоступно";
        }
      }
      return false
    },
  },
};
</script>

<style>
.hooper-next,
.hooper-prev {
  padding: 5px;
  opacity: 0.5;
}

.hooper-next:hover,
.hooper-prev:hover {
  opacity: 1;
}

.hooper-slide span {
  line-height: 50px;
}

.available-dates-wrapper {
  display: flex;
  align-items: flex-start;
}

.date-and-time {
  min-width: 230px;
  margin-right: 30px;
  border: 1px solid #ebebeb;
  border-radius: 5px;
}

.available-dates-wrapper .date-and-time-title {
  position: relative;
  padding: 13px;
  font-size: 20px;
  font-family: "Open Sans", sans-serif;
  text-align: center;
  border-bottom: 1px solid #ebebeb;
}

.available-dates-wrapper .date-and-time-title .next-day,
.available-dates-wrapper .date-and-time-title .previous-day {
  position: absolute;
  top: -2px;
  width: 8px;
  height: 14px;
  padding-top: 25px;
  padding-bottom: 15px;
  background-image: url("../assets/img/chevron.png");
  background-repeat: no-repeat;
  background-position: center center;
  cursor: pointer;
}

.available-dates-wrapper .date-and-time-title .previous-day {
  left: 8px;
  padding-right: 20px;
  transform: rotate(180deg);
}

.available-dates-wrapper .date-and-time-title .next-day {
  right: 8px;
  padding-left: 20px;
}

.available-dates-wrapper .hooper-slide.is-current {
  margin-right: 30px;
  margin-left: 30px;
  color: #f8d75c;
  border-top: 1px solid #ebebeb;
  border-bottom: 1px solid #ebebeb;
}

.hooper-slide .not_available {
  color: #adadad;
}

@media (max-width: 992px) {
  .available-dates-wrapper {
    flex-direction: column;
  }

  .available-dates-wrapper input {
    max-width: 400px;
    width: 100%;
    text-align: center;
    font-size: 18px;
  }

  .date-and-time {
    order: 1;
    width: 100%;
    max-width: 400px;
    margin-right: 0;
  }

  .available-dates-wrapper .date-and-time-title {
    font-size: 18px;
  }
}
</style>
