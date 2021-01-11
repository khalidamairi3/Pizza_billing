<template>
  <div id="textOrder">
    <h1>
      Please Enter your order in the following format (Size - Topping, Topping,
      Topping,...)
    </h1>
    <v-textarea
      style="width : 40vw"
      v-model="orderText"
      outlined
      name="input-7-4"
      label="Outlined textarea"
    ></v-textarea>
    <v-btn color="primary" @click="validateInput(orderText)">
      Validate
    </v-btn>
    <p v-if="!valid">the input is not valid, please follow the format</p>
    <modal height="auto" name="bill" id="billModal">
      <div id="items">
        <h3>Pizza bill</h3>
        <h4>Items</h4>
        <div class="item" v-for="order in orders" :key="order.orderText">
          <p>
            {{
              order.quantity +
                " " +
                order.orderText +
                ": $" +
                (order.quantity * order.price).toFixed(2)
            }}
          </p>
          <br />
        </div>
        <p>{{ "Subtotal: $" + calculateTotal() }}</p>
        <p>{{ "GST: $" + (total * 0.05).toFixed(2) }}</p>
        <p>{{ "Total: $" + (total * 1.05).toFixed(2) }}</p>
      </div>
    </modal>
  </div>
</template>

<script>
export default {
  name: "text-order",

  data() {
    return {
      orderText: "",
      valid: true,
      total: 0,
      orders: [],
      prices: {
        Small: {
          Cheese: 0.5,
          Pepperoni: 0.5,
          Ham: 0.5,
          Pineapple: 0.5,
          Sausage: 2.0,
          FetaCheese: 2.0,
          Tomatoes: 2.0,
          Olives: 2.0,
          price: 12.0,
        },
        Medium: {
          Cheese: 0.75,
          Pepperoni: 0.75,
          Ham: 0.75,
          Pineapple: 0.75,
          Sausage: 3.0,
          FetaCheese: 3.0,
          Tomatoes: 3.0,
          Olives: 3.0,
          price: 14.0,
        },
        Large: {
          Cheese: 1.0,
          Pepperoni: 1.0,
          Ham: 1.0,
          Pineapple: 1.0,
          Sausage: 4.0,
          FetaCheese: 4.0,
          Tomatoes: 4.0,
          Olives: 4.0,
          price: 16.0,
        },
      },
    };
  },

  methods: {
    //   this function is used to validate every item in the order text as follows
    //   clear the orders array to start a new bill
    //   spliting lines so each item can be processed individually
    //   spliting each line into size and toppings
    //   spliting toppings to chech every topping
    //   gitting rid of all possible spaces that migh the user enter
    //   check if item data is valid to be added to the order array
    //   check if all data is valid to show the bill

    validateInput(orderText) {
      this.orders = [];
      let prices = this.prices;
      orderText = orderText.trim();
      let items = orderText.split("\n");
      let valid = true;
      for (let i = 0; i < items.length; i++) {
        let itemDetails = items[i].split("-");
        let itemSize = itemDetails[0].trim();
        let itemToppings = [];
        if (itemDetails.length > 1) {
          itemToppings = itemDetails[1].trim().split(",");
          itemToppings = itemToppings.filter(function(topping) {
            return topping != "";
          });
        }
        if (prices[itemSize] == undefined) {
          valid = false;
          break;
        }
        itemToppings.forEach((topping) => {
          topping = topping.trim();
          if (topping.startsWith("Feta")) {
            topping = topping.split(" ").join("");
          }

          if (prices[itemSize][topping] == undefined && topping != "") {
            valid = false;
          }
        });

        if (valid) {
          this.addToOrders(itemSize, itemToppings);
        } else {
          break;
        }
      }

      this.valid = valid;
      if (valid) {
        this.$modal.show("bill");
      }
    },
    // this is to create an order object that has the order text, quantity and price
    addToOrders(itemSize, itemToppings) {
      let digits = [
        "Zero",
        "One",
        "Two",
        "Three",
        "Four",
        "Five",
        "Six",
        "Seven",
        "Eight",
      ];
      let itemPrice = 0;
      let quantity = 1;
      let orderText =
        itemSize + ", " + digits[itemToppings.length] + " Topping Pizza - ";
      itemPrice += this.prices[itemSize]["price"];
      for (let i = 0; i < itemToppings.length; i++) {
        let topping = itemToppings[i].trim();
        if (topping.startsWith("Feta")) {
          topping = topping.split(" ").join("");
        }
        itemPrice += this.prices[itemSize][topping];
        if (i == itemToppings.length - 1 && itemToppings.length != 1) {
          orderText += " and " + topping;
        } else if (i == 0) {
          orderText += topping;
        } else {
          orderText += ", " + topping;
        }
      }

      let order = {
        orderText: orderText,
        price: itemPrice,
        quantity: quantity,
      };
      let index = this.orderExist(order);
      if (index == -1) {
        this.orders.push(order);
      } else {
        this.orders[index].quantity += 1;
      }
    },
    orderExist(order) {
      for (let i = 0; i < this.orders.length; i++) {
        if (this.orders[i].orderText == order.orderText) {
          return i;
        }
      }
      return -1;
    },
    // to calculate the total before adding GST
    calculateTotal() {
      let total = 0;
      this.orders.forEach((order) => {
        total += order.quantity * order.price;
      });
      this.total = total.toFixed(2);
      return this.total;
    },
  },
};
</script>

<style lang="scss" scoped>
#textOrder {
  display: grid;
  align-items: center;
  justify-items: center;
  height: 100%;
}
#items {
  display: grid;
  align-items: center;
  justify-items: center;
  padding: 10%;
}
</style>
