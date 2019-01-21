<template>
  <div
    v-clickoutside="handleClose"
    class="select-wrapper"
    @click.prevent="selF"
    :class="{'active':selFlag}"
    :style="{'z-index':min}"
  >
    <div class="inners">{{models[names]}}</div>
    <div class="arrow" @click.stop="selF"></div>
    <ul v-show="selFlag">
      <li
        :class="{'active':models.value==item.value}"
        v-for="(item,index) in options"
        :key="index"
        :value="item[val]"
        @click.stop="sels(item)"
      >{{item[names]}}</li>
    </ul>
  </div>
</template>
<script>
import clickoutside from "./close";
export default {
  directives: { clickoutside },
  model: {
    prop: "sel",
    event: "change"
  },
  props: ["options", "sel", "val", "names"],
  data() {
    return {
      selFlag: false,
      models: "",
      min: 0
    };
  },
  methods: {
    selF() {
      this.min = 100;
      this.selFlag = !this.selFlag;
    },
    init() {
      console.log(clickoutside);
      this.models = this.sel;
    },
    sels(item) {
      this.models = item;
      this.selFlag = !this.selFlag;
      this.$emit("change", item);
    },
    handleClose() {
      this.min = 0;
      this.selFlag = false;
    }
  },
  mounted() {
    this.init();
  }
};
</script>
<style>
.select-wrapper {
  width: 120px;
  border: 1px solid #999;
  padding: 2px 30px 0 5px;
  font-size: 12px;
  height: 18px;
  position: relative;
  z-index: -1;
}
.inners {
  padding-right: 30px;
  overflow: hidden;
}
.select-wrapper .arrow {
  position: absolute;
  top: 50%;
  right: 10px;
  z-index: 30;
  transform: translateY(-50%);
  border-top: 5px solid #999;
  border-left: 5px solid transparent;
  border-right: 5px solid transparent;
}
.active {
  box-shadow: 0 0 3px #1e90ff;
}
ul {
  list-style: none;
  margin: 0;
  padding: 0;
  width: fit-content;
  text-align: left;
  position: absolute;
  max-height: 160px;
  overflow-y: auto;
  bottom: 0;
  transform: translateY(101%);
  left: 0;
  z-index: 10;
  background: #fff;
  border: 1px solid #1e90ff;
}
li {
  padding: 0 45px 0 0;
  background: #fff;
}
li:hover {
  background: #1e90ff;
  color: #fff;
}
li.active {
  background: #1e90ff;
  color: #fff;
}
</style>