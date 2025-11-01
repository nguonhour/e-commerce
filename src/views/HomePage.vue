<script setup lang="ts">
import { ref } from 'vue';
import PromotionProduct from '../components/promotionProduct.vue';
import ProductCard from '../components/productCard.vue';

const products = ref([
    {
        id: 1,
        name: 'Sample Product 1',
        item: 29,
        bgcolor: "#AD2424",
        image:
            'https://png.pngtree.com/png-vector/20210602/ourmid/pngtree-3d-beauty-cosmetics-product-design-png-image_3350323.jpg',
    },
    {
        id: 2,
        name: 'Sample Product 2',
        item: 39,
        bgcolor: "#AD2424",
        image:
            'https://png.pngtree.com/png-vector/20210602/ourmid/pngtree-3d-beauty-cosmetics-product-design-png-image_3350323.jpg',
    },
    {
        id: 3,
        name: 'Sample Product 3',
        item: 49,
        // itemcolor: "#AD2424",
        bgcolor: "#6B24AD",
        image:
            'https://png.pngtree.com/png-vector/20210602/ourmid/pngtree-3d-beauty-cosmetics-product-design-png-image_3350323.jpg',
    },
    {
        id: 4,
        name: 'Sample Product 4',
        item: 59,
        bgcolor: "#24AD37",
        image:
            'https://png.pngtree.com/png-vector/20210602/ourmid/pngtree-3d-beauty-cosmetics-product-design-png-image_3350323.jpg',
    },
    {
        id: 5,
        name: 'Sample Product 5',
        item: 69,
        bgcolor: "#AD2424",
        image:
            'https://png.pngtree.com/png-vector/20210602/ourmid/pngtree-3d-beauty-cosmetics-product-design-png-image_3350323.jpg',
    },
    {
        id: 6,
        name: 'Sample Product 6',
        item: 79,
        bgcolor: "#6B24AD",
        image:
            'https://png.pngtree.com/png-vector/20210602/ourmid/pngtree-3d-beauty-cosmetics-product-design-png-image_3350323.jpg',
    },
    {
        id: 7,
        name: 'Sample Product 7',
        item: 89,
        bgcolor: "#24AD37",
        image:
            'https://png.pngtree.com/png-vector/20210602/ourmid/pngtree-3d-beauty-cosmetics-product-design-png-image_3350323.jpg',
    },
    {
        id: 8,
        name: 'Sample Product 8',
        item: 99,
        bgcolor: "#AD2424",
        image:
            'https://png.pngtree.com/png-vector/20210602/ourmid/pngtree-3d-beauty-cosmetics-product-design-png-image_3350323.jpg',
    }
]);

const promotions = ref([
    {
        id: 1,
        title: '🌿 Discover Our New Skincare Line',
        color: "#F0E9D7",
        image:
            'https://png.pngtree.com/png-vector/20210602/ourmid/pngtree-3d-beauty-cosmetics-product-design-png-image_3350323.jpg',
        buttonText: 'Shop Now',
        bgcolors: "#C76161",
    },
    {
        id: 2,
        title: '💄 Exclusive Lipstick Collection',
        color: "#F0E9D7",
        image:
            'https://png.pngtree.com/png-vector/20210602/ourmid/pngtree-3d-beauty-cosmetics-product-design-png-image_3350323.jpg',
        buttonText: 'Shop Now',
        bgcolors: "#3345D6",
    },
    {
        id: 3,
        title: '✨ Limited Edition Fragrances',
        color: "#F0E9D7",
        image:
            'https://png.pngtree.com/png-vector/20210602/ourmid/pngtree-3d-beauty-cosmetics-product-design-png-image_3350323.jpg',
        buttonText: 'Shop Now',
        bgcolors: "#61C7C2",
    },
]);

const buttonpromotionalert = (promotion: any) => {
    alert("Let's shop: " + promotion.title);
};

</script>

<template>
    <div class="w-full bg-gray-50 min-h-screen">
        <section class="w-full mx-auto p-6">
            <h1 class="text-3xl font-bold text-gray-800 mb-6 text-center">
                Our Featured Products
            </h1>
            <div class="grid grid-cols-8 gap-6">
                <ProductCard 
                    v-for="product in products" 
                    :key="product.id" 
                    :productName="product.name"
                    :productItem="product.item"
                    :productItemcolorbackground="product.bgcolor"
                    :productImage="product.image"
                />
            </div>
        </section>
        
        <section class="w-full mx-auto p-6">
            <h2 class="text-2xl font-semibold text-gray-800 mb-6 text-center space-y-3">
                Special Promotions Just For You
            </h2>

            <div class="grid grid-cols-3 gap-6 ">
                <PromotionProduct 
                    v-for="promotion in promotions" 
                    :key="promotion.id" 
                    :productTitle="promotion.title"
                    :productImage="promotion.image"
                    :buttonText="promotion.buttonText"
                    :bgpromotionColor="promotion.bgcolors"
                    @click="buttonpromotionalert(promotion)"
                />
            </div>
            
        </section>     
    </div>
</template>
