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
              <h6 class="data-name">posted by:{{ name }}</h6>
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
      perPage: 3,
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
  },
  async mounted() {
    this.getUserName();
    let result = await axios.get("http://localhost:3000/blogs");
    this.blogs = result.data;
  },
};
</script>
<style scoped>
@import url(https://fonts.googleapis.com/css?family=Dancing+Script);
.data-name {
  font-family: "Dancing Script", cursive;
  font-size: 20px;
}

.card-title {
  color: steelblue;
}
</style>
