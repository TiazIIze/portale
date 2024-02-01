<template>
  <div class="navbar-container">
    <v-card>
      <v-layout>
        <v-navigation-drawer
          class="navbar"
          style="background-color: rgb(59, 131, 59)"
          v-model="drawer"
          :rail="rail"
          permanent
          @click="rail = false"
        >
          <v-list-item style="color: white">
            <template v-slot:append>
              <v-btn
                variant="text"
                icon="mdi-chevron-left"
                @click.stop="rail = !rail"
              ></v-btn>
            </template>
          </v-list-item>

          <v-divider></v-divider>

          <v-list density="compact" nav>
            <v-list-item
              to="/"
              style="color: white"
              prepend-icon="mdi-home-city"
              title="Home"
              value="home"
            ></v-list-item>
            <v-list-item
              to="/utenti"
              style="color: white"
              prepend-icon="mdi-account-group-outline"
              title="Users"
              value="users"
            ></v-list-item>
            <v-list-item
              to="/prodotti"
              style="color: white"
              prepend-icon="mdi-widgets"
              title="Products"
              value="products"
            ></v-list-item>
          </v-list>
        </v-navigation-drawer>
      </v-layout>
    </v-card>
  </div>
  <RouterView></RouterView>
</template>

<script>
export default {
  data() {
    return {
      drawer: true,
      rail: true,
    };
  },
};
</script>
<style>
body {
  padding: 10px;
}
.navbar-container {
  position: fixed;
  z-index: 1;
}
</style>
