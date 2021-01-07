<template>
  <div class="container container-small filter-tabs">
    <h1 class="filter-tabs-title">
      Выберите свой красивый номер
    </h1>

    <tabs :options="{ useUrlFragment: false }">
      <!-- Random Search -->
      <tab
        prefix="<span class='filter-icon filter-icon-random'></span> "
        name="Произвольный"
      >
        <p>Нажмите кнопку, и мы найдем для вас самые красивые номера</p>
        <div class="filter-fields">
          <button
            class="btn-main"
            :class="{ loading: false }"
          >
            <span>Подобрать</span>
            <button-preloader></button-preloader>
          </button>
        </div>
      </tab>

      <!-- Search by number -->
      <tab
        prefix="<span class='filter-icon filter-icon-number'></span> "
        name="Подбор по номеру"
      >
        <p>Подберите себе номер с вашим любимым числом. Укажите от 1 до 7 цифр в поле ввода.</p>
        <div class="filter-fields">
          <div>
            <app-select
              :options="[
                { name: '90', value: '90' },
                { name: '91', value: '91' },
              ]"
              v-model="filterByNumber.prefix"
            ></app-select>
            <input
              class="ml30"
              type="number"
              maxlength="7"
              placeholder="12345"
            />
          </div>
          <button
            :class="{ loading: false }"
            class="btn-main ml30"
          >
            <span>Подобрать</span>
            <button-preloader></button-preloader>
          </button>
        </div>
      </tab>

      <!-- Search by Group -->
      <tab
        prefix="<span class='filter-icon filter-icon-several-numbers'></span> "
        name="Несколько номеров"
      >
        <p>Подберите номера для всей семьи. Укажите количество необходимых похожих номеров.</p>
        <div class="filter-fields">
          <app-select
            :options="searchByGroupLimit"
          ></app-select>
          <button
            :class="{ loading: false }"
            class="btn-main ml30"
          >
            <span>Подобрать</span>
            <button-preloader></button-preloader>
          </button>
        </div>
      </tab>

      <!-- Search by Date -->
      <tab
        prefix="<span class='filter-icon filter-icon-by-date'></span> "
        name="По дате"
      >
        <p>Подберите себе номер по цифрам важной для вас даты. Введите день, месяц и год.</p>
        <div class="filter-fields">
          <date-pick
            :inputAttributes="{ readonly: true }"
            :format="'DD.MM.YYYY'"
          ></date-pick>
          <button
            :class="{ loading: false }"
            class="btn-main ml30"
          >
            <span>Подобрать</span>
            <button-preloader></button-preloader>
          </button>
        </div>
      </tab>

      <!-- Search by Mask -->
      <tab
        prefix="<span class='filter-icon filter-icon-by-mask'></span> "
        name="По маске"
      >
        <p>Подберите рисунок нового номера на ваш вкус: легко запоминающийся, красивый или содержащий счастливое число</p>
        <div class="filter-fields">
          <div>
            <app-select
              :options="[
                { name: '90', value: '90' },
                { name: '91', value: '91' },
              ]"
              v-model="filterByMask.prefix"
            ></app-select>
            <masked-input
              class="ml30"
              v-model="filterByMask.number"
              mask="111-11-11"
              placeholder-char="X"
            />
          </div>
          <button
            :class="{ loading: false }"
            class="btn-main ml30"
          >
            <span>Подобрать</span>
            <button-preloader></button-preloader>
          </button>
        </div>
      </tab>
    </tabs>
  </div>
</template>

<script>
import { Tabs, Tab } from 'vue-tabs-component';
import DatePick from "vue-date-pick";
import "vue-date-pick/dist/vueDatePick.css";
import MaskedInput from "vue-masked-input";

import AppSelect from "./AppSelect";
import ButtonPreloader from "./ButtonPreloader";

export default {
  data() {
    return {
      filterByMask: {
        prefix: "90",
        number: "XXXXXXX",
      },
      filterByNumber: {
        prefix: "90",
        number: "",
      },
      searchByGroupLimit: [{name: 2, value: 2}]
    };
  },
  components: {
    DatePick,
    AppSelect,
    MaskedInput,
    ButtonPreloader,
    Tabs,
    Tab,
  },
};
</script>

<style>
@import url("FilterTab.css");
</style>
