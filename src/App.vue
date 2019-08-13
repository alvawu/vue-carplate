<template>
  <div id="app">
      <!-- <div style="height: 998px">1</div> -->
      <!-- Text : <input type="text" /><br/> -->
      Car Plate : <car-plate v-model="carPlate"></car-plate>
  </div>
</template>

<script>
import CarPlate from './components/CarPlate/CarPlate'
export default {
  name: 'app',
  data () {
    return {
      carPlate: ''
    }
  },
  components: {
      CarPlate
  }
}
</script>

<style>
</style>
