<template>
  <div>
    <v-simple-table>
      <template v-slot:default>
        <thead>
          <tr>
            <th class="text-left">
              Topping
            </th>
            <th class="text-left">
              Small
            </th>
            <th class="text-left">
              Medium
            </th>
            <th class="text-left">
              Large
            </th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="item in toppings" :key="item.name">
            <td>{{ item.name }}</td>
            <td>{{ item.small }}</td>
            <td>{{ item.medium }}</td>
            <td>{{ item.large }}</td>
          </tr>
        </tbody>
      </template>
    </v-simple-table>
  </div>
</template>

<script>
export default {
  name: "toppings",
  data() {
    return {
      toppings: [
        {
          name: "Cheese",
          small: "$0.50",
          medium: "$0.75",
          large: "$1.00",
        },
        {
          name: "Pepperoni",
          small: "$0.50",
          medium: "$0.75",
          large: "$1.00",
        },
        {
          name: "Ham",
          small: "$0.50",
          medium: "$0.75",
          large: "$1.00",
        },
        {
          name: "Pineapple",
          small: "$0.50",
          medium: "$0.75",
          large: "$1.00",
        },
        {
          name: "Sausage",
          small: "$2.00",
          medium: "$3.00",
          large: "$4.00",
        },
        {
          name: "Feta Cheese",
          small: "$2.00",
          medium: "$3.00",
          large: "$4.00",
        },
        {
          name: "Tomatoes",
          small: "$2.00",
          medium: "$3.00",
          large: "$4.00",
        },
        {
          name: "Olives",
          small: "$2.00",
          medium: "$3.00",
          large: "$4.00",
        },
      ],
    };
  },
};
</script>

<style lang="scss" scoped></style>
