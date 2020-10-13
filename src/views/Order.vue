<template>
  <div class="container grid grid-50">
    <AppForm/>
    <AppOrder/>
  </div>
</template>

<script>
import Order from "@/components/Order";
import Form from "@/components/Form";

export default {
  name: "Order",
  components: {
    AppOrder: Order,
    AppForm: Form
  }
}
</script>

<style scoped>

</style>