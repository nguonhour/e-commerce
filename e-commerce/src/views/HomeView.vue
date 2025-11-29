<script setup lang="ts">
import { onMounted } from 'vue'
import PromotionProduct from '../components/promotionProduct.vue'
import ProductCard from '../components/productCard.vue'
import { handleCategoryChange, useListMenu } from '../stores/listMenu'
import MenuBAR from '../components/MenuBar.vue'
import ProductSale from '../components/ProductSale.vue'
const { categories, promotions, products, fetchAllData } = useListMenu()

const buttonpromotionalert = (promotion: (typeof promotions.value)[number]) => {
  alert("Let's shop: " + promotion.title)
}

const API_BASE_URL = 'http://localhost:3000'
// const getImageUrl = (imagePath: string | undefined) => {
//   if (!imagePath) {
//     return 'https://via.placeholder.com/300x200?text=No+Image'
//   }

//   if (imagePath && imagePath.startsWith('http')) {
//     return imagePath
//   }
//   return `${API_BASE_URL}${imagePath.startsWith('/') ? '' : '/'}${imagePath}`
// }
const getImageUrl = (imagePath: string | undefined) => {
  if (!imagePath) {
    return 'https://via.placeholder.com/300x200?text=No+Image'
  }

  let cleanPath = imagePath
  if (typeof imagePath === 'string' && imagePath.startsWith('[')) {
    cleanPath = JSON.parse(imagePath)[0]
  }

  if (cleanPath.startsWith('http')) {
    return cleanPath
  }

  return `${API_BASE_URL}${cleanPath.startsWith('/') ? '' : '/'}${cleanPath}`
}
onMounted(async () => {
  await fetchAllData()
  console.log('Categories:', categories.value)
  console.log('Promotions:', promotions.value)
  console.log('Products:', products.value)
  console.log('Data fetching completed.')
})
</script>

<template>
  <div class="w-full min-h-screen pt-8 pb-8 pr-12 pl-12 rounded-2xl">
    <section class="relative bg-amber-200 py-20 rounded-2xl overflow-hidden">
      <div class="container mx-auto px-4 relative z-10">
        <div class="grid grid-cols-1 lg:grid-cols-2 gap-12 items-center">
          <!-- Left Side - Content -->
          <div class="text-gray-700 pl-12">
            <h1 class="text-6xl lg:text-5xl font-bold mb-4 leading-tight">
              Don't miss amazing<br />
              <span>grocery deals</span>
            </h1>
            <p class="relative text-lg text-gray-500 mb-8">Sign up for the daily newsletter</p>
            <div class="absolute max-w-md pt-6 w-full">
              <div class="relative">
                <!-- SVG Icon -->
                <div class="absolute left-3 top-1/2 -translate-y-1/2">
                  <svg
                    width="20"
                    height="20"
                    viewBox="0 0 16 16"
                    fill="none"
                    xmlns="http://www.w3.org/2000/svg"
                  >
                    <path
                      d="M0.967142 4.43255C0.743886 4.49635 0.541155 4.61732 0.379009 4.78352C0.216864 4.94972 0.100924 5.15537 0.0426622 5.38014C-0.0155996 5.6049 -0.0141642 5.84098 0.0468265 6.06502C0.107817 6.28906 0.226249 6.49329 0.390404 6.6575L2.66535 8.92978V13.321H7.06124L9.35152 15.608C9.47436 15.7321 9.62057 15.8306 9.7817 15.8979C9.94283 15.9652 10.1157 15.9999 10.2903 16C10.4051 15.9998 10.5193 15.985 10.6304 15.956C10.855 15.8994 11.0608 15.7846 11.227 15.6232C11.3932 15.4618 11.514 15.2595 11.5771 15.0365L16.0004 0L0.967142 4.43255ZM1.33786 5.71471L12.6913 2.36763L4.00019 11.0447V8.37771L1.33786 5.71471ZM10.299 14.6652L7.61397 11.9875H4.94697L13.6367 3.30508L10.299 14.6652Z"
                      fill="#7E7E7E"
                    />
                  </svg>
                </div>
                <input
                  type="email"
                  placeholder="Your email address"
                  class="w-full px-10 py-3 rounded-lg border-0 focus:outline-none focus:ring-2 focus:ring-[#FFB300] text-gray-900 placeholder-gray-500 pr-28"
                />

                <button
                  class="absolute top-1/2 -translate-y-1/2 right-1 px-5 py-2 bg-green-500 text-white font-bold rounded-md hover:bg-[#FFC233] transition-colors duration-200 shadow"
                >
                  Subscribe
                </button>
              </div>
            </div>
          </div>

          <!-- Right Side - Images -->
          <div class="relative">
            <div class="relative">
              <img
                src="/images/bg2.jpg"
                alt="Fresh Grocery Basket"
                class="w-full h-96 object-cover rounded-3xl shadow-2xl"
              />

              <!-- <div
                class="absolute -top-4 -right-4 bg-red-500 text-white px-6 py-3 rounded-full shadow-xl transform rotate-6"
              >
                <div class="text-center">
                  <div class="text-2xl font-bold">50% OFF</div>
                  <div class="text-xs">First Order</div>
                </div>
              </div> -->
            </div>
          </div>
        </div>
      </div>
      <div class="absolute inset-0 flex items-center justify-center pointer-events-none">
        <img src="/images/bg.png" alt="Category Background" class="max-w-[100%] object-contain" />
      </div>
    </section>

    <section class="w-full mx-auto p-6">
      <div class="pt-6 mb-4">
        <MenuBAR
          NameMenu="Featured Categories"
          :items="[
            'All',
            'Milks & Dairies',
            'Coffes & Teas',
            'Pet Foods',
            'Meats',
            'Vegetables',
            'Fruits',
          ]"
          activeItem="text-green-600"
          @item-selected="handleCategoryChange"
        />
      </div>
      <div>
        <div class="w-full flex justify-center items-center gap-4 pt-6">
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
      <div class="mt-6 flex justify-center items-center w-full">
        <div class="px-4 py-2 transition flex items-center justify-between gap-6">
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

    <section class="w-full mx-auto p-6">
      <div class="mx-auto pt-6 mb-4">
        <MenuBAR
          NameMenu="Popular Products"
          :items="[
            'All',
            'Milks & Dairies',
            'Coffes & Teas',
            'Pet Foods',
            'Meats',
            'Vegetables',
            'Fruits',
          ]"
          activeItem="text-green-600"
          @item-selected="handleCategoryChange"
        />
        <div class="pt-6 grid grid-cols-5 gap-4">
          <ProductSale
            v-for="product in products"
            :key="product.id || product.name"
            :poduectsaleImage="getImageUrl(product.image)"
            :promotionNumber="product.rating"
            :decriptionfood="product.name"
            :rating="product.rating"
            :weightProduct="product.size"
            :price="product.price"
            :originalPrice="product.promotionAsPercentage"
            :bgpromotion="product.bgpromotionColor"
          />
        </div>
      </div>
    </section>
  </div>
</template>
