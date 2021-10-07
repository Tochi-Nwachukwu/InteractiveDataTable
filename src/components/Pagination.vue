<template>
  <div class="pagination-strip">
    <p>Showing 1 to {{ totalPages }} of {{ totalPages }} entries</p>
    <div class="util-flex">
      <p @click="pageFunction">Previous</p>

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
  name: "Pagination",
  props: {
    totalPages: Number,
    pageFunction: { type: Function },
    currentPage: String,
  },
};
</script>

<style scoped>
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

.active {
  background-color: #027bff;
  color: white;
}
.inactive {
  color: #027bff;
  background-color: white;
}
</style>