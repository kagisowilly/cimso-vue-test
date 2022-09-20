<template>
  <h1>Unit Types With Bookings</h1>

  <div v-if="unitTypesBookingUnits" class="container units">
    <div>
      <div class="row">
        <div
          v-for="unittype in unitTypesBookingUnits"
          :key="unittype['Booking Unit ID']"
          class="card col-12 col-md-4 col-sm-6 col-lg-3 p-2 g-2"
        >
          <h2 class="text-right">Unit Type</h2>
          <p class="text-start">
            Unit Type Id : {{ unittype["Unit Type ID"] }}
          </p>
          <p class="text-start">
            Unit Type Code : {{ unittype["Unit Type Code"] }}
          </p>
          <p class="text-start">
            Max Occupants : {{ unittype["Maximum Occupants"] }}
          </p>
          <p class="text-start">
            Max Adults : {{ unittype["Maximum Adults"] }}
          </p>
          <p class="text-start">
            Max Children : {{ unittype["Maximum Children"] }}
          </p>
          <p class="text-start">Location Id : {{ unittype["Location ID"] }}</p>
          <p class="text-start">Unit Count : {{ unittype["Unit Count"] }}</p>
          <p class="text-start">
            Unit Type Image UIDs : {{ unittype["Unit Type Image UIDs"] }}
          </p>
          <p class="text-start">
            Unit Type Description : {{ unittype["Unit Type Description"] }}
          </p>
          <p class="text-start">
            Unit Type Category : {{ unittype["Unit Type Category"] }}
          </p>

          <h2>Booking Unit</h2>

          <p class="text-start">
            Booking Unit ID : {{ unittype["Booking Unit ID"] }}
          </p>
          <p class="text-start">
            Booking Unit Number : {{ unittype["Booking Unit Number"] }}
          </p>
          <p class="text-start">
            Unit Type ID : {{ unittype["Unit Type ID"] }}
          </p>
          <p class="text-start">
            Booking Unit Name : {{ unittype["Booking Unit Name"] }}
          </p>
        </div>
      </div>
    </div>
  </div>
  <div v-else className="load">
    <div class="ring">
      Loading
      <span className="loader"></span>
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  components: {},
  data() {
    return {
      unitTypesBookingUnits: [],
    };
  },

  mounted() {
    const unitTypes =
      "https://apitest.cimsoweb.com/api/innterchange/unit_type_info_request";
    const bookingUnits =
      "https://apitest.cimsoweb.com/api/innterchange/get_booking_units_request";
    const firstFetch = axios.get(unitTypes);
    const secondFetch = axios.get(bookingUnits);
    axios
      .all([firstFetch, secondFetch])
      .then(
        axios.spread((...responses) => {
          const firstFetch = responses[0];
          const secondFetch = responses[1];
          const allUnits = firstFetch.data.payload["Unit Types"];
          const allBookings = secondFetch.data.payload["Booking Units"];
          this.unitTypesBookingUnits = allBookings.map((booking) => {
            const unitType = allUnits.find(
              (unit) => unit["Unit Type ID"] === booking["Unit Type ID"]
            );
            return { ...booking, ...unitType };
          });
        })
      )
      .catch((errors) => {
        console.error(errors);
      });
  },
};
</script>

<style scoped>
h1 {
  margin-top: 100px;
}
p {
  margin-bottom: 5px !important;
}
.card {
  border: solid 1px rgb(23, 57, 227);
  background-color: transparent;
}
/* LOADER */
.load {
  display: flex;
  justify-content: center;
  align-items: center;
  width: 100%;
  height: 80vh;
}
.ring {
  position: absolute;
  width: 150px;
  height: 150px;
  background: transparent;
  border: 3px solid #3c3c3c;
  border-radius: 50%;
  text-align: center;
  line-height: 150px;
  font-family: sans-serif;
  font-size: 20px;
  color: rgb(23, 57, 227);
  letter-spacing: 4px;
  text-transform: uppercase;
  text-shadow: 0 0 10px rgb(23, 57, 227);
  box-shadow: 0 0 20px rgba(0, 0, 0, 0.5);
}
.ring:before {
  content: "";
  position: absolute;
  top: -3px;
  left: -3px;
  width: 100%;
  height: 100%;
  border: 3px solid transparent;
  border-top: 3px solid rgb(23, 57, 227);
  border-right: 3px solid rgb(23, 57, 227);
  border-radius: 50%;
  animation: animateC 2s linear infinite;
}
.span {
  display: block;
  position: absolute;
  top: calc(50% - 2px);
  left: 50%;
  width: 50%;
  height: 4px;
  background: transparent;
  transform-origin: left;
  animation: animate 2s linear infinite;
}
.loader:before {
  content: "";
  position: absolute;
  width: 16px;
  height: 16px;
  border-radius: 50%;
  background: rgb(23, 57, 227);
  top: -6px;
  right: -8px;
  box-shadow: 0 0 20px rgb(23, 57, 227);
}
@keyframes animateC {
  0% {
    transform: rotate(0deg);
  }
  100% {
    transform: rotate(360deg);
  }
}
@keyframes animate {
  0% {
    transform: rotate(45deg);
  }
  100% {
    transform: rotate(405deg);
  }
}
</style>
