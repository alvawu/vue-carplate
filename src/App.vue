<template>
  <div id="app">
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
