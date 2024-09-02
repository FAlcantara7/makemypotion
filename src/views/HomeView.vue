<template>
  <BanneR/>
  <div class="main_container">
    <h1>Monte sua Potion</h1>
    <PotionForm/>
  </div>
</template>

<script>
import BanneR from '../components/Banner.vue'
import PotionForm from '../components/PotionForm.vue';

export default {
  name: 'HomeView',
  components: {
    BanneR,
    PotionForm
  }
}
</script>


