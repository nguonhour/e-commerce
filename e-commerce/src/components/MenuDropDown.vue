<template>
  <div class="relative">
    <button
      :id="`mega-menu-${Menu.toLowerCase().replace(/\s+/g, '-')}-button`"
      @click="toggleDropdown"
      class="flex items-center justify-between w-full py-2 px-3 font-medium text-heading border-b border-light md:w-auto hover:bg-neutral-secondary-soft md:hover:bg-transparent md:border-0 md:hover:text-fg-brand md:p-0"
    >
      {{ Menu }}
      <svg
        class="w-4 h-4 ms-1.5 transition-transform duration-200"
        :class="{ 'rotate-180': isDropdownOpen }"
        aria-hidden="true"
        xmlns="http://www.w3.org/2000/svg"
        width="24"
        height="24"
        fill="none"
        viewBox="0 0 24 24"
      >
        <path
          stroke="currentColor"
          stroke-linecap="round"
          stroke-linejoin="round"
          stroke-width="2"
          d="m19 9-7 7-7-7"
        />
      </svg>
    </button>

    <div
      v-if="isDropdownOpen"
      :id="`mega-menu-${Menu.toLowerCase().replace(/\s+/g, '-')}-dropdown`"
      class="absolute top-full left-0 z-10 grid w-20 grid-cols-2 text-sm bg-gray-200 rounded-xl shadow md:grid-cols-3"
    >
      <div class="p-4 pb-0 text-heading md:pb-4 border-light">
        <ul
          class="space-y-3 font-normal"
          :aria-labelledby="`mega-menu-${Menu.toLowerCase().replace(/\s+/g, '-')}-button`"
        >
          <li v-for="item in ItemsInMenu" :key="item.NameInMenu">
            <a
              :href="item.Link"
              @click="handleItemClick(item)"
              class="inline-flex items-center text-body hover:text-fg-brand transition-colors duration-200"
            >
              <span v-if="item.icon" class="w-4 h-4 me-1.5" v-html="item.icon"></span>
              {{ item.NameInMenu }}
            </a>
          </li>
        </ul>
      </div>

      <div
        v-for="(column, columnIndex) in displayColumns"
        :key="columnIndex"
        class="p-4 pb-0 md:pb-4 border-light last:border-r-0"
      >
        <h4
          v-if="column.title"
          class="font-semibold text-heading mb-3 text-xs uppercase tracking-wide"
        >
          {{ column.title }}
        </h4>
        <ul class="space-y-3 font-normal">
          <li v-for="item in column.items" :key="item.name">
            <a
              :href="item.link"
              @click="handleItemClick(item)"
              class="inline-flex items-center text-body hover:text-fg-brand transition-colors duration-200"
            >
              <svg
                v-if="item.icon"
                class="w-4 h-4 me-1.5"
                aria-hidden="true"
                fill="none"
                viewBox="0 0 24 24"
              >
                <g v-html="item.icon"></g>
              </svg>
              {{ item.name }}
            </a>
          </li>
        </ul>
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent, ref, computed, onMounted, onBeforeUnmount } from 'vue'

interface MenuItem {
  NameInMenu: string
  Link: string
  icon?: string
}

interface ColumnItem {
  name: string
  link: string
  icon?: string
}

interface Column {
  title?: string
  items: ColumnItem[]
}

export default defineComponent({
  name: 'MenuDropDown',
  props: {
    Menu: {
      type: String,
      required: true,
    },
    ItemsInMenu: {
      type: Array as () => MenuItem[],
      required: true,
    },
    Columns: {
      type: Array as () => Column[],
      required: true,
    },
  },
  setup(props) {
    const isDropdownOpen = ref(false)

    const toggleDropdown = (event: MouseEvent) => {
      event.stopPropagation() // Prevent the click from immediately closing the dropdown
      isDropdownOpen.value = !isDropdownOpen.value
    }

    const handleItemClick = (item: MenuItem | ColumnItem) => {
      isDropdownOpen.value = false
      console.log('Item clicked:', item)
    }

    const displayColumns = computed(() => {
      return props.Columns
    })

    const handleClickOutside = (event: MouseEvent) => {
      const dropdownButton = document.getElementById(
        `mega-menu-${props.Menu.toLowerCase().replace(/\s+/g, '-')}-button`,
      )
      const dropdownMenu = document.getElementById(
        `mega-menu-${props.Menu.toLowerCase().replace(/\s+/g, '-')}-dropdown`,
      )

      // Check if click is outside both button and dropdown
      if (
        dropdownButton &&
        !dropdownButton.contains(event.target as Node) &&
        dropdownMenu &&
        !dropdownMenu.contains(event.target as Node)
      ) {
        isDropdownOpen.value = false
      }
    }

    onMounted(() => {
      document.addEventListener('click', handleClickOutside)
    })

    onBeforeUnmount(() => {
      document.removeEventListener('click', handleClickOutside)
    })

    return {
      isDropdownOpen,
      toggleDropdown,
      handleItemClick,
      displayColumns,
    }
  },
})
</script>

