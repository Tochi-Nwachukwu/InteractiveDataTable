<template>
  <!-- Rendering the search input field -->
  <div class="input">
    <p>Search</p>
    <input
      id="text-input"
      type="text"
      v-model="search"
      v-on:keyup="getAllData"
    />
  </div>

  <!-- Rendering the table header component -->
  <Header />

  <!-- Rendering the table data -->
  <div
    class="data"
    :class="index % 2 === 0 ? 'shaded-row' : 'light-row'"
    :key="item.name"
    v-for="(item, index) in books.entries()"
  >
    <div class="util-border">{{ item[1].name }}</div>
    <div class="util-border">{{ item[1].isbn }}</div>
    <div class="util-border">
      {{ item[1].authors.join(", ") }}
    </div>
    <div class="util-border">{{ item[1].numberOfPages }}</div>
    <div class="util-border">{{ item[1].country }}</div>
    <div class="util-border">{{ item[1].released.split("T")[0] }}</div>
  </div>

  <!-- Rendering the header component -->
  <Header />

  <!-- Rendering the pagination component -->
  <Pagination
    :totalPages="books.length"
    :pageFunction="getPageNumber"
    :currentPage="currentPage"
    :lastPage="lastPageNumber"
  />
</template>

<script>
import Header from "./components/Header";
import Pagination from "./components/Pagination";
import axios from "axios";

export default {
  name: "App",
  mounted() {
    this.getAllData();
  },

  components: {
    Header,
    Pagination,
  },

  data() {
    return {
      books: [],
      search: "",
      currentPage: "1",
      PaginationData: { lastUrl: "" },
      lastPageNumber: 2,
    };
  },

  methods: {
    // Method to fetch all data from the API
    getAllData(url) {
      url = `https://www.anapioficeandfire.com/api/books/?name=${this.search}&page=${this.currentPage}&pageSize=10`;
      axios.get(url).then((res) => {
        this.books = res.data;
        this.PaginationData.lastUrl = res.headers.link.split(",")[2];

        this.extractPageNumber(this.PaginationData.lastUrl);
      });
    },
    // Method to retrieve page numbers from pagination component
    getPageNumber(input) {
      if (input == "Prev" && Number(this.currentPage > 1)) {
        this.currentPage = (Number(this.currentPage) - 1).toString();
      } else if (input == "Next" && Number(this.currentPage < 2)) {
        this.currentPage = (Number(this.currentPage) + 1).toString();
      } else this.currentPage = input;

      this.getAllData();
    },

    extractPageNumber(str) {
      const splitStr = str.split("page=")[1].split("&")[0];
      this.lastPageNumber = Number(splitStr);
      console.log(this.lastPageNumber);
    },
  },
  // Method to implement the search functionality
};
</script>

<style>
#app {
  font-family: "Open Sans", sans-serif;
  box-sizing: border-box;
  margin: 0;
  padding: 0;

  margin: 0px 42px;
}

/* Styles for the data table */
.data {
  font-weight: 400;
  font-size: 16px;
  display: grid;
  grid-template-columns: repeat(6, 1fr);
  justify-content: center;
}

.util-border {
  border: 1px solid #e5e8eb;
  padding: 12px;
  line-height: 1.5;
}

.shaded-row {
  background-color: #f2f2f2;
}

.light-row {
  background-color: #ffffff;
}

/* Styles for the search input field */
.input {
  display: flex;
  justify-content: end;
  align-items: center;
  margin: 16px 0px;
}

p {
  margin-right: 8px;
}

#text-input {
  padding: 8px 4px;
  border: 1px solid #dfdddd;
  border-radius: 4px;
}

#text-input:focus {
  outline: none;
}
</style>
