<template>
  <div id="app">
    <v-select name="school" v-model="school" :sel="school" :options="list" :val="val" :names="name"></v-select>

    <p>134312342</p>
    <v-select name="school" v-model="school" :sel="school" :options="list" :val="name" :names="val"></v-select>
  </div>
</template>

<script>
import vsel from "./v-select";

export default {
  components: {
    "v-select": vsel
  },
  name: "app",
  data() {
    return {
      school: { name: "test", value: 123 },
      val: "value",
      name: "name",
      school3: { name: "lll", value: 0 },
      msg: "Welcome to Your Vue.js App",
      list: [
        { name: "test", value: 123 },
        { name: "teserqwrqwrqwt", value: 103 },
        { name: "tesrqwerwrt", value: 13 },
        { name: "tesrwerqwrqwrrrrrrrt", value: 12 },
        { name: "tesrwerqwrqwrrrrrrrt", value: 12 },
        { name: "tesrwerqwrqwrrrrrrrt", value: 12 },
        { name: "test", value: 123 },
        { name: "teserqwrqwrqwt", value: 103 },
        { name: "tesrqwerwrt", value: 13 },
        { name: "tesrwerqwrqwrrrrrrrt", value: 12 },
        { name: "tesrwerqwrqwrrrrrrrt", value: 12 },
        { name: "tesrwerqwrqwrrrrrrrt", value: 12 },
        { name: "test", value: 123 },
        { name: "teserqwrqwrqwt", value: 103 },
        { name: "tesrqwerwrt", value: 13 },
        { name: "tesrwerqwrqwrrrrrrrt", value: 12 },
        { name: "tesrwerqwrqwrrrrrrrt", value: 12 },
        { name: "tesrwerqwrqwrrrrrrrt", value: 12 },
        { name: "tesrwerqwrqwrrrrrrrt", value: 12 }
      ]
    };
  },
  watch: {
    school: function(val) {
      console.log(val);
    }
  },
  methods: {}
};
</script>

<style>
</style>
