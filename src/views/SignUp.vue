<template>
  <div class="container mt-4 mb-4">
    <div class="row">
      <div
        id="lf"
        class="col-4 d-flex flex-column align-items-center justify-content-center"
        style="height: 80vh"
      >
        <img src="../assets/logo-grey.png" class="img-fluid" alt="" />
        <h6>wanna feel alive,come and chart with others</h6>
      </div>
      <div
        class="col-8 d-flex flex-column align-items-center justify-content-center"
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
          />
        </div>
        <div>
          <button>Sign Up</button>
        </div>
      </div>
    </div>
  </div>
</template>


<script>
// @ is an alias to /src

export default {
  name: "HomeView",
  components: {},
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