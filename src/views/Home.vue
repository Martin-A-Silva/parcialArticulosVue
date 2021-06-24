<template>
  <div class="home">   

    <Grilla :entidades="this.entidades" ></Grilla>
  </div>
</template>
<script>
// @ is an alias to /src
import Grilla from '../components/GrillaArticulos.vue'

export default {
  name: 'Home',
  components: {
    Grilla
  },
  data(){
    return{
      entidades: []
    }
  },
  mounted(){
    this.getEntidades()
  },
  updated(){
    this.getEntidades()
  },
  methods:{
    async getEntidades() {
      const res = await fetch("test/tc/articulos.json");
      this.entidades = await res.json(); 
      if(this.$route.query.codigo){
        this.entidades = this.entidades.filter( entidad => entidad.codigo == this.$route.query.codigo)
      }
      else if(this.$route.query.denominacion){
        this.entidades = this.entidades.filter( entidad => entidad.articulo.toLowerCase().includes(this.$route.query.denominacion.toLowerCase()))
      }
    }
  }
}
</script>