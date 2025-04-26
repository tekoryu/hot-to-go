<script lang="ts" setup>
import ListItem from './ListItem.vue'
import { ref, onMounted, computed } from 'vue'
import type { Ref } from 'vue'

type Item = {
  title: string
  checked?: boolean
}

const storageItems: Ref<Item[]> = ref([])

// const listItems: Ref<Item[]> = ref([
//   { title: 'Make a todo list app', checked: true },
//   { title: 'Predict the Weather', checked: false },
//   { title: 'Play some tunes', checked: false },
//   { title: 'Pump some iron', checked: false },
//   { title: 'Track my expenses', checked: false },
//   { title: 'Organize a game night', checked: false },
//   { title: 'Learn a new language', checked: false },
//   { title: 'Publish my work', checked: false },
// ])

const updateItem = (item: Item): void => {
  const updatedItem = findItemInList(item)
  if (updatedItem) {
    toggleItemChecked(updatedItem)
    setToStorage(storageItems.value) // Store the updated list in local storage
  }
}

const findItemInList = (item: Item): Item | undefined => {
  return storageItems.value.find((itemInList: Item) => itemInList.title === item.title)
}

const toggleItemChecked = (item: Item): void => {
  if (item) {
    item.checked = !item.checked
  }
}

const sortedList = computed(() =>
  [...storageItems.value].sort((a, b) => (a.checked ? 1 : 0) - (b.checked ? 1 : 0)),
)

const setToStorage = (items: Item[]): void => {
  localStorage.setItem('list-items', JSON.stringify(items)) // list-items is the same as listItems
  console.log('List items saved to local storage:', JSON.stringify(items))
}

const getFromStorage = (): Item[] | [] => {
  const stored = localStorage.getItem('list-items')
  if (stored) {
    console.log('List items retrieved from local storage:', stored)
    return JSON.parse(stored)
  }
  return []
}

const initListItems = (): void => {
  if (storageItems.value?.length === 0) {
    const listItems = [
      { title: 'Make a todo list app', checked: true },
      { title: 'Predict the Weather', checked: false },
      { title: 'Play some tunes', checked: false },
      { title: 'Pump some iron', checked: false },
      { title: 'Track my expenses', checked: false },
      { title: 'Organize a game night', checked: false },
      { title: 'Learn a new language', checked: false },
      { title: 'Publish my work', checked: false },
    ]

    setToStorage(listItems) // Store the initial list in local storage
    storageItems.value = listItems // Assign the initial list to the storageItems reference, that is reactive
  }
}

onMounted(() => {
  storageItems.value = getFromStorage() // Get the list from local storage
  initListItems() // Initialize the list items when the component is mounted
})
</script>

<template>
  <ul>
    <li :key="key" v-for="(item, key) in sortedList">
      <ListItem :isChecked="item.checked" v-on:click.prevent="updateItem(item)">{{
        item.title
      }}</ListItem>
    </li>
  </ul>
</template>

<style scoped>
ul {
  list-style: none;
  margin: 0.4rem;
}
</style>
