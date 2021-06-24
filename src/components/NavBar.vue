<template>
  <div>
    <b-navbar toggleable="lg" type="dark" variant="dark">
      <b-navbar-brand href="/">NavBar</b-navbar-brand>

      <b-navbar-toggle target="nav-collapse"></b-navbar-toggle>

      <b-collapse id="nav-collapse" is-nav>
        <b-navbar-nav>
          <b-nav-form v-on:submit.prevent="onSubmit('codigo', codigo)">
            <b-nav-text class="mx-2">Código:</b-nav-text>
            <b-form-input
              class="mx-2"
              v-model="codigo"
              placeholder="Search"
            ></b-form-input>
            <b-button
              variant="success"
              class="my-2 my-sm-0"
              type="submit"
              v-bind:to="`/?codigo=${codigo}`"
              >Search</b-button
            >
          </b-nav-form>
          <b-nav-form
            v-on:submit.prevent="onSubmit('denominacion', denominacion)"
          >
            <b-nav-text class="mx-2">Denominación:</b-nav-text>
            <b-form-input
              class="mr-sm-2"
              v-model="denominacion"
              placeholder="Search"
            ></b-form-input>
            <b-button
              variant="success"
              class="my-2 my-sm-0"
              type="submit"
              v-bind:to="`/?denominacion=${denominacion}`"
              >Search</b-button
            >
          </b-nav-form>
          <b-nav-item v-bind:to="`/detalle/${this.codBarato}`">MAS BARATO</b-nav-item>
        </b-navbar-nav>

        <!-- Right aligned nav items -->
      </b-collapse>
    </b-navbar>
  </div>
</template>
<script>
//import Grilla from "./GrillaArticulos.vue";
export default {  
  data() {
    return {
      codigo: "",
      denominacion: "",
      codBarato: 0,
    };
  },
  mounted(){
    this.getEntidades()
  },
  methods: {
    onSubmit(que, param) {
      this.$router.push(`/?${que}=${param}`);
    },
    async getEntidades() {
      const res = await fetch("test/tc/articulos.json");
      this.entidades = await res.json(); 
      let precios = [];
      let promedio = 0;
      this.entidades.forEach(entidad=>{
        entidad.preciosRelevados.forEach(precio =>{          
          promedio += precio
        })
        promedio= promedio/entidad.preciosRelevados.length
        precios.push(promedio);        
        
      })      
      let idxBarato = precios.indexOf(Math.min(...precios));
      this.codBarato = this.entidades[idxBarato].codigo      
    },
    calcularPromedio(id){
          let promedio=0;
          this.$props.entidades[id].preciosRelevados.forEach((element) =>{
              promedio += element;
          })
          promedio= promedio/this.$props.entidades[id].preciosRelevados.length;
          return promedio
      }
  },
};
</script>

<style lang="">
</style>