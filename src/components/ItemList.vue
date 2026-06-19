<script setup lang="ts">
import { ref } from 'vue'

interface Item { 
  name: string
  price: number
} 

const items = ref<Item[]>([ 
  { name: 'たまご', price: 100 }, 
  { name: 'りんご', price: 160 } 
])

// initialization
const newItemName = ref('')
const newItemPrice = ref(0)

const addItem = () => {
    if (
        items.value.some(
            item => item.name === newItemName.value
        ) 
    ) {
        // terminate this function at this point
        return 
    }
    if (newItemName.value === '') {
        return
    }
    // add new items into the array named items
    items.value.push({ name: newItemName.value, price: newItemPrice.value})

    newItemName.value = ''
    newItemPrice.value = 0
}

const deleteItem = (name: string) => {
    items.value = items.value.filter(
        item => item.name !== name
    )
}
</script>

<template>
  <div>
    <div>ItemList</div>
    <ul>
        <!-- take each item out of 'items' and put it into 'item' -->
        <li v-for = "item in items" :key = "item.name" :class="{ over500: item.price >= 500 }">
            <div>名前: {{ item.name }}</div>
            <div>{{ item.price }} 円</div>
            <div v-if="item.price >= 10000">高額商品</div>
            <!--  -->
            <button @click = "deleteItem(item.name)">削除</button>
        </li>
    </ul>
    <div>
        <label>
            名前
            <!-- synchronize the input field with the variable -->
            <input v-model = "newItemName" type = "text" />
        </label>
        <label>
            価格
            <input v-model = "newItemPrice" type = "number" />
        </label>
        <button @click = "addItem">追加</button>
    </div>
  </div>
</template>

<!-- CSS -->
<style>
.over500 { 
  color: red; 
} 
</style>