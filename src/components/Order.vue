<template>
    <div v-if="order.drinks.length == 0" class="card">
        尚未建立訂單
    </div>
    <div v-else class="card">
        <div class="card-body">
            <div class="card-title">
                <h5>訂單</h5>
                <table class="table">
                    <thead>
                        <tr>
                            <td>品項</td>
                            <td>數量</td>
                            <td>小計</td>
                        </tr>
                    </thead>
                    <tbody>
                        <tr v-for="item in order.drinks" :key="item.id">
                            <td>{{ item.name }}</td>
                            <td>{{ item.quantity }}</td>
                            <td>{{ item.price * item.quantity }}</td>
                        </tr>
                    </tbody>
                </table>
                <div class="text-end">備註:{{ order.remark }}</div>
                <div class="text-end">總計: ${{ order.sum }}</div>
            </div>
        </div>
    </div>

</template>

<script setup>
import { defineProps } from 'vue';

const props = defineProps(["order"]);


</script>