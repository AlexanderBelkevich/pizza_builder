<template>
  <div class="panel">
    <div class="panel-heading">
      <h3 class="panel-title"><span class="panel-title__number">1.</span>Выберите размер пиццы</h3>
    </div>
    <div class="panel-body">
      <div class="pizza-size">
        <label class="pizza-size-radio-label" v-for="size in sizes" :key="size.value" @change="setSize(size)">
          <input type="radio" class="pizza-size-radio" name="size" v-model="selectedSize" :value="size.name">
          <span class="pizza-size-radio-round round-9" :class="`round-${size.size}`">{{size.size}}''</span>
          <span class="pizza-size-radio-name">{{size.name}}</span>
        </label>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Size',
  data() {
    return {
      selectedSize: '',
      sizes: [
        {
          size: 9,
          name: 'Маленькая',
          price: 100
        },
        {
          size: 12,
          name: 'Средняя',
          price: 150
        },
        {
          size: 14,
          name: 'Большая',
          price: 200
        },
        {
          size: 16,
          name: 'Экстра',
          price: 300
        },
        {
          size: 18,
          name: 'Вечеринка',
          price: 350
        },
      ]
    }
  },
  methods: {
    setSize(size) {
      this.$store.commit('setSelectedSize', size)
    }
  }
}
</script>

<style scoped>
.pizza-size {
  display: flex;
  align-items: flex-end;
}

.pizza-size-radio-label {
  margin-right: 15px;
  cursor: pointer;
}

.pizza-size-radio-round {
  position: relative;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 24px;
  font-weight: 700;
  border: 2px solid #fff;
  border-radius: 50%;
  transition: all 0.1s;
  color: #fff;
}

.pizza-size-radio {
  display: none;
}

.pizza-size-radio:checked + .pizza-size-radio-round {
  border-color: #D94F2B;
  background: #d94f2b;
}

.pizza-size-radio-round.round-9 {
  height: 67px;
  width: 67px;
}

.pizza-size-radio-round.round-12 {
  height: 78px;
  width: 78px;
}

.pizza-size-radio-round.round-14 {
  height: 95px;
  width: 95px;
}

.pizza-size-radio-round.round-16 {
  height: 104px;
  width: 104px;
}

.pizza-size-radio-round.round-18 {
  height: 113px;
  width: 113px;
}

.pizza-size-radio-name {
  color: #fff;
  display: block;
  margin-top: 23px;
  text-align: center;
  font-weight: bold;
}

@media screen and (max-width: 767px) {
  .pizza-size {
    flex-wrap: wrap;
  }
  .pizza-size-radio-label {
    width: 50%;
    margin-right: 0;
    text-align: center;
    margin-bottom: 20px;
  }
  .pizza-size-radio-round {
    margin: auto;
  }
}
</style>