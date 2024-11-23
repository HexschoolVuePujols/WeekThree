<script setup>
import { ref, computed } from 'vue'
import Menu from '@/components/Menu.vue'
import Cart from '@/components/Cart.vue'
import Order from '@/components/Order.vue'

const drinks = ref([
  {
    id: 1,
    name: '珍珠奶茶',
    description: '香濃奶茶搭配QQ珍珠',
    price: 50,
  },
  {
    id: 2,
    name: '冬瓜檸檬',
    description: '清新冬瓜配上新鮮檸檬',
    price: 45,
  },
  {
    id: 3,
    name: '翡翠檸檬',
    description: '綠茶與檸檬的完美結合',
    price: 55,
  },
  {
    id: 4,
    name: '四季春茶',
    description: '香醇四季春茶，回甘無比',
    price: 45,
  },
  {
    id: 5,
    name: '阿薩姆奶茶',
    description: '阿薩姆紅茶搭配香醇鮮奶',
    price: 50,
  },
  {
    id: 6,
    name: '檸檬冰茶',
    description: '檸檬與冰茶的清新組合',
    price: 45,
  },
  {
    id: 7,
    name: '芒果綠茶',
    description: '芒果與綠茶的獨特風味',
    price: 55,
  },
  {
    id: 8,
    name: '抹茶拿鐵',
    description: '抹茶與鮮奶的絕配',
    price: 60,
  },
]);
const cart = ref([]);
const remark = ref("");

const sum = computed(() => {
  // let total = 0;
  // cart.value.forEach(item=> {
  //   total += item.quantity * item.price;
  // });
  // return total;

  return cart.value.reduce((prev, current) => {
    return prev + current.price * current.quantity;
  }, 0);


});

const addToCart = (drink) => {
  const target = cart.value.find(item => item.id === drink.id);

  if (target) {
    return;
  }

  const cartDrink = { ...drink, quantity: 1 };
  cart.value.push(cartDrink);
}

const removeFromCart = (drink) => {

  const target = cart.value.find(item => item.id === drink.id);
  const index = cart.value.indexOf(target);
  cart.value.splice(index, 1);

}


const order = ref({
  drinks: [],
  remark: "",
  sum: 0
});
const submitOrder = () => {
  order.value.drinks = [];

  cart.value.forEach(item => {
    order.value.drinks.push({ ...item });
  });
  order.value.remark = remark.value;
  order.value.sum = sum.value;

  cart.value = [];
}


</script>

<template>
  <main class="mt-3">
    <div class="container">
      <div class="row">
        <div class="col-md-4">
          <Menu :drinks="drinks" @emitAddToCart="addToCart"></Menu>
        </div>
        <div class="col-md-4">
          <Cart :cart="cart" @emitSubmitOrder="submitOrder" @emitRemoveFromCart="removeFromCart"></Cart>
        </div>
      </div>
      <hr>
      <div class="row">
        <div class="col-8">
          <Order v-if="order" :order="order"></Order>
        </div>
      </div>
    </div>

  </main>
</template>