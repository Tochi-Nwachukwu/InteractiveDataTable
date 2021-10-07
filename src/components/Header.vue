<template>
  <div class="header">
    <h1 class="util-border">Name</h1>
    <h1 class="util-border">ISBN</h1>
    <h1 class="util-border">Authors</h1>
    <h1 class="util-border">Pages</h1>
    <h1 class="util-border">Country</h1>
    <h1 class="util-border">Released</h1>
  </div>
</template>

<script>
export default {
  name: "Header",
};
</script>

<style scoped>
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

.header {
  display: grid;
  grid-template-columns: repeat(6, 1fr);
  justify-content: center;
}

.header h1 {
  font-weight: 600;
  font-size: 16px;
  padding: 16px;
}
.util-border {
  border: 1px solid #e5e8eb;
}
</style>