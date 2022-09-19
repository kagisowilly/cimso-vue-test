<template>
    <h1>Booking Units</h1>
  <div class="unit-types">
    <div v-for="payload_data in payload" :key="payload_data">
      <div v-for="payload in payload_data" :key="payload" class="container">
        <div class="row">
          <div
            v-for="payloads in payload"
            :key="payloads"
            class="col-12 col-md-4 col-sm-6 col-lg-3 g-2"
          >
            <div class="card">
              <!-- <img src="..." class="card-img-top" alt="..." /> -->
              <div class="card-body">
                <p class="text-start">
                  <span>Booking Unit ID:</span> {{ payloads["Booking Unit ID"] }}
                </p>
                <p class="text-start">
                  <span>Booking Unit Name:</span> {{ payloads["Booking Unit Name"] }}
                </p>
                <p class="text-start">
                  <span>Booking Unit Number: </span>
                  {{ payloads["Booking Unit Number"] }}
                </p>
                <p class="text-start">
                  <span>Unit Type ID:</span>
                  {{ payloads["Unit Type ID"] }}
                </p>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      payload: null,
    };
  },

  mounted() {
    fetch("https://apitest.cimsoweb.com/api/innterchange/get_booking_units_request")
      .then((res) => res.json())
      .then((payload_data) => {
        console.log(this.payload_data);
        this.payload = payload_data;
      });
  },
  method: {},
};
</script>

<style scoped>
  .card{
    background-color:transparent;
  }
.unit-types {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  align-items: center;
  min-height: 80vh;
}
p span{
  font-weight: bold;
}
p{
  margin-bottom: 5px !important;
}
h1{
  margin-top: 100px;
}
@media all and (max-width: 575px) {
  .row{
    width: 80%;
  }
  .container{
    display: flex;
    justify-content: center !important;
  }
}
@media all and (max-width: 430px) {
  .row{
    width: 90%;
  }
}
@media all and (max-width: 370px) {
  .row{
    width: 100%;
  }
}

</style>
