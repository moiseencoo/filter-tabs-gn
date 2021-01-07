<template>
  <div
    v-if="options"
    class="app-select"
    :tabindex="tabindex"
    @blur="open = false"
  >
    <div class="selected" :class="{ open: open }" @click="open = !open">
      {{ getSelected }}
    </div>
    <div class="items" :class="{ selectHide: !open }">
      <div
        class="item"
        v-for="(option, i) of options"
        :key="i"
        @click="selectOption(option)"
      >
        {{ option.name }}
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    options: {
      type: Array,
      required: true,
    },
    tabindex: {
      type: Number,
      required: false,
      default: 0,
    },
    predefined: {
      type: String | Number,
    },
  },
  data() {
    return {
      selected_name: null,
      open: false,
      selected_value: null,
    };
  },

  async mounted() {
    if (!this.getPredifined) {
      this.$emit("input", this.getValue);
    } else {
      await this.selectPredefined();
    }
  },
  computed: {
    getSelected() {
      return this.selected_name == null
        ? this.options[0].name
        : this.selected_name;
    },
    getValue() {
      return this.selected_value == null
        ? this.options[0].value
        : this.selected_value;
    },
    getPredifined() {
      return this.predefined;
    },
  },
  methods: {
    selectOption(option) {
      this.selected_name = option.name;
      this.selected_value = option.value;
      this.$emit("input", this.selected_value);
      this.open = false;
    },
    selectPredefined() {
      this.selected_value = this.getPredifined;
      let x = this.options.find((el) => el.value == this.selected_value);
      if (x) {
        this.selected_name = x.name;
        return this.$emit("input", x.value);
      }
    },
  },
  watch: {
    options() {
      this.selectPredefined();
    },
  },
};
</script>

<style scoped>
.app-select {
  position: relative;
  height: 43px;
  font-family: "Roboto", sans-serif;
  line-height: 41px;
  text-align: left;
  outline: none;
}

.selected {
  padding-right: 30px;
  padding-left: 8px;
  border: 1px solid #e5e5e5;
  border-radius: 3px;
  cursor: pointer;
  user-select: none;
}

.selected.open {
  border: 1px solid #f7d145;
  border-radius: 6px 6px 0 0;
}

.selected::after {
  position: absolute;
  top: 50%;
  right: 10px;
  width: 0;
  height: 0;
  border: 4px solid transparent;
  border-color: #000 transparent transparent transparent;
  transform: translateX(-50%);
  content: "";
}

.items {
  position: absolute;
  right: 0;
  left: 0;
  z-index: 999;
  overflow: hidden;
  background: #fff;
  border-right: 1px solid #f7d145;
  border-bottom: 1px solid #f7d145;
  border-left: 1px solid #f7d145;
  border-radius: 0 0 6px 6px;
}

.item {
  padding-left: 8px;
  font-size: 18px;
  cursor: pointer;
  user-select: none;
}

.item:hover {
  background-color: #f7d145;
}

.selectHide {
  display: none;
}
</style>
