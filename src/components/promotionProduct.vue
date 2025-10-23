<template>
    <div class="flex justify-between items-center rounded-2xl p-6 w-full max-w-3xl mx-auto hover:scale-105 ease-in-out duration-300 cursor-pointer transition">
        <div>
            <h2 class="text-2xl font-semibold text-gray-800 mb-4 leading-tight"><slot></slot></h2>
            <shopButton>Shop Now</shopButton>
        </div>
        <img :src="productImage" alt="Promotion Product" class="w-40 h-40 object-contain"/>
    </div>
</template>

<script lang="ts">
import shopButton from './shopButton.vue';

export default{
    name: "PromotionProduct",
    components: { shopButton },
    props: { productImage: String },
};
</script>
