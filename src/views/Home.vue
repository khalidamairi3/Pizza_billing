<template>
  <div class="home">
    <orderText />
  </div>
</template>

<script>
// @ is an alias to /src
import orderText from "../components/textOrder";

export default {
  name: "Home",
  components: {
    orderText
  }
};
</script>
<style lang="scss">
.home{
  height: 100%;
}
</style>
