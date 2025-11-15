<script setup lang="ts">
import { ref, onMounted } from 'vue';
import { computed } from 'vue';

import axios from 'axios';
import PromotionProduct from '../components/promotionProduct.vue';
import ProductCard from '../components/productCard.vue';

import { defineStore } from 'pinia';
// import { mapState } from 'pinia';
// import { storeToRefs } from 'pinia';
// import { group } from 'console';



interface Category {
    id?: number;
    name: string;
    url: string;
    productCount: number;
    color: string;
    image: string;
    group: string;
}

interface Promotion {
    id: number;
    title: string;
    color: string;
    image: string;
    url: string;
    buttonText: string;
    buttonColor: string;
}


const categories = ref<Category[]>([]);
const promotions = ref<Promotion[]>([]);


const buttonpromotionalert = (promotion: Promotion | Promotion) => {
    alert("Let's shop: " + promotion.title);
};

const API_BASE_URL = 'http://localhost:3000';
const getImageUrl = (imagePath: string | undefined) => {

    if (!imagePath) {
        return 'https://via.placeholder.com/300x200?text=No+Image';
    }

    if (imagePath && imagePath.startsWith('http')) {
        return imagePath;
    }
    return `${API_BASE_URL}${imagePath.startsWith('/') ? '' : '/'}${imagePath}`;

};

const fetchProducts = async () => {
    try {
        const response = await axios.get<Category[]>('http://localhost:3000/api/categories');
        console.log('Categories API Response:', response.data);
        categories.value = response.data;
    } catch (error) {
        console.error('Error fetching products:', error);
    }
};

const fetchPromotions = async () => {
    try {
        const response = await axios.get<Promotion[]>('http://localhost:3000/api/promotions');
        console.log('Promotions API Response:', response.data);
        promotions.value = response.data;
    } catch (error) {
        console.error('Error fetching promotions:', error);
    }
};

const userProductsStore = defineStore('products', {
    state: () => ({
        groups: [],
        promotions: [],
        categories: [],
        products: [],
    }),
    getters: {
       
        getCategoriesByGroup: (state) => {
           return (groupName) => state.categories.find((category) => category.group === groupName);
        },
        getProductsByGroup: (state) => {
            return (groupName) => state.products.filter((product) => product.group === groupName);
        },
        // getProductsByCategory: (categoryId) => {
        //     return (state) => state.products.filter((product) => product.categoryId === categoryId);
        // },
        getProductsByCategory: (state) => {
            return (categoryId) => {
                // Add a check to ensure products exists and is an array
                // if (!state.products || !Array.isArray(state.products)) {
                //     return [];
                // }
                return state.products.filter((product) => product.categoryId === categoryId);
            };
        },
        getPopularProducts: (state) => {
            return state.products.filter((product) => product.isPopular);
        },
    },
    actions: {
        async fetchAllData() {
            try {
                const [groupsResponse, promotionsResponse, categoriesResponse, productsResponse] = await Promise.all([
                    axios.get('http://localhost:3000/api/groups'),
                    axios.get('http://localhost:3000/api/promotions'),
                    axios.get('http://localhost:3000/api/categories'),
                    axios.get('http://localhost:3000/api/products'),
                ]);

                this.groups = groupsResponse.data;
                this.promotions = promotionsResponse.data;
                this.categories = categoriesResponse.data;
                this.products = productsResponse.data;

                console.log('Store data loaded:', {
                    groups: this.groups.length,
                    promotions: this.promotions.length,
                    categories: this.categories.length,
                    products: this.products.length,
                });
            } catch (error) {
                console.error('Error fetching data:', error);
            }
        },
    },
});

const userProductsStoreInstance = userProductsStore();
const currentGroupName = ref('Group A');

const popularProducts = computed(() => userProductsStoreInstance.getPopularProducts);
const categorys = computed(() => userProductsStoreInstance.getCategoriesByGroup(currentGroupName.value));
const productsByGroup = computed(() => userProductsStoreInstance.getProductsByGroup(currentGroupName.value));
const productsByCategory = (categoryId: number) => { return userProductsStoreInstance.getProductsByCategory(categoryId);};

const storeCategories = computed(() => userProductsStoreInstance.categories);
const storePromotions = computed(() => userProductsStoreInstance.promotions);

onMounted(() => {
    userProductsStoreInstance.fetchAllData();
    fetchProducts();
    fetchPromotions();

    console.log('Categories:', storeCategories.value);
    console.log('Promotions:', storePromotions.value);
    console.log('Popular Products:', popularProducts.value);
    console.log('Products By Group:', productsByGroup.value);
    console.log('Products By Category (ID=1):', productsByCategory(1));
});

</script>


<template>
    <div class="w-full bg-gray-50 min-h-screen">
        <section class="w-full mx-auto p-6">
            <h1 class="text-3xl font-bold text-gray-800 mb-6 text-center">
                Our Featured Products
            </h1>
            <div>
                <div class="grid grid-cols-1 sm:grid-cols-2 md:grid-cols-3 lg:grid-cols-4 xl:grid-cols-5 gap-6 p-6">
                    <ProductCard 
                        v-for="category in categories" 
                        :key="category.id || category.name" 
                        :productName="category.name"
                        :productItem="category.productCount"
                        :productItemcolorbackground="category.color"
                        :productImage="getImageUrl(category.image)"
                    />
                </div>
            </div>
        </section>
        
        <section class="w-full mx-auto p-6">
            <h1 class="text-2xl pb-8 font-semibold text-gray-800 mb-6 text-center space-y-3">
                Special Promotions Just For You
            </h1>

            <div class="mt-6 flex justify-center items-center">
                <div class="px-4 py-2 transition grid grid-cols-1 sm:grid-cols-2 md:grid-cols-3 lg:grid-cols-4 xl:grid-cols-5 gap-6">
                    <PromotionProduct 
                    v-for="promotion in promotions" 
                    :key="promotion.id || promotion.title" 
                    :productTitle="promotion.title"
                    :productImage="getImageUrl(promotion.image)"
                    :buttonText="promotion.buttonText"
                    :bgpromotionColor="promotion.color"
                    :bgbtn="promotion.buttonColor"
                    @shop-click="() => buttonpromotionalert(promotion)"
                />
                </div>
            </div>
        </section>     
    </div>
</template>
