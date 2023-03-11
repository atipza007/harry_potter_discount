<script setup>
import { ref } from 'vue'

const dataBook = ref([
  {
    id: 1,
    name: "แฮร์รี่ พอตเตอร์ กับศิลาอาถรรพ์",
    url: "./assets/pic_harry/harry_1.jpg",
    amount: 1,
    price: 100,
    discount: 0,
    disable: false
  },
  {
    id: 2,
    name: "แฮร์รี่ พอตเตอร์ กับห้องแห่งความลับ",
    url: "./assets/pic_harry/harry_2.jpg",
    amount: 1,
    price: 100,
    discount: 0,
    disable: false
  },
  {
    id: 3,
    name: "แฮร์รี่ พอตเตอร์ กับนักโทษแห่งอัซคาบัน",
    url: "./assets/pic_harry/harry_3.jpg",
    amount: 1,
    price: 100,
    discount: 0,
    disable: false
  },
  {
    id: 4,
    name: "แฮร์รี่ พอตเตอร์ กับถ้วยอัคนี",
    url: "./assets/pic_harry/harry_4.jpg",
    amount: 1,
    price: 100,
    discount: 0,
    disable: false
  },
  {
    id: 5,
    name: "แฮร์รี่ พอตเตอร์ กับภาคีนกฟีนิกซ์",
    url: "./assets/pic_harry/harry_5.jpg",
    amount: 1,
    price: 100,
    discount: 0,
    disable: false
  },
  {
    id: 6,
    name: "แฮร์รี่ พอตเตอร์ กับเจ้าชายเลือดผสม",
    url: "./assets/pic_harry/harry_6.jpg",
    amount: 1,
    price: 100,
    discount: 0,
    disable: false
  },
  {
    id: 7,
    name: "แฮร์รี่ พอตเตอร์ กับเครื่องรางยมทูต",
    url: "./assets/pic_harry/harry_7.jpg",
    amount: 1,
    price: 100,
    discount: 0,
    disable: false
  },

])

const cartItems = ref([]);
const totalBook = ref(0);
const allPrice = ref(0);
const discount = ref(0);
const price = ref(0);

function loadpic(url) {
  const imageUrl = new URL(url, import.meta.url).href;
  return imageUrl;
}

function addItem(item, index) {
  if (cartItems.value.indexOf(item) === -1) {
    cartItems.value.push(item);
    dataBook.value[index].disable = true;
    var count = 0;
    count++
    var countItem = count * item.amount
    var countCart = cartItems.value.length;
    var maxDiscount = 0
    totalBook.value = totalBook.value + countItem;
    allPrice.value = totalBook.value * 100;
    if (countCart == 2) {
      for (let i = 0; i < cartItems.value.length; i++) {
        if (cartItems.value[i].amount >= 2) {
          cartItems.value[i].discount = cartItems.value[i].amount * 100 * 0.1
        }
        maxDiscount = maxDiscount + cartItems.value[i].discount
      }
    } else if (countCart == 3) {
      for (let i = 0; i < cartItems.value.length; i++) {
        cartItems.value[i].discount = cartItems.value[i].amount * 100 * 0.2
        maxDiscount = maxDiscount + cartItems.value[i].discount
      }
    }
    else if (countCart == 4) {
      for (let i = 0; i < cartItems.value.length; i++) {
        cartItems.value[i].discount = cartItems.value[i].amount * 100 * 0.3
        maxDiscount = maxDiscount + cartItems.value[i].discount
      }
    } else if (countCart == 5) {
      for (let i = 0; i < cartItems.value.length; i++) {
        cartItems.value[i].discount = cartItems.value[i].amount * 100 * 0.4
        maxDiscount = maxDiscount + cartItems.value[i].discount
      }
    } else if (countCart == 6) {
      for (let i = 0; i < cartItems.value.length; i++) {
        cartItems.value[i].discount = cartItems.value[i].amount * 100 * 0.5
        maxDiscount = maxDiscount + cartItems.value[i].discount
      }
    } else if (countCart == 7) {
      for (let i = 0; i < cartItems.value.length; i++) {
        cartItems.value[i].discount = cartItems.value[i].amount * 100 * 0.6
        maxDiscount = maxDiscount + cartItems.value[i].discount
      }
    }
    discount.value = maxDiscount;
    price.value = allPrice.value - discount.value;
  }
}
function removeItem() {
  location.reload();
}
loadpic()
</script>

<template>
  <div class="mx-auto p-5">
    <div class="grid grid-cols-2 gap-2">
      <div class=" border-4 border-red-500">
        <div class="grid grid-cols-4 gap-4 p-2">
          <div v-for="(item, index) in dataBook" class="w-full max-w-sm bg-white rounded-lg border-2 border-blue-500">
            <a href="#">
              <img class="p-8 rounded-t-lg" :src="loadpic(item.url)" alt="product image" />
            </a>
            <div class="px-5 pb-5">
              <div class="h-[50px]">
                <a href="#">
                  <h5 class="text-sm font-semibold tracking-tight text-gray-900">{{ item.name }}</h5>
                </a>
              </div>
              <div class="flex items-center justify-between mt-1">
                <span class="text-lg font-bold text-gray-900">100฿</span>
                <select v-model.number="item.amount" :disabled="item.disable"
                  class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-15 p-2.5 disabled:opacity-75">
                  <option value=1 selected>1</option>
                  <option value=2>2</option>
                  <option value=3>3</option>
                  <option value=4>4</option>
                  <option value=5>5</option>
                  <option value=6>6</option>
                  <option value=7>7</option>
                  <option value=8>8</option>
                  <option value=9>9</option>
                  <option value=10>10</option>
                </select>
              </div>
              <div class=" flex justify-center mt-2">
                <a @click="addItem(item, index)"
                  class="text-white bg-blue-700 hover:bg-blue-800 focus:ring-4 focus:outline-none focus:ring-blue-300 font-medium rounded-lg text-sm px-5 py-2.5 text-center cursor-pointer">เพิ่ม
                </a>
              </div>
            </div>
          </div>
        </div>
      </div>
      <div class=" border-4 border-red-500">
        <div class="grid grid-cols-4 gap-4 p-2">
          <div v-for="(item, index) in cartItems" class="w-full max-w-sm bg-white rounded-lg border-2 border-blue-500">
            <a href="#">
              <img class="p-8 rounded-t-lg" :src="loadpic(item.url)" alt="product image" />
            </a>
            <div class="px-5 pb-5">
              <div class="h-[50px]">
                <a href="#">
                  <h5 class="text-sm font-semibold tracking-tight text-gray-900">{{ item.name }}</h5>
                </a>
              </div>
              <div class="flex items-center justify-between mt-3">
                <span class="text-lg font-bold text-gray-900">{{ item.amount * 100 }}฿</span>
              </div>
              <div class="flex text-center mt-6 mb-2">
                <span class="text-base font-bold text-gray-900">จำนวน : {{ item.amount }} เล่ม</span>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
    <div class="flex justify-between mt-2 text-2xl">
      <div class="flex justify-between gap-[75px] mt-4">
        <p>ทั้งหมด : {{ totalBook }} เล่ม</p>
        <p>ราคารวม : {{ allPrice }} บาท</p>
        <p>ส่วนลด : {{ discount }} บาท</p>
        <p>รวมสุทธิ : {{ price }} บาท</p>
      </div>
      <button @click="removeItem()"
        class="text-white bg-blue-700 hover:bg-blue-800 focus:ring-4 focus:outline-none focus:ring-blue-300 rounded-lg text-xl px-5 py-2.5 text-center">ลบทั้งหมด</button>
    </div>
  </div>
</template>
