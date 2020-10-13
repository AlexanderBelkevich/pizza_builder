<template>
  <form class="send-form" @submit.prevent="sendEmail">
    <input v-model="name" type="text" class="send-form__input" placeholder="Ваше имя">
    <input v-model="phone" type="phone" class="send-form__input" placeholder="Ваш телефон">
    <input v-model="email" type="email" class="send-form__input" placeholder="Ваш email">
    <button class="order-now">Оформить заказ</button>
  </form>
</template>

<script>
import emailjs from 'emailjs-com';

export default {
  name: "Form",
  data() {
    return {
      name: '',
      phone: '',
      email: ''
    }
  },
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
  },
  methods: {
    sendEmail() {
      const params = {
        name: this.name,
        phone: this.phone,
        email: this.email,
        size: this.size.name,
        sauces: this.sauces.map(el => `${el.name}`),
        ingredients: this.ingredients.map(el => `${el.name} x ${el.count}`)
      }
      emailjs.send('service_57vej2j', 'template_s960cud', params, 'user_zIvrxTwh6OTGH2Q5MQbW7')
        .then(response => this.$router.replace('/'))
        .catch(error => console.log(error.response))
    }
  }
}
</script>

<style scoped>
.send-form {
  padding: 20px 30px 25px 35px;
  background-color: rgba(0, 0, 0, 0.3);
}

.send-form__input {
  display: block;
  height: 40px;
  border-radius: 3px;
  width: 100%;
  border: none;
  margin-bottom: 6px;
  padding: 0 10px;
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
</style>