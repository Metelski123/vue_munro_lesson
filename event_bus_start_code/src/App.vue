<template>
  <div>
    <h1>Munros</h1>
    <div class="main-container">
      <munros-list :munros='munros'></munros-list>
      <munro-detail :munro='selectedMunro'></munro-detail>
    </div>
  </div>
</template>

<script>
import MunrosList from './components/MunrosList.vue';
import MunroDetail from '.components/MunroDetails.vue';
import {eventBus} from './main.js'
import MunroDetail from '../../event_bus_end/src/components/MunroDetail.vue';

export default {
  name: 'app',
  data(){
    return {
      munros: [],
      selectedMunro: null
    };
  },
  mounted(){
    fetch('https://munroapi.herokuapp.com/munros')
    .then(res => res.json())
    .then(munros => this.munros = munros)

    eventBus.$on('munro-selected', (munro) => {
      console.log('within $on:', munro)
    })
  },
  components: {
    "munros-list": MunrosList,
    "munro-detail": MunroDetail,
    MunroDetail
  }
}
</script>

<style>
  .main-container {
    display: flex;
    justify-content: space-between;
  }
</style>
