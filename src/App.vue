<template>
  <div class="container">
    <h1>Carrito</h1>
    <!-- {{productos}} -->
    <!-- <pre>{{carrito}}</pre> -->
    <hr>
    <Carrito />
    <div class="row">
      <Card 
        v-for="producto of productos" :key="producto.id" :producto="producto"
      />  
    </div>
    
  </div>

</template>

<script>
import {useStore} from 'vuex'
import { computed, onMounted } from 'vue'
import Card from './components/Card'
import Carrito from './components/Carrito'

  export default {
    name: 'App',
    components: {
      Card,
      Carrito
    },
    setup(){
      //Esto es para importar la tienda donde esta el fetchdata
      const store = useStore()
      onMounted(() => {
        store.dispatch('fetchData')
      })
      // Se usa para mapear las propiedades computadas que se encuentran en setup y 
      // poderlas mostrar en la app
      const productos = computed(() => store.state.productos)
      const carrito = computed(() => store.state.carrito)

      return {productos, carrito}
    }
  }
</script>