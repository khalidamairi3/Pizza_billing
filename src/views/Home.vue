<template>
  <div class="home">
    <h1>Welcome to Pizza Billing System</h1>
    <div id="pageMenu">
      <sizeTable />
      <toppingsTable />
    </div>
    <orderText />
  </div>
</template>

<script>
// @ is an alias to /src
import orderText from "../components/textOrder";
import sizeTable from "../components/sizeTable";
import toppingsTable from "../components/toppings";

export default {
  name: "Home",
  components: {
    orderText,
    sizeTable,
    toppingsTable,
  },
};
</script>
<style lang="scss">
.home {
  height: 100%;
  display: grid;
  justify-items: center;
  align-items: center;
}

#pageMenu {
  padding: 3%;
  width: 90%;
  display: grid;
  grid-template-columns: 1fr 3fr;
  column-gap: 2vw;
  align-items: center;
}
</style>
