<template>
  <div>
    <detalle-articulo :articulo="entidad"></detalle-articulo>
  </div>
</template>

<script>
import detalleArticulo from "../components/DetalleArticulo.vue";

export default {
  components:{
    detalleArticulo
  },
  data(){
    return{
      entidad: {}
    }
  },
  mounted(){
    this.getEntidad()    
  },
  updated(){
    this.getEntidad()
  },
  methods:{
    async getEntidad() {
      const res = await fetch("/test/tc/articulos.json");
      const resJson = await res.json();             
      this.entidad = await resJson.find(e => e.codigo == this.$route.params.codigo)
      
    }
  }
}
</script>

<style>

</style>