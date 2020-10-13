<template>
  <header class="header">
    <div class="container">
      <router-link to="/" class="title-page">Pizza Builder</router-link>
    </div>
  </header>
</template>

<style scoped>
.header {
  padding-top: 104px;
  padding-bottom: 96px;
  background: url(../assets/images/bg-title.jpg) no-repeat 50% 0;
  background-size: cover;
  box-shadow: 0 1px 7px 0 rgba(1, 2, 2, 0.6);
  text-align: center;
  margin-bottom: 50px;
}

.title-page {
  margin-bottom: 17px;
  font-family: Caveat, Roboto, Arial, sans-serif;
  font-size: 72px;
  color: #fff;
  text-decoration: none;
}

@media screen and (max-width: 767px) {
  .header {
    padding-top: 20px;
    padding-bottom: 20px;
  }
  .title-page {
    font-size: 20px;
  }
}
</style>