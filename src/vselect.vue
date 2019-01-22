<template>
  <div
    v-clickoutside="handleClose"
    class="select-wrapper"
    @click.prevent="selF"
    :class="{'active':selFlag}"
    :style="{'z-index':min}"
  >
    <div class="inners"><input type="text" :readonly="search==false?readonly:false"  v-model="selectV" @input="getV"></div>
    <div class="arrow" @click.stop="selF"></div>
    <ul v-show="selFlag" v-if="optionsL.length>0">
      <li
        
        :class="{'active':models.value==item.value}"
        v-for="(item,index) in optionsL"
        :key="index"
        :value="item[val]"
        @click.stop="sels(item)"
      >{{item[names]}}</li>
      
    </ul>
    <div class="ul" v-else>暂无数据</div>
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
  props: ["options", "sel", "val", "names","search"],
  data() {
    return {
      selFlag: false,
      models: "",
      optionsL:[],
      selectV:'',
      min: 0
    };
  },
  methods: {
    selF() {
      this.min = 100;
      this.selFlag = !this.selFlag;
    },
    init() {
      this.models = this.sel;
      this.optionsL = this.options;
      this.selectV = this.models[this.names];
    },
    sels(item) {
      this.models = item;
      this.selectV = item[this.names];
      this.selFlag = !this.selFlag;
      this.$emit("change", item);
    },
    handleClose() {
      this.min = 0;
      this.selFlag = false;
    },
    getV(){
      console.log(this.selectV,this.names);
      if(this.selectV==''){
        return this.optionsL = this.options;
      }
     const arr = this.optionsL.filter((item)=>{
       return  item[this.names].toString().indexOf(this.selectV)>=0;
      })
      this.optionsL = arr;
    }
  },
  mounted() {
    this.init();
  }
};
</script>
<style scoped>
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
.inners input{
  outline:0 none;
  border:0 none;
  background-image:0 none;
  cursor: pointer;
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
.select-wrapper ul {
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
  min-width: 100%;
}
.ul{
  width:100%;
  bottom: 0;
  transform: translateY(101%);
  left: 0;
  position:absolute;
  background:#fff;
  color:#333;
  border:1px solid #999;
}
.select-wrapper li {
  padding: 0 45px 0 0;
  background: #fff;
}
.select-wrapper li:hover {
  background: #1e90ff;
  color: #fff;
}
.select-wrapper li.active {
  background: #1e90ff;
  color: #fff;
}
</style>