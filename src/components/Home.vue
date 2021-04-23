<template>
  <div class="long-title">
    <h3>DXCinema Upcoming Movies</h3>
  </div>
  
  <DxScheduler
    id="scheduler"
    :data-source="dataSource"
    :views="views"
    currentView="day"
    :currentDate="currentDate"
    :firstDayOfWeek="0"
    :startDayHour="9"
    :endDayHour="23"
    :showAllDayPanel="false"
    :height="600"
  >
  </DxScheduler>
</template>

<script>
import DxScheduler from "devextreme-vue/scheduler";

import { data, rows, seats } from "./data.js";

export default {
  name: "Home",
  props: {
    msg: String,
  },
  components: {
    DxScheduler,
  },
  data() {
    return {
      dataSource: data,
      rows: rows,
      seats: seats,
      views: ["day", "timelineDay"],
      currentDate: new Date(2015, 4, 25),
    };
  },
  computed: {
    getText() {
      return `Click count: ${this.count}`;
    },
  },
  methods: {
    clickHandler() {
      this.count += 1;
    },
  },
};
</script>

<style scoped>
.long-title h3 {
  font-family: "Segoe UI Light", "Helvetica Neue Light", "Segoe UI",
    "Helvetica Neue", "Trebuchet MS", Verdana;
  font-weight: 200;
  font-size: 28px;
  text-align: center;
  margin-bottom: 20px;
}
</style>
