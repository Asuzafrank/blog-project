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
          <h1 class="text-bold">Welcome To Our Website</h1>
        </div>
        <div class="sign-inputs">
          <label for="username" style="display: block; margin-bottom: 10px"
            >username:</label
          >
          <input
            id="username"
            type="text"
            name="username"
            placeholder="Enter your name"
            v-model="username"
          />
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
            placeholder="Enter Password"
            v-model="password"
          />
        </div>
        <div class="sign-inputs">
          <label
            for="password_confirm"
            style="display: block; margin-bottom: 10px"
            >confirm password:</label
          >
          <input
            id="password_confirm"
            type="password"
            name="password_confirm"
            placeholder="Enter Password"
            v-model="confirm_password"
          />
        </div>
        <div>
          <button @click="signup">Sign Up</button>
        </div>
      </div>
      <p>Have an Account <router-link to="/login">login</router-link></p>
    </div>
  </div>
</template>


<script>
import axios from "axios";
// @ is an alias to /src

export default {
  name: "HomeView",
  components: {},
  data() {
    return {
      username: "",
      email: "",
      password: "",
      confirm_password: "",
    };
  },
  methods: {
    async signup() {
      if (
        !this.username ||
        !this.email ||
        !this.password ||
        !this.confirm_password
      ) {
        alert("please fill in the required fields");
        return;
      }
      if (this.password !== this.confirm_password) {
        alert("password do not match");
      } else {
        let result = await axios.post("http://localhost:3000/users", {
          username: this.username,
          email: this.email,
          password: this.password,
          confirm_password: this.confirm_password,
        });
        if (result.status == 201) {
          localStorage.setItem("user.info", JSON.stringify(result));
          this.$router.push({ name: "login" });
        }
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