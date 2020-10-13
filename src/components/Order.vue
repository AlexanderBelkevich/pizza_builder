<template>
  <div class="order" v-if="total > 0">
    <span class="order__title">Ваш заказ</span>
    <div class="order-table-title" v-if="sauces.length || ingredients.length">
      <span>Ингридиент</span>
      <span>Стоимость</span>
    </div>
    <div class="order-table">
      <div class="order-table-row" v-for="sauce in sauces" :key="sauce.id">
        <div class="order-table-row-left">
          <span class="order-table__name">{{sauce.name}}</span>
        </div>
        <div class="order-table-row-right">
          <span class="order-table__price">{{ sauce.price }} руб.</span>
          <button class="order-table__remove" @click="uncheckSauce(sauce.id)">
            <img src="../assets/images/remove.png" alt="">
          </button>
        </div>
      </div>
      <div class="order-table-row" v-for="ingredient in ingredients" :key="ingredient.id">
        <div class="order-table-row-left">
          <div class="order-table-buttons">
            <button class="order-table__button" @click="incrementIngredient(ingredient.id)"><img src="../assets/images/minus.png"></button>
            <button class="order-table__button" @click="addIngredient(ingredient.id)"><img src="../assets/images/plus.png"></button>
          </div>
          <span class="order-table__name">{{ ingredient.name }} x {{ingredient.count}}</span>
        </div>
        <div class="order-table-row-right">
          <span class="order-table__price">{{ ingredient.price * ingredient.count }} руб.</span>
          <button class="order-table__remove" @click="removeIngredient(ingredient.id)"><img src="../assets/images/remove.png" alt=""></button>
        </div>
      </div>
      <div class="order-table-row" v-if="size.name">
        <div class="order-table-row-left">
          <span class="order-table__name size">Размер пиццы: {{size.size}}'' ({{ size.name }})</span>
        </div>
        <div class="order-table-row-right">
          <span class="order-table__price">{{size.price}} руб.</span>
        </div>
      </div>
      <div class="order-table-row">
        <span class="order-table-total">Общая сумма заказа: {{ total }} руб.</span>
      </div>
    </div>
    <router-link
        v-if="size.name && (sauces.length || ingredients.length)"
        to="/order"
        class="order-now"
        :style="{display: $route.path === '/order' ? 'none' : 'flex'}">Оформить заказ</router-link>
  </div>
</template>

<script>
export default {
  name: "Order",
  computed: {
    size() {
      return this.$store.state.selectedSize;
    },
    sauces() {
      return this.$store.getters['getSelectedSauces'];
    },
    ingredients() {
      return this.$store.getters['getSelectedIngredients'];
    },
    total() {
      const totalSauces = this.sauces.length ? this.sauces.reduce((total, acc) => total + acc.price, 0) : 0;
      const totalIngredients = this.ingredients.length ? this.ingredients.reduce((total, acc) => total + (acc.price * acc.count), 0) : 0;
      const size = this.size.price ? this.size.price : 0;
      return size + totalSauces + totalIngredients
    }
  },
  methods: {
    uncheckSauce(id) {
      this.$store.commit('uncheckedSauce', id)
    },
    incrementIngredient(id) {
      this.$store.commit('incrementIngredient', id)
    },
    addIngredient(id) {
      this.$store.commit('addIngredient', id)
    },
    removeIngredient(id) {
      this.$store.commit('removeIngredient', id)
    }
  }
}
</script>

<style scoped>
.order {
  padding: 20px 30px 25px 35px;
  background-color: rgba(0, 0, 0, 0.3);
}

.order__title {
  display: block;
  margin-bottom: 20px;
  color: #fdbc2c;
  font-size: 24px;
  font-weight: bold;
}

.order-table {
  margin-top: 20px;
}

.order-table-title {
  display: grid;
  grid-template-columns: 3fr 2fr;
  text-transform: uppercase;
  padding: 20px 0;
  color: #fff;
  font-size: 14px;
  font-weight: bold;
  border-bottom: 1px solid #fff;
}

.order-table-title span:last-child {
  text-align: right;
}

.order-table-row {
  display: grid;
  grid-template-columns: 3fr 2fr;
  padding: 3px 0;
}

.order-table-buttons {
  margin-right: 10px;
  min-width: 35px;
  max-width: 35px;
  display: flex;
  justify-content: space-between;
}

.order-table-total {
  margin-top: 20px;
  font-size: 16px;
  color: #fff;
  padding-top: 20px;
  border-top: 1px solid #fff;
}

.order-table__button {
  border: none;
  background: none;
  padding: 0;
  cursor: pointer;
}

.order-table__button img {
  width: 15px;
  height: 15px;
}

.order-table-row-left {
  display: flex;
  align-items: center;
}

.order-table__name {
  font-size: 11px;
  color: #fff;
}

.order-table__name.size {
  font-size: 15px;
}

.order-table__price {
  color: #fff;
  font-size: 18px;
  font-family: Caveat, Roboto, Arial, sans-serif;
}

.order-table-row-right {
  display: flex;
  align-items: center;
  justify-content: flex-end;
}

.order-table__remove {
  cursor: pointer;
  background: none;
  padding: 0;
  border: none;
  margin-left: 10px;
}

.order-now {
  margin-top: 40px;
  height: 40px;
  display: flex;
  align-items: center;
  justify-content: center;
  border-radius: 3px;
  background: #fdbc2c;
  text-transform: uppercase;
  color: #000;
  cursor: pointer;
  transition: all 0.3s;
  text-decoration: none;
  font-weight: bold;
}

.order-now:hover {
  opacity: .8;
}
</style>