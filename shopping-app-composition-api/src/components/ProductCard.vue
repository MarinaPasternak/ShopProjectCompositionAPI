<script setup>
import { defineProps, ref } from 'vue';
const props = defineProps(['product']);

const productData = ref(props.product);
</script>

<template>
    <div class="product-card-container">
        <div class="box">
            <svg fill="#2c3e50" version="1.1" id="Capa_1" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" width="24px" height="24px" viewBox="0 0 902.86 902.86" xml:space="preserve"><g id="SVGRepo_bgCarrier" stroke-width="0"></g><g id="SVGRepo_tracerCarrier" stroke-linecap="round" stroke-linejoin="round"></g><g id="SVGRepo_iconCarrier"> <g> <g> <path d="M671.504,577.829l110.485-432.609H902.86v-68H729.174L703.128,179.2L0,178.697l74.753,399.129h596.751V577.829z M685.766,247.188l-67.077,262.64H131.199L81.928,246.756L685.766,247.188z"></path> <path d="M578.418,825.641c59.961,0,108.743-48.783,108.743-108.744s-48.782-108.742-108.743-108.742H168.717 c-59.961,0-108.744,48.781-108.744,108.742s48.782,108.744,108.744,108.744c59.962,0,108.743-48.783,108.743-108.744 c0-14.4-2.821-28.152-7.927-40.742h208.069c-5.107,12.59-7.928,26.342-7.928,40.742 C469.675,776.858,518.457,825.641,578.418,825.641z M209.46,716.897c0,22.467-18.277,40.744-40.743,40.744 c-22.466,0-40.744-18.277-40.744-40.744c0-22.465,18.277-40.742,40.744-40.742C191.183,676.155,209.46,694.432,209.46,716.897z M619.162,716.897c0,22.467-18.277,40.744-40.743,40.744s-40.743-18.277-40.743-40.744c0-22.465,18.277-40.742,40.743-40.742 S619.162,694.432,619.162,716.897z"></path> </g> </g> </g></svg>
        </div>
        <div class="card-image">
            <img :src="productData.image ? productData.image : 'https://www.generationsforpeace.org/wp-content/uploads/2018/03/empty.jpg'" :alt="productData.title">
        </div>
        <div class="desc">
            <div class="button">DETAIL</div>
            <span class="title">{{ productData.title }}</span>
            <div class="price">${{ productData.price }}</div>
        </div>
    </div>
</template>

<style scoped>
.product-card-container {
    position: relative;
    overflow: hidden;
    cursor: pointer;
    width: 250px;
    background-color: #fff;
    box-shadow: 0px 4px 8px rgba(0, 0, 0, 0.25);
    border-radius: 15px;
}

.card-image {
    width: 100%;
    object-fit: fill;
    margin-bottom: 1rem;
    border-radius: 15px 15px 0 0;
}

.card-image img {
    width: 100%;
    height: 250px;
}

.desc {
    white-space: nowrap;
    overflow: hidden;
    text-overflow: ellipsis;
    color: #2c3e50;
    font-size: 12px;
    font-weight: 500;
    padding: 0.5rem;
    position: relative;
    max-height: 60px;
}

.price {
    margin-top: 0.5rem;
    font-weight: 500;
    color: #192430;
    font-size: 20px;
}

.button {
    display: flex;
    justify-content: center;
    align-items: center;
    position: absolute;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    transition: all .4s ease; /* Changed .4 to .4s for transition duration */
    background-color: rgba(204, 202, 202, 0.785);
    color: #2c3e50;
    font-weight: 500;
    transform: translateY(100px);
    letter-spacing: 12px;
}

.product-card-container:hover > .desc > .button,
.product-card-container:focus > .desc > .button {
    background-color: #64a4e4;
    transform: translateY(0px);
    color: #fff;
    font-weight: 600;
}

.title {
    font-weight: 600;
    color: #2c3e50;
    text-transform: uppercase;
    letter-spacing: 2px;
    font-size: 14px;
}

.box {
    width: 35px;
    height: 35px;
    position: absolute;
    background-color: #fff;
    border: 1px solid rgba(204, 202, 202, 0.785);
    border-radius: 100%;
    top: 8px;
    right: 15px;
    display: flex;
    justify-content: center;
    align-items: center;
}
</style>