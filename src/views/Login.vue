<template>
  <div class="container mt-4 mb-4">
    <div class="row">
      <div
        id="lf"
        class="col-md-6 col-lg-4 d-flex flex-column align-items-center justify-content-center"
        style="height: 80vh"
      >
        <img src="../assets/logo-grey.png" class="img-fluid" alt="" />
        <h6>wanna feel alive,come and chart with others</h6>
      </div>
      <div
        class="col-md-6 col-lg-8 d-flex flex-column align-items-center justify-content-center"
      >
        <div class="">
          <h1 class="text-bold">Login</h1>
        </div>

        <div class="sign-inputs">
          <label for="email" style="display: block; margin-bottom: 10px"
            >email:</label
          >
          <input
            id="email"
            type="email"
            name="email"
            placeholder="example@gmail.com"
            v-model="email"
          />
        </div>
        <div class="sign-inputs">
          <label for="password" style="display: block; margin-bottom: 10px"
            >password:</label
          >
          <input
            id="password"
            type="password"
            name="password"
            placeholder="Enter password"
            v-model="password"
          />
        </div>

        <div>
          <button @click="login">Login</button>
        </div>
      </div>
    </div>
  </div>
</template>


<script>
// @ is an alias to /src
import axios from "axios";
export default {
  name: "HomeView",
  components: {},
  data() {
    return {
      email: "",
      password: "",
    };
  },
  methods: {
    async login() {
      let result = await axios.get(
        `http://localhost:3000/users?email=${this.email}& password=${this.password}`
      );
      if (result.status == 200 && result.data.length > 0) {
        localStorage.setItem("user.info", JSON.stringify(result.data[0]));
        this.$router.push({ name: "home" });
      }
    },
  },
};
</script>
<style scoped>
.container {
  box-shadow: 0px 0px 10px rgba(129, 30, 30, 0.2);
  border-radius: 10px;
}
#lf {
  background-color: lightgreen;
}
.sign-inputs {
  padding: 10px;
  display: block;
}
input {
  width: 300px;
  padding: 10px;
  border: 2px solid lightgreen;
  border-radius: 5px;
}
label {
  font-weight: bold;
}
button {
  width: 300px;
  padding: 10px;
  border-radius: 5px;
  background-color: lightgreen;
}
</style>