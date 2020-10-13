<template>
  <div class="container grid">
    <div class="container-left">
      <AppSize/>
      <AppSauces/>
      <AppIngredients/>
    </div>
    <div class="container-right">
      <AppOrder/>
    </div>
  </div>

</template>

<script>
import Size from '@/components/Buiilder/Size'
import Sauces from '@/components/Buiilder/Sauces'
import Ingredients from '@/components/Buiilder/Ingredients'
import Order from '@/components/Order'

export default {
  name: 'Home',
  components: {
    AppSize: Size,
    AppSauces: Sauces,
    AppIngredients: Ingredients,
    AppOrder: Order
  }
}
</script>
