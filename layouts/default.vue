<template>
  <v-app>
    <v-app-bar app hide-on-scroll>
      <span class="w-100 mx-auto">{{title}}</span>
    </v-app-bar>
    <v-main><v-container> <Nuxt/> </v-container></v-main>
  </v-app>
</template>

<script>
export default {
  name: "DefaultLayout",
  data() {
    return {
      title: "Algoritmo Cesar"
    };
  },
};
</script>