<style scoped>
.rotate-180 {
  transform: rotate(180deg);
}
</style>
<!-- <template>
  <div class="relative">
    <button
      @click="toggleDropdown"
      class="flex items-center justify-between bg-green-600 text-white px-4 py-2 rounded-lg font-medium hover:bg-green-700 transition-colors duration-200"
    >
      <span class="flex items-center">
        <svg class="w-4 h-4 mr-2" fill="none" stroke="currentColor" viewBox="0 0 24 24">
          <path
            stroke-linecap="round"
            stroke-linejoin="round"
            stroke-width="2"
            d="M4 6h16M4 12h16M4 18h16"
          />
        </svg>
        {{ Menu }}
      </span>
      <svg
        class="w-4 h-4 ml-2 transition-transform duration-200"
        :class="{ 'rotate-180': isDropdownOpen }"
        fill="none"
        stroke="currentColor"
        viewBox="0 0 24 24"
      >
        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M19 9l-7 7-7-7" />
      </svg>
    </button>

    <div
      v-if="isDropdownOpen"
      class="absolute top-full left-0 mt-2 w-96 bg-white border border-gray-200 rounded-lg shadow-xl z-50"
    >
      <div class="p-6">
        <div class="grid grid-cols-2 gap-8">
          <div class="space-y-4">
            <h3 class="font-semibold text-gray-900 text-sm uppercase tracking-wide mb-3">
              Popular Categories
            </h3>
            <ul class="space-y-3">
              <li v-for="item in ItemsInMenu" :key="item.NameInMenu">
                <a
                  :href="item.Link"
                  @click="handleItemClick(item)"
                  class="flex items-center text-sm text-gray-700 hover:text-green-600 transition-colors duration-200"
                >
                  {{ item.NameInMenu }}
                </a>
              </li>
            </ul>
          </div>

          <div class="space-y-6">
            <div v-for="(column, columnIndex) in Columns" :key="columnIndex" class="space-y-3">
              <h4 class="font-semibold text-gray-900 text-sm uppercase tracking-wide">
                {{ column.title }}
              </h4>
              <ul class="space-y-2">
                <li v-for="item in column.items" :key="item.name">
                  <a
                    :href="item.link"
                    @click="handleItemClick(item)"
                    class="text-sm text-gray-600 hover:text-green-600 transition-colors duration-200"
                  >
                    {{ item.name }}
                  </a>
                </li>
              </ul>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent, ref, onMounted, onBeforeUnmount } from 'vue'
interface MenuItem {
  NameInMenu: string
  Link: string
  icon?: string
}

interface ColumnItem {
  name: string
  link: string
  icon?: string
}

interface Column {
  title?: string
  items: ColumnItem[]
}

export default defineComponent({
  name: 'MenuDropDown',
  props: {
    Menu: {
      type: String,
      required: true,
    },
    ItemsInMenu: {
      type: Array as () => MenuItem[],
      required: true,
    },
    Columns: {
      type: Array as () => Column[],
      required: true,
    },
  },
  setup(props) {
    const isDropdownOpen = ref(false)

    const toggleDropdown = (event: MouseEvent) => {
      event.stopPropagation()
      isDropdownOpen.value = !isDropdownOpen.value
    }

    const handleItemClick = (item: MenuItem | ColumnItem) => {
      isDropdownOpen.value = false
      console.log('Item clicked:', item)
    }

    const handleClickOutside = (event: MouseEvent) => {
      const dropdownElement = document.querySelector('.relative')
      if (dropdownElement && !dropdownElement.contains(event.target as Node)) {
        isDropdownOpen.value = false
      }
    }

    onMounted(() => {
      document.addEventListener('click', handleClickOutside)
    })

    onBeforeUnmount(() => {
      document.removeEventListener('click', handleClickOutside)
    })

    return {
      isDropdownOpen,
      toggleDropdown,
      handleItemClick,
    }
  },
})
</script>

<style scoped>
.rotate-180 {
  transform: rotate(180deg);
}
</style> -->
