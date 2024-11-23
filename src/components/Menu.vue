<template>
    <ul class="list-group">
        <li class="list-group-item" v-for="drink in drinks" :key=drink.id @click="addToCart(drink)">
            <div>
                {{ drink.name }} | ${{ drink.price }} | {{ drink.description }}
            </div>
        </li>
    </ul>
</template>

<script setup>
import { defineProps, defineEmits } from 'vue';
defineProps(['drinks'])
const emit = defineEmits(["emitAddToCart"]);

const addToCart = (drink) => {
    emit("emitAddToCart", { ...drink, quantity: 1 });
}


</script>

<style scoped>
.list-group-item {
    cursor: pointer;
}
</style>