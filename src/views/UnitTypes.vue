<template>
  <h1>Unit Types</h1>
  <div v-if="payload" class="unit-types">
    <div v-for="payload_data of payload" :key="payload_data">
      <div v-for="payload of payload_data" :key="payload" class="container">
        <div class="row">
          <div
            v-for="payloads of payload"
            :key="payloads"
            class="col-12 col-md-4 col-sm-6 col-lg-3 g-2"
          >
            <div class="card">
              <!-- <img src="..." class="card-img-top" alt="..." /> -->
              <div class="card-body">
                <p class="text-start">
                  <span>Unit Type ID:</span> {{ payloads["Unit Type ID"] }}
                </p>
                <p class="text-start">
                  <span>Unit Type Code:</span> {{ payloads["Unit Type Code"] }}
                </p>
                <p class="text-start">
                  <span>Unit Type Description:</span>
                  {{ payloads["Unit Type Description"] }}
                </p>
                <p class="text-start">
                  <span>Unit Type Category: </span>
                  {{ payloads["Unit Type Category"] }}
                </p>
                <p class="text-start">
                  <span>Maximum Occupants:</span>
                  {{ payloads["Maximum Occupants"] }}
                </p>
                <p class="text-start">
                  <span>Maximum Adults:</span> {{ payloads[""] }}
                </p>
                <p class="text-start">
                  <span>Maximum Children: </span>
                  {{ payloads["Maximum Children"] }}
                </p>
                <p class="text-start">
                  <span>Unit Type Description:</span>
                  {{ payloads["Unit Type Description"] }}
                </p>
                <p class="text-start">
                  <span>Location ID:</span> {{ payloads["Location ID"] }}
                </p>
                <p class="text-start">
                  <span>Unit Count:</span> {{ payloads["Unit Count"] }}
                </p>
                <p class="text-start">
                  <span>Unit Type Image UIDs:</span>
                  {{ payloads["Unit Type Image UIDs"] }}
                </p>
              </div>
            </div>
          </div>
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
export default {
  data() {
    return {
      payload: null,
    };
  },

  mounted() {
    fetch(
      "https://apitest.cimsoweb.com/api/innterchange/unit_type_info_request"
    )
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
  /* LOADER */
.load{
  display: flex;
  justify-content: center;
  align-items: center;
  width: 100%;
  height: 80vh;
}
.ring
{
  position:absolute;
  width:150px;
  height:150px;
  background:transparent;
  border:3px solid #3c3c3c;
  border-radius:50%;
  text-align:center;
  line-height:150px;
  font-family:sans-serif;
  font-size:20px;
  color:rgb(23, 57, 227);
  letter-spacing:4px;
  text-transform:uppercase;
  text-shadow:0 0 10px rgb(23, 57, 227);
  box-shadow:0 0 20px rgba(0,0,0,.5);
}
.ring:before
{
  content:'';
  position:absolute;
  top:-3px;
  left:-3px;
  width:100%;
  height:100%;
  border:3px solid transparent;
  border-top:3px solid rgb(23, 57, 227);
  border-right:3px solid rgb(23, 57, 227);
  border-radius:50%;
  animation:animateC 2s linear infinite;
}
.span
{
  display:block;
  position:absolute;
  top:calc(50% - 2px);
  left:50%;
  width:50%;
  height:4px;
  background:transparent;
  transform-origin:left;
  animation:animate 2s linear infinite;
}
.loader:before
{
  content:'';
  position:absolute;
  width:16px;
  height:16px;
  border-radius:50%;
  background:rgb(23, 57, 227);
  top:-6px;
  right:-8px;
  box-shadow:0 0 20px rgb(23, 57, 227);
}
@keyframes animateC
{
  0%
  {
    transform:rotate(0deg);
  }
  100%
  {
    transform:rotate(360deg);
  }
}
@keyframes animate
{
  0%
  {
    transform:rotate(45deg);
  }
  100%
  {
    transform:rotate(405deg);
  }
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
.card{
    background-color:transparent;
    min-height: 470px;
    border: solid 1px rgb(23, 57, 227);
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
  .card{
    min-height: auto !important;
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
