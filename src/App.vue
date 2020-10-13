<template>
  <AppHeader/>

  <router-view/>
</template>

<script>
import Header from '@/components/Header.vue'
export default {
  components: {
    AppHeader: Header
  },
}
</script>