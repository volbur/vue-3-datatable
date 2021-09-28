<template>
  <div class="container">
    <DataTable />
  </div>
</template>

<script>
import DataTable from "./views/DataTable.vue";

export default {
  name: "App",
  components: {
    DataTable,
  },
};
</script>

<style lang="scss">
@import url("https://pro.fontawesome.com/releases/v5.10.0/css/all.css");
@import url("https://cdn.jsdelivr.net/npm/bootstrap@5.1.1/dist/css/bootstrap.min.css");
</style>
