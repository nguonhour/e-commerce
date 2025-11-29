<script setup lang="ts">
import { RouterView } from 'vue-router'
import FooterPages from './layout/footerPages.vue'
import HeaderPages from './layout/headerPages.vue'
import NavCategory from './layout/NavCategory.vue'
import { onMounted } from 'vue'
import { initFlowbite } from 'flowbite'

// initialize components based on data attribute selectors
onMounted(() => {
  initFlowbite()
})
</script>

<template>
  <div>
    <HeaderPages />
    <NavCategory />
    <br>


    <main class="flex justify-center items-center">
      <RouterView />
    </main>
    <br>
    <FooterPages />
  </div>
</template>
