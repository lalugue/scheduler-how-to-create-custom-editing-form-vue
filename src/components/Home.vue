<template>
  <div class="long-title">
    <h3>DXCinema Upcoming Movies</h3>
  </div>

  <DxScheduler
    id="scheduler"
    :data-source="dataSource"
    :views="views"
    current-view="day"
    :current-date="currentDate"
    :first-day-of-week="0"
    :start-day-hour="9"
    :end-day-hour="23"
    :show-all-day-panel="false"
    :height="600"
    :on-appointment-form-opening="onAppointmentFormOpening"
    :editing="editing"
  >
  </DxScheduler>

  <DxPopup
    :width="500"
    :closeOnOutsideClick="true"
    v-model:visible="isCustomPopupVisible"
    >
    <template #content>
      <DxScrollView
        width="100%"
        height="100%"
      >       
      <img :src="editAppointmentData.image" class="dx-field-label" />
      <div class="dx-field-label">
        <p>
          <b>{{ editAppointmentData.text }}</b>
        </p>
        <p>Year: {{ editAppointmentData.year }}</p>
        <p>Duration: {{ editAppointmentData.duration }} minutes</p>
      </div>

      <div class="dx-field-label">
        <b>{{ formatDate(editAppointmentData.startDate, "shortTime") }} -
          {{ formatDate(editAppointmentData.endDate, "shortTime") }}</b>
      </div>

      <div class="dx-field-label"><b>Price ($): </b></div>
      <div id="priceView" class="dx-field-label">
        {{
          editAppointmentData.seatRow && editAppointmentData.seatNumber
            ? setSeatPrice(
                editAppointmentData.price,
                editAppointmentData.seatRow
              )
            : "Pick a seat for pricing"
        }}
      </div>      

      <DxSelectBox
        id="rowView"
        class="dx-field-label"
        :dataSource="rows"
        :width="400"
        placeholder="Pick a row"
        v-model:value="editAppointmentData.seatRow">
      </DxSelectBox>

      <DxSelectBox
        id="seatView"
        class="dx-field-label"
        :dataSource="seats"
        :width="400"
        placeholder="Pick a seat"
        v-model:value="editAppointmentData.seatNumber">
      </DxSelectBox>
      </DxScrollView>
    </template>
  </DxPopup>

</template>

<script>
import { DxScheduler } from "devextreme-vue/scheduler";
import { DxPopup } from "devextreme-vue/popup";
import { DxScrollView } from "devextreme-vue/scroll-view"
import {DxSelectBox} from "devextreme-vue/select-box"
import { formatDate } from "devextreme/localization";

import { data, rows, seats } from "./data.js";

export default {
  name: "Home", 
  components: {
    DxScheduler,
    DxPopup,
    DxScrollView,
    DxSelectBox
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
  methods: {
    onAppointmentFormOpening(e) {
      e.cancel = true;
      this.editAppointmentData = { ...e.appointmentData };    
      if(this.editAppointmentData.id){
        this.isCustomPopupVisible = true;
      }      
    },
    formatDate
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
