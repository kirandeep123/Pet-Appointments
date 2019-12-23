<template>
  <div clas="col-12 col-md-10 col-lg-7">
    <div class="list-group list-group-flush">
      <div
        class="list-group-item d-flex align-items-start"
        :key="appointment.aptId"
        v-for="appointment in appointments"
      >
        <button
          @click="$emit('remove', appointment)"
          class="mr-2 btn btn-sm btn-danger"
        >
          <font-awesome-icon icon="trash" />
        </button>
        <div class="w-100">
          <div class="d-flex justify-content-between">
            <span class="h4 text-primary" contenteditable="contenteditable" @blur="$emit('edit',appointment.aptId,'petName',$event.target.innerText)" >{{              appointment.petName
            }}</span>
            <span class="float-right">{{
              formattedDate(appointment.aptDate)
            }}</span>
          </div>
          <div class="owner-name">
            <span contenteditable="contenteditable" @blur="$emit('edit',appointment.aptId,'petOwner',$event.target.innerText)" class="font-weight-bold text-primary mr-1">Owner:</span>
            <span>{{ appointment.petOwner }}</span>
          </div>
          <div>{{ appointment.aptNotes }}</div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { FontAwesomeIcon } from "@fortawesome/vue-fontawesome";
import moment from "moment";

export default {
  name: "AppointmentsList",
  props: ["appointments"],
  components: {
    FontAwesomeIcon
  },
  methods: {
    formattedDate: function(date) {
      return new moment(new Date(date)).format("MM-DD-YYYY h:mm");
    }
  }
};
</script>

<style></style>
