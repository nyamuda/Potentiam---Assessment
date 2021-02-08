<template>
  <div id="app">
    <input type="number" v-model="limit" />
    <!-- Passing in a prop to the child component  -->
    <app-numbers :limit="limit"></app-numbers>
  </div>
</template>

<script>
import Numbers from "@/components/Numbers";

export default {
  name: "App",
  components: {
    "app-numbers": Numbers,
  },
  data() {
    return {
      limit: 100,
    };
  },
};
</script>

<style scoped></style>
