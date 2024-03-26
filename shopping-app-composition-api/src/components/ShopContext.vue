<script setup>
import { defineProps, defineEmits, ref } from 'vue';

const emits = defineEmits(['onRedirectToCheckOut']);
const props = defineProps(['products']);

const allCardProducts = ref(props.products);
console.log(allCardProducts);
const redirectToCheckOut = () => {
    emits('onRedirectToCheckOut');
};
</script>

<template>
    <div class="context-wrapper">
        <div v-for="product in allCardProducts" :key="product.id" class="context-item">
            <div class="image">
                <img :src="product.image ? product.image : 'https://www.generationsforpeace.org/wp-content/uploads/2018/03/empty.jpg'" :alt="product.title">
            </div>
            <div class="content">
                <div class="title">{{ product.title }}</div>
                <div class="price">${{ product.price }}</div>
            </div>
        </div>
        <div @click="redirectToCheckOut" class="context-item complate-box">Complate The Shopping</div>
    </div>
</template>


<style scoped>
.context-wrapper {
    z-index: 10;
    position: absolute;
    background-color: #fff;
    right: 0;
    box-shadow: 0px 4px 8px rgba(0, 0, 0, 0.25);
    padding-top: 1.5rem;
    border-radius: 15px;
    max-width: 600px;
    min-width: 350px;
    filter: drop-shadow(0 8px 12px rgba(0, 0, 0, 0.15));  
}

.context-item {
    display: flex;
    padding: 0 1rem 0 1rem;
    border-bottom: 3px solid rgba(204, 202, 202, 0.785);
}

.image {
    margin-right: 1rem;
    margin-top: 1rem;
}

.image img {
    width: 50px;
    height: 50px;
    object-fit: fill;
}

.content {
    font-weight: 500;
    margin-top: 1rem;
    display: flex;
    flex-direction: column;
}

.price {
    margin-top: 0.3rem;
    margin-bottom: 1rem;
    font-size: 12px;
}

.title {
    font-weight: 600;
    color: #2c3e50;
    text-transform: uppercase;
    letter-spacing: 2px;
    font-size: 14px;
}

.complate-box {
   display: flex;
   justify-content: center;
   align-items: center; 
   padding: 1rem 0;
   color: #192430;
   border-bottom: none;
   font-size: 14px;
   border-radius: 0 0 15px 15px;
}

.complate-box:hover, .complate-box:focus{
    background-color: #80b6eca5;
}
</style>