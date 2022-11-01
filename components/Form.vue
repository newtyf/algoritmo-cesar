<template>
  <v-form ref="form" v-model="valid" lazy-validation>
    <v-container>
      <v-row class="align-center mr-2">
        <v-col cols="6" md="5">
          <v-text-field
            v-model="cadena.value"
            :rules="cadena.rules"
            :label="cadena.label"
            required
          ></v-text-field>
        </v-col>

        <v-col cols="6" md="5">
          <v-text-field
            v-model="separador.value"
            :rules="separador.rules"
            :label="separador.label"
            type="number"
            required
          ></v-text-field>
        </v-col>

        <v-col
          cols="12"
          md="2"
          :class="$vuetify.breakpoint.xs ? 'd-flex justify-center' : ''"
        >
          <v-btn :disabled="!valid" color="success" @click="validate">
            Calcular
          </v-btn>
        </v-col>
      </v-row>
      <v-row v-if="resultCesar.length > 0">
        <v-card-title>
          Encriptado:<span style="color: #dd223d; padding-left: 5px">{{ resultCesar }}</span>
        </v-card-title>
      </v-row>
    </v-container>
  </v-form>
</template>

<script>
export default {
  data() {
    return {
      valid: true,
      cadena: {
        value: "",
        label: "Cadena de numeros y letras",
        rules: [(v) => !!v || "cadena es necesario"],
      },
      separador: {
        value: 1,
        label: "Separador",
        rules: [
          (v) => !!v || "separador es necesario",
          (v) => parseInt(v) >= 0 || "Debe ser mayor o igual cero",
        ],
      },
      resultCesar: "",
    };
  },
  methods: {
    validate() {
      if (this.$refs.form.validate()) {
        this.calculate(
          this.cadena.value.toLowerCase(),
          parseInt(this.separador.value)
        );
      }
    },
    calculate(cadena, separador) {
      const abcedarioEs = [
        "a",
        "b",
        "c",
        "d",
        "e",
        "f",
        "g",
        "h",
        "i",
        "j",
        "k",
        "l",
        "m",
        "n",
        "ñ",
        "o",
        "p",
        "q",
        "r",
        "s",
        "t",
        "u",
        "v",
        "w",
        "x",
        "y",
        "z",
      ];

      let CesarString = "";
      for (let i = 0; i < cadena.length; i++) {
        const element = cadena[i];
        console.log(typeof element);
        if (parseInt(element)) {
          CesarString += element
        } else {
          let positionWithSeparator =
          (abcedarioEs.indexOf(element) + separador) % abcedarioEs.length;
        CesarString += abcedarioEs[positionWithSeparator];
        }
      }
      this.resultCesar = CesarString;
      console.log(CesarString);
    },
  },
};
</script>

<style>
.nuxt-logo {
  height: 180px;
}
</style>
