<script setup lang="ts">
import { ref } from 'vue'

interface Item {
    name: string
    price: number
}

const items = ref<Item[]>([
    { name: '鉛筆', price: 300 },
    { name: 'ノート', price: 400 },
    { name: '消しゴム', price: 500 },
])

const newItemName = ref('')
const newItemPrice = ref(0)

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
    <div>
        <div>ItemList</div>
        <ul>
            <li v-for="item in items" :key="item.name" :class="{over500:item.price>=500}">
                <div>名前：{{ item.name }}</div>
                <div>{{ item.price }}円</div>
                <div v-if="item.price>=10000">高額商品</div>
            </li>
        </ul>
        <div>
            <label>
                名前：
                <input v-model="newItemName" type="text" />
            </label>
            <label>
                価格：
                <input v-model.number="newItemPrice" type="number" />
            </label>
            <button @click="addItem">追加</button>
        </div>
    </div>
</template>

<style>
    .over500{
        color: red;
    }
</style>