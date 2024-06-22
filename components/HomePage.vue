<template>
  <div>
    <v-img
      src="~/public/images/background-img/fashion-g16fb4f5d6_1280.jpg"
      height="650px"
      cover
      class="mb-5"
    />
    <v-divider color="black" class="mb-2"></v-divider>
    <v-row>
      <v-col col="12" class="d-flex justify-center">
        <span class="text-h4" style="border-bottom: 1px solid">
          Products on Sale
        </span>
      </v-col>
    </v-row>
    <v-row>
      <v-col col="6" md="3">
        <v-card> </v-card>
      </v-col>
    </v-row>
  </div>
</template>

<script lang="ts">
import { defineComponent } from "vue";
import product from "~/public/data/product.json";
import type { iProduct } from "~/types/types";

const HomePage = defineComponent({
  data() {
    return {
      products: product as iProduct[],
    };
  },
  computed: {
    saleProducts(): iProduct[] {
      const saleProducts = this.products.filter(
        (x) =>
          <number>this.convertCurrencyToNumber(x.sale) <
          <number>this.convertCurrencyToNumber(x.price)
      );
      return saleProducts.slice(0, 12);
    },
  },
  mounted() {
    console.log(this.saleProducts);
  },
  methods: {
    convertCurrencyToNumber(value: string): number | undefined {
      if (!value.startsWith("¥")) {
        return undefined;
      }
      const str = value.substring(1).replaceAll(/[.]/g, "");
      if (!/^[0-9]+$/.test(str)) {
        return undefined;
      }
      return parseInt(str);
    },
  },
});
export default HomePage;
export type HomePageType = InstanceType<typeof HomePage>;
</script>
