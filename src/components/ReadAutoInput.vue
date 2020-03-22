<template>
  <div>
    <el-popover
      placement="bottom-start"
      popper-class="shadow"
      width="100%"
      trigger="click"
      @show="handleShow"
      v-model="flag"
    >
      <el-autocomplete
        ref="autoInput"
        v-model="stateVal"
        :fetch-suggestions="fetchSuggestions"
        :autofocus="false"
        :value-key="valueKey"
        :debounce="100"
        @select="handleSelect"
        :style="{'min-width': minWidth - 22 + 'px'}"
      ></el-autocomplete>
      <el-input
        v-model="currentValue"
        :readonly="true"
        @focus="setMinWidth"
        slot="reference"
      ></el-input>
    </el-popover>
  </div>
</template>

<script>
export default {
  name: "ReadAutoInput",
  data() {
    return {
      minWidth: 0,
      currentValue: this.value,
      stateVal: "",
      flag: false
    };
  },
  props: {
    value: String,
    valueKey: {
      //输入建议对象中用于显示的键名
      type: String,
      default: "value"
    },
    fetchSuggestions: {
      type: Function,
      default: function() {}
    }
  },
  watch: {
    value(newVal) {
      //console.log("newVal", newVal);
      this.currentValue = newVal;
    },
  },
  methods: {
    handleShow() {
      this.$nextTick(() => {
        this.$refs.autoInput.focus();
      });
    },
    handleSelect(item) {
      console.log("item",item);
      this.currentValue = item[this.valueKey];
      this.flag = false;
      this.$emit("input", this.currentValue);
    },
    setMinWidth(val) {
      //console.log("val", val);
      this.minWidth = val.srcElement.clientWidth;
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="scss">
.el-popover {
  height: 315px;
}
.shadow {
  box-shadow: none !important;
}
</style>
