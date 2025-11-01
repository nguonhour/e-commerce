<script setup lang="ts">
import { ref, onMounted } from 'vue';
import axios from 'axios';
import PromotionProduct from '../components/promotionProduct.vue';
import ProductCard from '../components/productCard.vue';

// Define types
interface Product {
    id: number;
    name: string;
    productCount: number;
    color: string;
    image: string;
}

interface Promotion {
    id: number;
    title: string;
    color: string;
    image: string;
    buttonText: string;
    buttonColor: string;
}

interface Category {
    id?: number;
    name: string;
    productCount: number;
    color: string;
    image: string;
}

interface Promotionn {
    id: number;
    title: string;
    color: string;
    image: string;
    buttonText: string;
    buttonColor: string;
}

const products = ref<Product[]>([
    {
        id: 1,
        name: 'Sample Product 1',
        productCount: 29,
        color: "#AD2424",
        image: 'https://png.pngtree.com/png-vector/20210602/ourmid/pngtree-3d-beauty-cosmetics-product-design-png-image_3350323.jpg',
    },
    {
        id: 2,
        name: 'Sample Product 2',
        productCount: 39,
        color: "#AD2424",
        image: 'https://png.pngtree.com/png-vector/20210602/ourmid/pngtree-3d-beauty-cosmetics-product-design-png-image_3350323.jpg',
    },
    {
        id: 3,
        name: 'Sample Product 3',
        productCount: 49,
        color: "#6B24AD",
        image: 'https://png.pngtree.com/png-vector/20210602/ourmid/pngtree-3d-beauty-cosmetics-product-design-png-image_3350323.jpg',
    },
    {
        id: 4,
        name: 'Sample Product 4',
        productCount: 59,
        color: "#24AD37",
        image: 'https://png.pngtree.com/png-vector/20210602/ourmid/pngtree-3d-beauty-cosmetics-product-design-png-image_3350323.jpg',
    },
    {
        id: 5,
        name: 'Sample Product 5',
        productCount: 69,
        color: "#AD2424",
        image: 'https://png.pngtree.com/png-vector/20210602/ourmid/pngtree-3d-beauty-cosmetics-product-design-png-image_3350323.jpg',
    },
    {
        id: 6,
        name: 'Sample Product 6',
        productCount: 79,
        color: "#6B24AD",
        image: 'https://png.pngtree.com/png-vector/20210602/ourmid/pngtree-3d-beauty-cosmetics-product-design-png-image_3350323.jpg',
    },
    {
        id: 7,
        name: 'Sample Product 7',
        productCount: 89,
        color: "#24AD37",
        image: 'https://png.pngtree.com/png-vector/20210602/ourmid/pngtree-3d-beauty-cosmetics-product-design-png-image_3350323.jpg',
    },
    {
        id: 8,
        name: 'Sample Product 8',
        productCount: 99,
        color: "#AD2424",
        image: 'https://png.pngtree.com/png-vector/20210602/ourmid/pngtree-3d-beauty-cosmetics-product-design-png-image_3350323.jpg',
    }
]);

const promotionss = ref<Promotion[]>([
    {
        id: 1,
        title: '🌿 Discover Our New Skincare Line',
        color: "#F0E9D7",
        image: 'https://png.pngtree.com/png-vector/20210602/ourmid/pngtree-3d-beauty-cosmetics-product-design-png-image_3350323.jpg',
        buttonText: 'Shop Now',
        buttonColor: "#C76161",
    },
    {
        id: 2,
        title: '💄 Exclusive Lipstick Collection',
        color: "#F0E9D7",
        image: 'https://png.pngtree.com/png-vector/20210602/ourmid/pngtree-3d-beauty-cosmetics-product-design-png-image_3350323.jpg',
        buttonText: 'Shop Now',
        buttonColor: "#3345D6",
    },
    {
        id: 3,
        title: '✨ Limited Edition Fragrances',
        color: "#F0E9D7",
        image: 'https://png.pngtree.com/png-vector/20210602/ourmid/pngtree-3d-beauty-cosmetics-product-design-png-image_3350323.jpg',
        buttonText: 'Shop Now',
        buttonColor: "#61C7C2",
    },
]);

const categories = ref<Category[]>([]);
const promotionns = ref<Promotionn[]>([]);


const buttonpromotionalert = (promotion: Promotion) => {
    alert("Let's shop: " + promotion.title);
};

const fetchProducts = async () => {
    try {
        const response = await axios.get<Category[]>('http://localhost:3000/api/categories');
        categories.value = response.data;
    } catch (error) {
        console.error('Error fetching products:', error);
    }
};

const fetchPromotions = async () => {
    try {
        const response = await axios.get<Promotionn[]>('http://localhost:3000/api/promotions');
        promotionns.value = response.data;
    } catch (error) {
        console.error('Error fetching promotions:', error);
    }
};

onMounted(() => {
    fetchProducts();
    fetchPromotions();
});
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
                    :productItem="product.productCount"
                    :productItemcolorbackground="product.color"
                    :productImage="product.image"
                />
            </div>
            <div>
                <h3 class="px-4 py-2 transition">
                    <!-- Load More Products -->
                </h3>
                <div class="grid grid-cols-4 gap-6">
                    <ProductCard 
                        v-for="category in categories" 
                        :key="category.id || category.name" 
                        :productName="category.name"
                        :productItem="category.productCount"
                        :productItemcolorbackground="category.color"
                        :productImage="category.image"
                    />
                </div>
            </div>
        </section>
        
        <section class="w-full mx-auto p-6">
            <h2 class="text-2xl font-semibold text-gray-800 mb-6 text-center space-y-3">
                Special Promotions Just For You
            </h2>

            <div class="grid grid-cols-3 gap-6">
                <PromotionProduct 
                    v-for="promotion in promotionss" 
                    :key="promotion.id" 
                    :productTitle="promotion.title"
                    :productImage="promotion.image"
                    :buttonText="promotion.buttonText"
                    :bgpromotionColor="promotion.color"
                    :bgbtn="promotion.buttonColor"
                    @shop-click="buttonpromotionalert(promotion)"
                />
            </div>
            <div class="mt-6">
                <div class="px-4 py-2 transition grid grid-cols-4 gap-6">
                    <PromotionProduct 
                    v-for="promotion in promotionns" 
                    :key="promotion.id || promotion.title" 
                    :productTitle="promotion.title"
                    :productImage="promotion.image"
                    :buttonText="promotion.buttonText"
                    :bgpromotionColor="promotion.color"
                    :bgbtn="promotion.buttonColor"
                    @shop-click="buttonpromotionalert(promotion)"
                />
                </div>
            </div>
        </section>     
    </div>
</template>
