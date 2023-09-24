<script setup>
import { computed, ref } from 'vue';

defineProps({
    categoryName: String
})

const itemsList = ref([])
const watchedList = ref([])
const newItemName = ref();

const isListFinished = computed(() => 
    itemsList.value.length > 0 && itemsList.value.length === watchedList.value.length
)

const onAddItem = () => {
    if(newItemName.value && !itemsList.value.includes(newItemName.value)) {
        itemsList.value.push(newItemName.value);
        resetInputValue();
    }
}

const onRemoveItem = (index) => {
   itemsList.value.splice(index, 1)
}

const resetInputValue = () => newItemName.value = undefined
</script>

<template>
    <div>
        <p>{{ categoryName }}</p>
        <ul>
            <li v-for="(item, index) in itemsList" :key="`item-${index}`">
                <input type="checkbox" :value="item" v-model="watchedList">
                <span 
                    :style="{'text-decoration': watchedList.includes(item) ? 'line-through' : 'none'}"
                >{{ item }}</span>
                <button @click="onRemoveItem(index)">Excluir</button>
            </li>
        </ul>
        <input v-model="newItemName" @keypress.enter="onAddItem"/>
        <button @click="onAddItem">Add Item</button>
        <p v-if="isListFinished">Você finalizou toda a lista, parabéns!</p>
    </div>
</template>

<style scoped>

</style>