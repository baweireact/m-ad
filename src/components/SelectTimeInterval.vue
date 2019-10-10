<template>
  <div>
    <div v-for="(item, index) in initData" :key="item.id">
      <el-checkbox
        :indeterminate="item.isIndeterminate"
        v-model="item.checked"
        @change="handleWeek(index, $event)"
      >{{item.week}}</el-checkbox>
      <span
        v-for="(hourItem,hourIndex) in item.hours"
        :key="hourIndex"
        class="m-hour"
        :class="{active: hourItem.checked}"
        @click="handleHour(index, hourIndex)"
      >{{hourItem.hour}}</span>
    </div>
  </div>
</template>

<script>
export default {
  model: {
    prop: "initData",
    //event: "change"
  },
  props: ["initData"],
  methods: {
    handleHour(index, hourIndex) {
      this.initData[index].hours[hourIndex].checked = !this.initData[index]
        .hours[hourIndex].checked;

      let count = this.initData[index].hours.filter(
        item => item.checked === false
      ).length;

      if (this.initData[index].hours.length > count && count > 0) {
        this.initData[index].isIndeterminate = true;
      } else {
        this.initData[index].isIndeterminate = false;
      }

      this.initData[index].checked = !(this.initData[index].hours.length === count);

    },
    handleWeek(index, checked) {
      this.initData[index].hours.forEach(item => {
        item.checked = checked;
      });
    }
  },
  updated() {
    //this.$emit("change", this.initData);
  }
};
</script>

<style>
</style>