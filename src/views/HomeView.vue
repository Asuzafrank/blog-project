<template>
  <Header />
  <div class="container mt-5">
    <div class="row">
      <div class="col-8">
        <div v-for="blog in blogs" :key="blog.id">
          <div class="card w-100 mb-3">
            <div class="card-body">
              <div class="d-flex justify-content-between align-items-center">
                <h5 class="card-title">{{ blog.title }}</h5>
                <h6 class="text-secondary">date-posted: {{ blog.date }}</h6>
              </div>

              <hr />
              <p class="card-text">
                {{ blog.content }}
              </p>
              <div class="d-flex justify-content-between">
                <h6 class="data-name">posted by:{{ blog.user_name }}</h6>
                <button
                  @click="delpost(blog.id, blog.user_id)"
                  class="borderless-button"
                >
                  delete
                </button>
              </div>
            </div>
          </div>
        </div>
      </div>
      <div class="col-4">
        <div>
          <ListGroup />
        </div>
        <div>
          <Comments />
        </div>
      </div>
    </div>
    <nav aria-label="Page navigation example">
      <ul class="pagination justify-content-center">
        <li class="page-item" :class="{ disabled: currentPage === 1 }">
          <a
            class="page-link"
            href="#"
            aria-label="Previous"
            @click.prevent="prevPage()"
          >
            <span aria-hidden="true">&laquo;</span>
          </a>
        </li>
        <li
          class="page-item"
          v-for="page in pages"
          :key="page"
          :class="{ active: page === currentPage }"
        >
          <a class="page-link" href="#" @click.prevent="changePage(page)">{{
            page
          }}</a>
        </li>
        <li
          class="page-item"
          :class="{ disabled: currentPage === pages.length }"
        >
          <a
            class="page-link"
            href="#"
            aria-label="Next"
            @click.prevent="nextPage()"
          >
            <span aria-hidden="true">&raquo;</span>
          </a>
        </li>
      </ul>
    </nav>
  </div>
</template>

<script>
// @ is an alias to /src
import Header from "../components/Header.vue";
import ListGroup from "@/components/ListGroup.vue";
import Comments from "@/components/Comments.vue";
import axios from "axios";

export default {
  name: "HomeView",
  components: {
    Header,
    ListGroup,
    Comments,
  },
  data() {
    return {
      blogs: [],
      name: "",
      currentPage: 1,
      perPage: 2,
    };
  },
  computed: {
    totalPages() {
      return Math.ceil(this.blogs.length / this.perPage);
    },
    paginatedProducts() {
      const start = (this.currentPage - 1) * this.perPage;
      const end = start + this.perPage;
      return this.blogs.slice(start, end);
    },
    pages() {
      const pagesArray = [];
      for (let i = 1; i <= this.totalPages; i++) {
        pagesArray.push(i);
      }
      return pagesArray;
    },
  },
  methods: {
    getUserName() {
      let user = localStorage.getItem("user.info");
      this.name = JSON.parse(user).username;
    },
    prevPage() {
      if (this.currentPage > 1) {
        this.currentPage--;
      }
    },
    nextPage() {
      if (this.currentPage < this.totalPages) {
        this.currentPage++;
      }
    },
    changePage(page) {
      this.currentPage = page;
    },
    async loadData() {
      let user = localStorage.getItem("user.info");
      this.name = JSON.parse(user).username;

      let result = await axios.get("http://localhost:3000/blogs");
      this.blogs = result.data;
    },
    async delpost(id, user_id) {
      let user = localStorage.getItem("user.info");
      let currentUser = JSON.parse(user).id;

      if (currentUser !== user_id) {
        alert("You are not authorized to delete this post!");
        return;
      }

      let res = await axios.delete("http://localhost:3000/blogs/" + id);
      console.log(res);
      if (res.status == 200) {
        alert("Deleted successfully");
        this.loadData();
      }
    },
  },
  async mounted() {
    let users = await axios.get("http://localhost:3000/users");
    let result = await axios.get("http://localhost:3000/blogs");
    result.data.forEach((blog) => {
      let user = users.data.find((user) => user.id === blog.user_id);
      blog.user_name = user.username;
    });

    this.blogs = result.data;
  },
};
</script>
<style scoped>
@import url(https://fonts.googleapis.com/css?family=Dancing+Script);
.data-name {
  font-family: "Dancing Script", cursive;
  font-size: 20px;
  color: steelblue;
}

.card-title {
  color: steelblue;
}
.borderless-button {
  border: none;
  background-color: transparent;
  color: red;
  font-size: 16px;
  cursor: pointer;
}
</style>
