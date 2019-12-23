<template>
  <div id="main-app" class="container">
    <div class="row justify-content-center">
      <appointments-list
        :appointments="appointments"
        @remove="removeAppointment"
        @edit="editAppointment"
      />
    </div>
  </div>
</template>

<script>
import AppointmentsList from "./components/Appointments";
import axios from "axios";
import _ from "lodash";
export default {
  name: "MainApp",
  data: function() {
    return {
      title: "Pet Appointments",
      appointments: [],
      aptIndex: 0
    };
  },
  components: {
    AppointmentsList
  },
  mounted() {
    axios.get("./data/appointments.json").then(
      response =>
        (this.appointments = response.data.map(appointment => {
          appointment.aptId = this.aptIndex;
          this.aptIndex++;
          return appointment;
        }))
    );
  },
  methods: {
    removeAppointment(apt) {
      this.appointments = _.without(this.appointments, apt);
    },
    editAppointment(id,field,text){
     const appointmentToChange = this.appointments.filter(appointment=>appointment.aptId===id);
     console.log(appointmentToChange)
     this.appointments[appointmentToChange.aptId][field]=text;
    
    }
  }
};
</script>
