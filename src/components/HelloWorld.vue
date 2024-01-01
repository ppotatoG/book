<template>
  <v-container>
    <v-data-table
      :options.sync="options"
      :items="desserts"
      v-model="selected"
      :items-per-page="5"
      item-key="name"
      class="elevation-1"
      @update:options="optionsUpdated"
    >
      <template v-slot:header>
        <tr>
          <th>
            <v-checkbox
              v-model="allSelected"
              @change="(value) => toggleSelectAll(value)"
              hide-details
            ></v-checkbox>
          </th>
          <th v-for="header in headers" :key="header.value">
            {{ header.text }}
          </th>
        </tr>
      </template>
      <template v-slot:item="{ item }">
        <tr>
          <td>
            <v-checkbox
              :input-value="selected.includes(item)"
              :disabled="!item.status"
            ></v-checkbox>
          </td>
          <td>{{ item.name }}</td>
          <td>{{ item.calories }}</td>
          <td>{{ item.fat }}</td>
          <td>{{ item.carbs }}</td>
          <td>{{ item.protein }}</td>
          <td>{{ item.status }}</td>
        </tr>
      </template>
    </v-data-table>
  </v-container>
</template>

<script>
export default {
  name: "HelloWorld",
  created() {
    this.desserts.forEach((dessert) => {
      dessert.status = this.inuse.includes(dessert.id);
    });
  },
  data() {
    return {
      selected: [],
      allSelected: false,
      inuse: [2, 4, 6, 8, 10],
      options: {
        page: 1,
        itemsPerPage: 5,
      },
      desserts: this.generateDesserts(20),
      headers: [
        { text: "Select", value: "data-table-select", sortable: false },
        { text: "Dessert (100g serving)", value: "name" },
        { text: "Calories", value: "calories" },
        { text: "Fat (g)", value: "fat" },
        { text: "Carbs (g)", value: "carbs" },
        { text: "Protein (g)", value: "protein" },
        { text: "Status", value: "status" },
      ],
    };
  },
  methods: {
    optionsUpdated() {
      this.selected = [];
      this.allSelected = false;
    },
    toggleSelectAll(value) {
      if (value) {
        const startIndex = (this.options.page - 1) * this.options.itemsPerPage;
        const endIndex = startIndex + this.options.itemsPerPage;
        const currentPageItems = this.desserts.slice(startIndex, endIndex);
        this.selected = currentPageItems.filter((item) => item.status);
      } else {
        this.selected = [];
      }
    },
    generateDesserts(count) {
      const desserts = [];
      for (let i = 1; i <= count; i++) {
        desserts.push({
          id: i,
          name: `Dessert ${i}`,
          calories: Math.floor(Math.random() * 100) + 100,
          fat: Math.random() * 10,
          carbs: Math.random() * 100,
          protein: Math.random() * 10,
          status: true,
        });
      }
      return desserts;
    },
  },
};
</script>
