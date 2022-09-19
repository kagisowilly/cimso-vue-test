<template>
  <nav :class="{ change_color: scrollPosition > 50 }">
    <div class="nav-div container">
      <div>
        <router-link to="/">Unit Types</router-link>
        <router-link to="/bookingunits">Booking Units </router-link>
      </div>
      <div>
        <h1>CIMSO</h1>
      </div>
    </div>
  </nav>
</template>

<script>
export default {
    data() {
    return {
      scrollPosition: null,
    };
  },
  mounted() {
    window.addEventListener("scroll", this.updateScroll);
  },
  methods: {
    updateScroll() {
      this.scrollPosition = window.scrollY;
    },
  },
};
</script>

<style scoped>
.change_color {
  background-color: rgb(23, 57, 227);
}
nav a {
  font-weight: bold;
  color: #61a7ec;
  margin: 5px;
  text-decoration: navy;
}
a:hover {
  color: #f1f1f1;
}

nav a.router-link-exact-active {
  color: rgb(23, 57, 227);
  background-color: #fff;
  padding: 5px;
  border-radius: 20px;
}
nav {
  position: fixed;
  top: 0;
  width: 100%;
  z-index: 999;
  background: rgb(23, 57, 227,0.25);
}
h1 {
  color: #61a7ec;
  margin: 0 !important;
}
.nav-div {
  display: flex;
  align-items: center;
  justify-content: space-between;
  height: 70px;
}
</style>
