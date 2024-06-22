<template>
  <v-app-bar dark color="black" density="compact">
    <template v-slot:prepend>
      <v-app-bar-nav-icon
        class="d-block d-md-none"
        variant="text"
        @click.stop="drawer = !drawer"
      />
    </template>
    <v-app-bar-title>
      <v-btn
        :ripple="false"
        text="Tien's Shop"
        variant="text"
        exact
        to="/"
        flat
      />
      <div class="d-none d-md-inline-flex">
        <v-btn
          v-for="item in drawerItems"
          :key="item.title"
          variant="text"
          :text="item.title"
          :prepend-icon="item.icon"
          exact
          :to="item.value"
        />
      </div>
    </v-app-bar-title>
    <v-spacer></v-spacer>
    <v-btn icon="mdi-cart-outline" exact to="/cart" flat />
    <v-btn icon="mdi-account-circle-outline" />
  </v-app-bar>
  <v-navigation-drawer v-model="showDrawer" temporary>
    <v-list nav>
      <v-list-item
        v-for="item in drawerItems"
        :key="item.title"
        :prepend-icon="item.icon"
        :title="item.title"
        exact
        :to="item.value"
      />
    </v-list>
  </v-navigation-drawer>
  <v-main>
    <v-container>
      <NuxtPage />
    </v-container>
  </v-main>
</template>

<script lang="ts">
import { defineComponent } from "vue";
import type { drawerMenu } from "~/types/types";

const DefaultLayout = defineComponent({
  data() {
    return {
      drawer: false,
      drawerItems: [
        {
          title: "Products",
          icon: "mdi-tshirt-crew-outline",
          value: "/products",
        },
        {
          title: "About",
          icon: "mdi-information-outline",
          value: "/about",
        },
        {
          title: "Stores",
          icon: "mdi-store-outline",
          value: "/stores",
        },
      ] as drawerMenu[],
    };
  },
  computed: {
    showDrawer: {
      get(): boolean {
        return this.drawer && this.$vuetify.display.mobile;
      },
      set(value: boolean) {
        this.drawer = value;
      },
    },
  },
});
export default DefaultLayout;
</script>

<style scoped>
*:deep(.v-toolbar__content > .v-toolbar-title) {
  width: fit-content;
}
</style>
