<template>
  <!-- This is the layout for the pagination component -->
  <div class="pagination-strip">
    <p>Showing 1 to {{ totalPages }} of {{ totalPages }} entries</p>
    <div class="util-flex">
      <p @click="pageFunction">Previous</p>

      <!-- The two page numbers have classes conditionally applied -->
      <div
        @click="pageFunction"
        id="page-number"
        class="util-margin"
        :class="currentPage === '1' ? 'active' : 'inactive'"
      >
        1
      </div>
      <div
        @click="pageFunction"
        id="page-number"
        class="util-margin"
        :class="currentPage === '2' ? 'active' : 'inactive'"
      >
        2
      </div>

      <p @click="pageFunction">Next</p>
    </div>
  </div>
</template>

<script>
export default {
  // The components are exported here and the props are received here
  name: "Pagination",
  props: {
    totalPages: Number,
    pageFunction: { type: Function },
    currentPage: String,
  },
};
</script>

<style scoped>

/* Styles for the pagination component go in here */
.pagination-strip {
  display: flex;
  align-items: center;
  justify-content: space-between;
  margin-top: 8px;
}

.util-flex {
  display: flex;
  align-items: center;
  cursor: pointer;
}

.util-margin {
  margin: 0px 8px;
}

#page-number {
  padding: 4px 8px;
  cursor: pointer;
}

/* styles for the active and inactive components are applied here */
.active {
  background-color: #027bff;
  color: white;
}
.inactive {
  color: #027bff;
  background-color: white;
}
</style>