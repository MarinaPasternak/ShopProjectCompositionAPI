<script setup>
import { onMounted, ref, watch } from 'vue';
import ShopContext from '@/components/ShopContext.vue';
import ProductCard from '@/components/ProductCard.vue';

const isShopContextVisible = ref(false);
const categories = ref([]);
const products = ref([]);
const cardProducts = ref([]);
const activeCategory = ref(null);

const openShopContext = () => {
  isShopContextVisible.value = !isShopContextVisible.value;
};

const fetchAllCategories = async () => {
  try {
    const response  = await fetch('https://fakestoreapi.com/products/categories');
    const jsonData = await response.json();
    categories.value = jsonData;
  } catch(error) {
    console.log(error);
  }
};

const fetchAllProducts = async () => {
  try {
    const response  = await fetch('https://fakestoreapi.com/products');
    const jsonData = await response.json();
    products.value = jsonData;
  } catch(error) {
    console.log(error);
  }
};

const fetchProductsByCategory = async () => {
  try {
    const response  = await fetch(`https://fakestoreapi.com/products/category/${activeCategory.value}`);
    const jsonData = await response.json();
    products.value = jsonData;
  } catch(error) {
    console.log(error);
  }
};

const updateProductCard = (e) => {
  cardProducts.value.push(e.value);
};

onMounted(() => {
  fetchAllCategories();
  fetchAllProducts();
});

watch(activeCategory, (newActiveCategory) => {
  if (!newActiveCategory) {
    fetchAllProducts();
  } else {
    fetchProductsByCategory();
  }
});
</script>

<template>
  <div class="filter-wrapper">
    <div class="top-flex-block">
      <div class="categories-block">
        <div 
          :class = "activeCategory === item ? 'active-category': ''"
          @click="activeCategory = activeCategory === item ? '': item" 
          v-for="item in categories" :key="item" 
          class="category-block">
            {{ item }}
        </div>
      </div>
      <div class="box">
        <div class="cart-icon-container" @click="openShopContext">
          <div class="items-in-cart-block">
            <p>{{ cardProducts.length }}</p>
          </div>
          <svg 
              fill="#2c3e50" 
              version="1.1" 
              id="Capa_1" 
              xmlns="http://www.w3.org/2000/svg" 
              xmlns:xlink="http://www.w3.org/1999/xlink" 
              width="34px" 
              height="34px" 
              viewBox="0 0 902.86 902.86" 
              xml:space="preserve">
                  <g id="SVGRepo_bgCarrier" stroke-width="0"></g>
                  <g 
                      id="SVGRepo_tracerCarrier" 
                      stroke-linecap="round" 
                      stroke-linejoin="round"></g>
                  <g id="SVGRepo_iconCarrier"> 
                    <g>
                        <g> 
                            <path 
                                d="M671.504,577.829l110.485-432.609H902.86v-68H729.174L703.128,179.2L0,178.697l74.753,399.129h596.751V577.829z M685.766,247.188l-67.077,262.64H131.199L81.928,246.756L685.766,247.188z"></path> 
                            <path 
                                d="M578.418,825.641c59.961,0,108.743-48.783,108.743-108.744s-48.782-108.742-108.743-108.742H168.717 c-59.961,0-108.744,48.781-108.744,108.742s48.782,108.744,108.744,108.744c59.962,0,108.743-48.783,108.743-108.744 c0-14.4-2.821-28.152-7.927-40.742h208.069c-5.107,12.59-7.928,26.342-7.928,40.742 C469.675,776.858,518.457,825.641,578.418,825.641z M209.46,716.897c0,22.467-18.277,40.744-40.743,40.744 c-22.466,0-40.744-18.277-40.744-40.744c0-22.465,18.277-40.742,40.744-40.742C191.183,676.155,209.46,694.432,209.46,716.897z M619.162,716.897c0,22.467-18.277,40.744-40.743,40.744s-40.743-18.277-40.743-40.744c0-22.465,18.277-40.742,40.743-40.742 S619.162,694.432,619.162,716.897z"></path>
                        </g> 
                    </g>
                  </g>
            </svg>
        </div>
        <ShopContext 
              @onRedirectToCheckOut="openShopContext"
              v-if="isShopContextVisible"
              :products="cardProducts"
        ></ShopContext>
      </div>
    </div>
  </div>
  <div class="bottom-flex-block">
   <ProductCard 
      v-for="item in products" 
      :product="item" 
      :key="item.title" 
      @onItemAdded="updateProductCard($event)"></ProductCard>
  </div>
</template>

<style scoped>
.filter-wrapper {
  display: flex;
  justify-content: space-between;
  align-items: center;
  gap: 25px;
  flex-wrap: wrap;
  margin-bottom: 3rem;
}

.top-flex-block {
  display: flex;
  align-items: start;
  gap: 25px;
  justify-content: space-between;
  width: 100%;
}

.categories-block {
  display: flex;
  align-items: start;
  gap: 25px;
  width: 100%;
}

.category-block {
  cursor: pointer;
  padding: 1rem 1.5rem;
  background-color: #e3e3e391;
  font-size: 16px;
  font-weight: 600;
  border-radius: 15px;
  margin: 1rem 0 0 1rem;
}

.active-category {
  border: 2px solid rgb(73, 168, 73);
  background-color: rgb(194, 244, 194);
  font-weight: 600;
}

.box {
  position: relative;
  cursor: pointer;
  transition: all 0.5s;
}

.box:hover {
  color: #1d5184;
}

.items-in-cart-block {
  display: flex;
  align-items: center;
  justify-content: center;
  position: absolute;
  top: -13px;
  right: 10px;
  background-color: #1d5184;
  color: #fff;
  font-size: 16px;
  border-radius: 15px;
}

.items-in-cart-block p {
  margin: 0;
  padding: 3px;
}

.bottom-flex-block {
  display: flex;
  justify-content: center;
  align-items: center;
  flex-wrap: wrap;
  gap: 3rem;
}
</style>
