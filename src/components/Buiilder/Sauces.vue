<template>
  <div class="panel">
    <div class="panel-heading">
      <h3 class="panel-title"><span class="panel-title__number">2.</span>Выберите соус</h3>
    </div>
    <div class="panel-body">
      <div class="pizza-sauce">
        <label v-for="sauce in sauces" :key="sauce.id" class="pizza-sauce-checkbox-label" @change="setSelectedSauces(sauce.id, sauce.checked)">
          <input type="checkbox" class="pizza-sauce-checkbox" name="size" v-model="sauce.checked">
          <div class="pizza-sauce-info">
            <img class="pizza-sauce__image" :src="sauce.image" alt="">
            <span class="pizza-sauce__name">{{ sauce.name }}</span>
            <span class="pizza-sauce__description">{{ sauce.description }}</span>
            <span class="pizza-sauce__price">{{ sauce.price }} руб.</span>
          </div>
        </label>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Sauce",
  computed: {
    sauces() {
      return this.$store.state.sauces
    }
  },
  methods: {
    setSelectedSauces(id, checked) {
      this.$store.commit('setCheckedSauce', {id, checked})
    }
  }
}
</script>

<style scoped>
.pizza-sauce {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  column-gap: 30px;
  row-gap: 50px;
}

.pizza-sauce-checkbox-label {
  text-align: center;
}

.pizza-sauce__image {
  display: block;
  margin: auto;
}

.pizza-sauce__name {
  display: block;
  color: #fdbc2c;
  font-size: 30px;
  font-weight: bold;
  margin-top: 20px;
  margin-bottom: 15px;
}

.pizza-sauce__description {
  display: block;
  margin-bottom: 15px;
  color: #fff;
  font-size: 13px;
}

.pizza-sauce__price {
  display: block;
  font-family: Caveat, Roboto, Arial, sans-serif;
  color: #D94F2B;
  font-size: 24px;
}

.pizza-sauce-checkbox {
  display: none;
}

.pizza-sauce-info {
  cursor: pointer;
  position: relative;
}

.pizza-sauce-info:before {
  content: '';
  background: url('../../assets/images/checkbox.png');
  background-size: cover;
  width: 32px;
  height: 32px;
  left: 50%;
  top: -16px;
  position: absolute;
  transform: translateX(-50%);
  display: none;
}

.pizza-sauce-checkbox:checked + .pizza-sauce-info:before {
  display: block;
}

@media screen and (max-width: 767px) {
  .pizza-sauce {
    grid-template-columns: 1fr;
  }
}
</style>