<template></template>

<script lang="ts">
import { defineComponent } from "vue";

const ProductCard = defineComponent({
  name: "ProductCard",
  data() {
    return {};
  },
});
export default ProductCard;
export type ProductCardType = InstanceType<typeof ProductCard>;
</script>
