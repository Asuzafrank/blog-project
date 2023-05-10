<template>
  <Header />
  <div class="container">
    <h1 class="text-center mt-5 p-3">post a blog</h1>
    <div class="post-blog-inputs">
      <div>
        <label style="display: block; margin-bottom: 10px" for="title"
          >blog-title</label
        >
        <input
          type="text"
          id="title"
          placeholder="enter post title"
          v-model="title"
        />
      </div>
      <div class="">
        <label style="display: block; margin-bottom: 10px" for="content"
          >blog-content</label
        >
        <textarea id="content" cols="38" rows="3" v-model="content"></textarea>
      </div>
      <button @click="post" class="btn btn-primary mt-3" style="width: 300px">
        post
      </button>
    </div>
  </div>
</template>
<script>
import Header from "../components/Header.vue";

import axios from "axios";
export default {
  name: "Post",
  components: {
    Header,
  },
  data() {
    return {
      title: "",
      content: "",
      date: "",
      user_id: null,
      name: "",
    };
  },
  methods: {
    getUserId() {
      const user = JSON.parse(localStorage.getItem("user.info"));
      if (user) {
        return user.id;
      }
      return;
    },

    async post() {
      if (!this.title || !this.content) {
        alert("please fill in the required fields");
        return;
      }

      const userId = this.getUserId();
      if (!userId) {
        alert("Please log in to make a booking.");
        this.$router.push({ name: "login" });
        return;
      }
      let result = await axios.post("http://localhost:3000/blogs", {
        title: this.title,
        content: this.content,
        date: new Date().toLocaleDateString(),
        user_id: userId,
      });
      console.log(result);
    },
  },
};
</script>
<style scoped>
.post-blog-inputs {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
}
.text-center {
  color: steelblue;
}
input {
  width: 300px;
  padding: 10px;
  border: 1px solid grey;
  border-radius: 10px;
}
label {
  font-size: 20px;
  color: steelblue;
  font-weight: bold;
}
textarea {
  border: 1px solid grey;
  border-radius: 10px;
}
</style>