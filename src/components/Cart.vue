<template>
    <table class="table">
        <thead>
            <tr>
                <th>操作</th>
                <th>品項</th>
                <th>描述</th>
                <th>數量</th>
                <th>單價</th>
                <th>小計</th>
            </tr>
        </thead>
        <tbody v-if="cart.length > 0">
            <tr v-for="item in cart" :key="item.id">
                <td><button type="button" @click="removeFromCart(item)" class="btn-delete">X</button> </td>
                <td>{{ item.name }}</td>
                <td>{{ item.description }}</td>
                <td>
                    <select v-model="item.quantity">
                        <option v-for="i in 10" :key="i" :value="i">{{ i }}</option>
                    </select>
                </td>
                <td>{{ item.price }}</td>
                <td>{{ item.price * item.quantity }}</td>
            </tr>
        </tbody>
    </table>
    <div v-if="cart.length == 0">
        請選擇商品
    </div>
    <div v-else>
        總計: ${{ sum }}
    </div>
    <div v-if="cart.length > 0" style="text-align: right;">
        <textarea v-if="cart.length != 0" v-model="remark" class="remark" placeholder="備註"
            style="width: 100%;"></textarea>
        <button type="button" @click="submitOrder">送出</button>
    </div>
</template>

<script setup>
import { ref, watch, defineProps, defineEmits } from 'vue';

const props = defineProps(["cart"]);
const emit = defineEmits(["emitSubmitOrder", "emitRemoveFromCart"]);


const remark = ref("");
const sum = ref(0);

watch(props.cart, (newValue) => {
    let total = 0;
    if (newValue) {
        newValue.forEach(item => {
            total += item.quantity * item.price;
        });
        sum.value = total;
    }
});

const submitOrder = () => {
    emit("emitSubmitOrder", {
        drinks: props.cart.value,
        remark: remark.value,
        sum: sum.value
    });
}

const removeFromCart = (drink) => {
    emit("emitRemoveFromCart", drink);
}


</script>
