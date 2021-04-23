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
    @onAppointmentFormOpening="onAppointmentFormOpening"
    :editing="editing"
  >
  </DxScheduler>
</template>

<script>
import { DxScheduler } from "devextreme-vue/scheduler";
//import { DxPopup } from "devextreme-vue/popup";
//import { DxScrollView } from "devextreme-vue/scroll-view"

import { data, rows, seats } from "./data.js";

export default {
  name: "Home", 
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
      editAppointmentData: {},
      isCustomPopupVisible: false,
      editing: {allowResizing: false, allowDragging: false}
    };
  },
  computed: {
    getText() {
      return `Click count: ${this.count}`;
    },
  },
  methods: {
    onAppointmentFormOpening(e) {
      e.cancel = true;
      this.editAppointmentData = { ...e.appointmentData };    
      if(this.editAppointmentData.id){
        this.isCustomPopupVisible = true;
      }      
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
