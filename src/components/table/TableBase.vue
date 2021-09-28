<template>
  <table class="table">
    <thead>
      <tr>
        <th v-for="th in tableHeader" :key="th">
          <div class="d-flex justify-content-between align-items-center">
            <span v-if="!th.icon">{{ th.text }}</span>
            <i
              v-else
              class="fa"
              :class="th.icon"
              data-toggle="tooltip"
              :data-original-title="th.text"
            >
            </i>
            <i v-if="th.sort" class="fas fa-arrows-alt-v"></i>
          </div>
        </th>
      </tr>
    </thead>
    <tbody>
      <tr v-for="td in tableData" :key="td">
        <td>{{ td.created_at }}</td>
        <td>{{ td.name }}</td>
        <td>{{ td.currency.code }}</td>
        <td>{{ td.name }}</td>
        <td>{{ td.casinos_count }}</td>
        <td>{{ td.players_count }}</td>
        <td>{{ td.comment }}</td>
      </tr>
    </tbody>
  </table>
</template>

<script>
export default {
  name: "TableData",
  props: {
    columns: Array,
    entries: Array,
  },
  computed: {
    tableHeader() {
      return this.columns || [];
    },
    tableData() {
      return this.entries || [];
    },
  },
};
</script>