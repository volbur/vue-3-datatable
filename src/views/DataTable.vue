<template>
  <div class="data-table-length">
    <label>
      <select v-model="currentEntries">
        <option v-for="se in showEntries" :key="se" :value="se">
          {{ se }}
        </option>
      </select>
    </label>
  </div>
  <TableBase :columns="columns" :entries="paginateEntries" />
  <div>
    <div>Show {{ from }} to {{ to }} of {{ entries.length }} entries</div>
  </div>
  <div class="pagination">
    <div
      class="page"
      :class="{ page__selected: page === pageNumber }"
      v-for="page in pages"
      :key="page"
      @click="pageClick(page)"
    >
      {{ page }}
    </div>
  </div>
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
      showEntries: [10, 25, 50, 100],
      currentEntries: 10,
      filteredEntries: [],
      pageNumber: 1,
    };
  },
  created() {
    this.getAllEmployees().then((data) => {
      this.entries = data;
    });
  },
  computed: {
    pages() {
      return Math.ceil(this.entries.length / this.currentEntries);
    },
    from() {
      return (this.pageNumber - 1) * this.currentEntries;
    },
    to() {
      return this.from + this.currentEntries;
    },
    paginateEntries() {
      return this.entries.slice(this.from, this.to);
    },
  },
  methods: {
    async getAllEmployees() {
      const response = await fetch("http://localhost:3000/data");
      return response.json();
    },
    pageClick(page) {
      this.pageNumber = page;
      console.log("this.pageNumber: ", this.pageNumber);
      console.log("from: ", this.from);
      console.log("to: ", this.to);
      this.paginateEntries = this.entries.slice(this.from, this.to);
      console.log("paginateEntries: ", this.paginateEntries);
    },
  },
};
</script>

<style lang="scss" scoped>
.pagination {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
}
.page {
  padding: 8px;
  border: solid 1px #e7e7e7;
  cursor: pointer;
  &:hover {
    background-color: #aeaeae;
    color: #fff;
  }
}
.page__selected {
  background-color: #aeaeae;
  color: #fff;
}
// .data-table-length {
// label {
//   font-weight: normal;
//   text-align: left;
//   white-space: nowrap;
//   display: inline-block;
//   margin-bottom: 0.5rem;
// }

// select {
//   width: auto;
//   display: inline-block;
//   height: calc(1.8125rem + 2px);
//   padding-top: 0.25rem;
//   padding-bottom: 0.25rem;
//   padding-left: 0.5rem;
//   font-size: 75%;
//   font-weight: 400;
//   line-height: 1.5;
//   color: #495057;
//   vertical-align: middle;
//   background-color: #fff;
//   border: 1px solid #ced4da;
//   border-radius: 0.25rem;
//   box-shadow: inset 0 1px 2px rgb(0, 0, 0 / 8%);
//   appearance: none;
// }

// option {
//   line-height: 1.5;
//   color: #495057;
// }
// }
</style>

/* FIX:
*-при кліку на кнопку сторінки не змінюється data в 
таблиці(проблема в тому що данні не підгрузились)
(можливо зв'язано з життєвим циклом компонента)
(реалізувати через vuex )
*/