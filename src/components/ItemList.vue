<script setup lang="ts">
import { ref } from 'vue'

interface Item {
    name: string
    price: number
}

const items = ref<Item[]>([
    { name: 'りんご', price: 100 },
    { name: 'ばなな', price: 3000 },
    { name: 'いちご', price: 600 },
])
const newItemName = ref<string>('')
const newItemPrice = ref<number>(0)

const addItem = () => {
    items.value.push({
        name: newItemName.value,
        price: newItemPrice.value,
    })
    newItemName.value = ''
    newItemPrice.value = 0
}
</script>

<template>
    <div>ItemList</div>
    <div>
        <label>
            名前
            <input v-model="newItemName" type="text" />
        </label>
        <label>
            価格
            <input v-model="newItemPrice" type="number" />
        </label>
        <button @click="addItem">追加</button>
    </div>
    <ul>
        <li v-for="item in items" :key="item.name" :class="{ over500: item.price >= 500 }">
            <div>名前: {{ item.name }}</div>
            <div>{{ item.price }} 円</div>
            <div v-if="item.price >= 10000">高額商品</div>
        </li>
    </ul>
</template>

<style>
.over500 {
    color: red;
}
</style>