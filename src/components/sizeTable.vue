<template>
  <div>
    <v-simple-table>
      <template v-slot:default>
        <thead>
          <tr>
            <th class="text-left">
              Size
            </th>
            <th class="text-left">
              Price
            </th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="category in categories" :key="category.name">
            <td>{{ category.size }}</td>
            <td>{{ category.price }}</td>
          </tr>
        </tbody>
      </template>
    </v-simple-table>
  </div>
</template>

<script>
export default {
  name: "size-table",
  data() {
    return {
      categories: [
        {
          size: "Small",
          price: "$12",
        },
        {
          size: "Medium",
          price: "$14",
        },
        {
          size: "Large",
          price: "$16",
        },
      ],
    };
  },
};
</script>

<style lang="scss" scoped></style>
