<template>
  <div>
    <b-card>
      <b-table ref="table" striped hover :items="entidades" :fields="fields">
        <template #cell(promedioPrecio)="data">
          {{ calcularPromedio(data.index) }}
        </template>
        <template #cell(Detalle)="data">
          <b-button @click="verDetalle(data.item.codigo)" variant="primary"
            >Ver Detalle</b-button
          >
        </template>
      </b-table>
    </b-card>
  </div>
</template>

<script>
export default {
  props: ["entidades"],
  data() {
    return {
      fields: [
        "articulo",
        "codigo",
        "fechaVencimiento",
        "promedioPrecio",
        "Detalle",
      ],
    };
  },
  methods: {
    verDetalle(codigo) {
      this.$router.push(`/detalle/${codigo}`);
    },
    calcularPromedio(id) {
      let promedio = 0;
      this.$props.entidades[id].preciosRelevados.forEach((element) => {
        promedio += element;
      });
      promedio = promedio / this.$props.entidades[id].preciosRelevados.length;
      return promedio;
    },
  },
};
</script>

<style>
</style>