<script setup lang="ts">
import ProductCards from '../components/productCard.vue';
import PromotionProduct from '../components/promotionProduct.vue';
</script>
<template>
    <div class="w-full bg-gray-50 min-h-screen">
        <!-- 🛍️ Product Grid Section -->
        <section class="w-full mx-auto p-6">
            <h1 class="text-3xl font-bold text-gray-800 mb-6 text-center">
                Our Featured Products
            </h1>
            <!-- <div
            class="grid grid-cols-1 sm:grid-cols-2 md:grid-cols-3 lg:grid-cols-4 xl:grid-cols-5 gap-6"
        >
            <ProductCards
            v-for="i in 10"
            :key="i"
            class="bg-white border border-gray-200 rounded-2xl hover:shadow-lg transition hover:-translate-y-1"
            productImage="https://png.pngtree.com/png-vector/20210602/ourmid/pngtree-3d-beauty-cosmetics-product-design-png-image_3350323.jpg"
            productName="Sample Product"
            :productItem="29.99"
            />
        </div> -->
        </section>
        <div class="w-full p-6 grid grid-cols-10 gap-4"> 
            <!-- grid-cols-1 sm:grid-cols-2 md:grid-cols-4 lg:grid-cols-6 xl:grid-cols-10 -->
            <ProductCards
                class="bg-green-200"
                productImage="https://png.pngtree.com/png-vector/20210602/ourmid/pngtree-3d-beauty-cosmetics-product-design-png-image_3350323.jpg"
                productName="Sample product"
                :productItem="29.99"
            />
            <ProductCards
                class="bg-red-200"
                productImage="https://png.pngtree.com/png-vector/20210602/ourmid/pngtree-3d-beauty-cosmetics-product-design-png-image_3350323.jpg"
                productName="Sample product"
                :productItem="29.99"
            />
            <ProductCards
                class="bg-yellow-200"
                productImage="https://png.pngtree.com/png-vector/20210602/ourmid/pngtree-3d-beauty-cosmetics-product-design-png-image_3350323.jpg"
                productName="Sample product"
                :productItem="29.99"
            />
            <ProductCards
                class="bg-blue-200"
                productImage="https://png.pngtree.com/png-vector/20210602/ourmid/pngtree-3d-beauty-cosmetics-product-design-png-image_3350323.jpg"
                productName="Sample product"
                :productItem="29.99"
            />
            <ProductCards
                class="bg-pink-200"
                productImage="https://png.pngtree.com/png-vector/20210602/ourmid/pngtree-3d-beauty-cosmetics-product-design-png-image_3350323.jpg"
                productName="Sample product"
                :productItem="29.99"
            />
            <ProductCards
                class="bg-gray-200"
                productImage="https://png.pngtree.com/png-vector/20210602/ourmid/pngtree-3d-beauty-cosmetics-product-design-png-image_3350323.jpg"
                productName="Sample product"
                :productItem="29.99"
            />
            <ProductCards
                class="bg-indigo-200"
                productImage="https://png.pngtree.com/png-vector/20210602/ourmid/pngtree-3d-beauty-cosmetics-product-design-png-image_3350323.jpg"
                productName="Sample product"
                :productItem="29.99"
            />
            <ProductCards
                class="bg-rose-200"
                productImage="https://png.pngtree.com/png-vector/20210602/ourmid/pngtree-3d-beauty-cosmetics-product-design-png-image_3350323.jpg"
                productName="Sample product"
                :productItem="29.99"
            />
            <ProductCards
                class="bg-stone-200"
                productImage="https://png.pngtree.com/png-vector/20210602/ourmid/pngtree-3d-beauty-cosmetics-product-design-png-image_3350323.jpg"
                productName="Sample product"
                :productItem="29.99"
            />
            <ProductCards
                class="bg-teal-200"
                productImage="https://png.pngtree.com/png-vector/20210602/ourmid/pngtree-3d-beauty-cosmetics-product-design-png-image_3350323.jpg"
                productName="Sample product"
                :productItem="29.99"
            />
        </div>
        <section class="w-full mx-auto p-6">
            <h2 class="text-2xl font-semibold text-gray-800 mb-6 text-center space-y-3">
                Special Promotions Just For You
            </h2>
            <!-- <PromotionProduct
            class="bg-green-200"
            productImage="https://png.pngtree.com/png-vector/20210602/ourmid/pngtree-3d-beauty-cosmetics-product-design-png-image_3350323.jpg"
            /> -->
            <div class="grid grid-cols-3 gap-6 ">
                <PromotionProduct
                    class="bg-green-200"
                    productImage="https://png.pngtree.com/png-vector/20210602/ourmid/pngtree-3d-beauty-cosmetics-product-design-png-image_3350323.jpg"
                    >
                    🌿 Discover Our New Skincare Line
                </PromotionProduct>
                <PromotionProduct
                    class="bg-pink-200"
                    productImage="https://png.pngtree.com/png-vector/20210602/ourmid/pngtree-3d-beauty-cosmetics-product-design-png-image_3350323.jpg"
                    >
                    💄 Exclusive Lipstick Collection
                </PromotionProduct>
                <PromotionProduct
                    class="bg-indigo-200"
                    productImage="https://png.pngtree.com/png-vector/20210602/ourmid/pngtree-3d-beauty-cosmetics-product-design-png-image_3350323.jpg"
                    >
                    ✨ Limited Edition Fragrances
                </PromotionProduct>
            </div>
            
        </section>     
    </div>
</template>