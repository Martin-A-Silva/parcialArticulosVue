<template>
  <div>
    <b-container fluid>
      <b-row><br /></b-row>
      <b-row>
        <b-col>
          <img :src="articulo.foto" height="300px" />
          <b-row style="text-align: left">
            <br />
            Descripción: <br /><br />{{ articulo.articulo }}
          </b-row>
        </b-col>
        <b-col
          style="
            border-left-style: solid;
            border-left-width: 1px;
            border-left-color: lightgrey;
          "
        >
          <b-col style="text-align: left">
            <b-row>
              <b-col style="color: grey"
                >{{ articulo.cantidadVendida }} vendidos</b-col
              >
            </b-row>
            <b-row>
              <b-col
                ><h2>{{ articulo.instrumento }}</h2></b-col
              >
            </b-row>
            <b-row>
              <b-col
                ><h1 style="fontfamily: Franklin Gothic Book">
                  ${{ articulo.precio }}
                </h1></b-col
              >
            </b-row>
            <b-row>
              <b-col
                ><h6><br />Marca: {{ articulo.marca }}</h6></b-col
              >
            </b-row>
            <b-row>
              <b-col
                ><h6>Modelo: {{ articulo.modelo }}</h6></b-col
              >
            </b-row>
            <b-row>
              <b-col
                ><br />Costo Envio: <br />
                <span style="color: #00cc00" v-if="articulo.costoEnvio == 'G'"
                  ><img src="/images/camion.png" alt="costo" />Envío
                  Gratis</span
                >
                <span style="color: orange" v-if="articulo.costoEnvio != 'G'"
                  >${{ articulo.costoEnvio }}</span
                >
              </b-col>
            </b-row>
            <b-row>
              <p style="margin-left: 20px">
                <br />
                <br />
                <br />
                <b-button variant="outline-primary"
                  >Agregar al carrito</b-button
                >
              </p>
            </b-row>
          </b-col>
        </b-col>
      </b-row>
    </b-container>
  </div>
</template>

<script>
export default {
  name: "DetalleArticulo",
  props: ["articulo"],
  mounted() {},
  data() {
    return {
      productoEncontrado: [],
    };
  },
  methods: {},
};
</script>

<style>
</style>