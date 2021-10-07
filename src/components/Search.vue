<template>
  <div class="input">
    <p>Search</p>
    <input id="text-input" type="text" />
  </div>
</template>

<script>
export default {
  name: "Search",
};
</script>

<style scoped>
* {
  margin: 0;
  padding: 0;
}

.input {
  display: flex;
  justify-content: end;
  align-items: center;
}

p {
  margin-right: 8px;
}

#text-input {
  padding: 8px 4px;
}
</style>