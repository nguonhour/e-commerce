<template>
    <div class="w-40 h-48 rounded-2xl shadow-md flex flex-col items-center justify-center hover:scale-105 transition cursor-pointer">
        <img :src="productImage" alt="product" class="w-20 h-20 object-contain mb-2" />
        <h2 class="text-gray-800 font-semibold text-md">{{ productName }}</h2>
        <p class="text-gray-500 text-sm"> {{ productItem }} </p>
    </div>
</template>

<script lang="ts">

export default {
  name: "productCard",
  props: {
    productImage: String,
    productName: String,
    productItem: Number,
  },
  
};
</script>

