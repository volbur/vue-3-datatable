<template>
  <TableBase :columns="columns" :entries="entries" />
</template>

<script>
import TableBase from "../components/table/TableBase.vue";
export default {
  name: "DataTable",
  components: {
    TableBase,
  },
  data() {
    return {
      columns: [
        { name: "created", text: "Created" },
        { name: "name", text: "Name", sort: true },
        {
          name: "currency",
          text: "Currency",
          sort: true,
          icon: "fa-money-bill",
        },
        { name: "provider", text: "Provider", sort: true },
        {
          name: "casino",
          text: "icon-casino",
          sort: true,
          icon: "fa-copyright",
        },
        {
          name: "player",
          text: "icon-player",
          sort: true,
          icon: "fa-user-circle",
        },
        { name: "comment", text: "Comment", sort: true, icon: "fa-comment" },
      ],
      entries: [],
    };
  },
  created() {
    this.getAllEmployees().then((data) => {
      this.entries = data;
    });
  },
  methods: {
    async getAllEmployees() {
      const response = await fetch("http://localhost:3000/data");
      return response.json();
    },
  },
};
</script>

