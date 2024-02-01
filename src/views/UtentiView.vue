<template>
  <div class="utenti">
    <v-card class="mx-auto" max-width="344">
      <v-img
        src="https://cdn.vuetifyjs.com/images/cards/sunshine.jpg"
        height="200px"
        cover
      ></v-img>

      <v-card-title> Top western road trips </v-card-title>

      <v-card-subtitle> 1,000 miles of wonder </v-card-subtitle>

      <v-card-actions>
        <v-btn color="orange-lighten-2" variant="text"> Explore </v-btn>

        <v-spacer></v-spacer>

        <v-btn
          :icon="show ? 'mdi-chevron-up' : 'mdi-chevron-down'"
          @click="show = !show"
        ></v-btn>
      </v-card-actions>

      <v-expand-transition>
        <div v-show="show">
          <v-divider></v-divider>

          <v-card-text> hi i am oleg </v-card-text>
        </div>
      </v-expand-transition>
    </v-card>
  </div>

  <RouterView></RouterView>
</template>

<script>
export default {
  name: "UtentiView",
  data() {
    return {
      utenti: [],
      show: false,
    };
  },
  methods: {},
  mounted() {

  },
};
</script>

<style>
.utenti {
  position: relative;
  margin-left: 100px;
  padding: 10px;
}
</style>

