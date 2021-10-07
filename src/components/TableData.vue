<template>
  <div :v-for="item in books">
    <h3>{{ item }}</h3>
  </div>
</template>

<script>
export default {
  name: "TableData",
  props: {
    books: Array,
  },

  methods: {
   
  },
};
</script>

<style>
</style>