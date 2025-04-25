<script lang="ts" setup>
import ListItem from './ListItem.vue'
import { ref, computed } from 'vue'
import type { Ref } from 'vue'

type Item = {
  title: string
  checked?: boolean
}

// The listItems array is a reactive reference that contains the list of items.
// Each item is an object with a title and a checked property.
// The checked property is optional and defaults to false.
const listItems: Ref<Item[]> = ref([
  { title: 'Make a todo list app', checked: true },
  { title: 'Predict the Weather', checked: false },
  { title: 'Play some tunes', checked: false },
  { title: 'Pump some iron', checked: false },
  { title: 'Track my expenses', checked: false },
  { title: 'Organize a game night', checked: false },
  { title: 'Learn a new language', checked: false },
  { title: 'Publish my work', checked: false },
])

// The updateItem function takes an item as an argument and finds it in the listItems array.
// If the item is found, it toggles its checked property using the toggleItemChecked function.
const updateItem = (item: Item): void => {
  const updateItem = findItemInList(item)
  if (updateItem) {
    toggleItemChecked(updateItem)
  }
}

const findItemInList = (item: Item): Item | undefined => {
  return listItems.value.find((itemInList: Item) => itemInList.title === item.title)
}

const toggleItemChecked = (item: Item): void => {
  if (item) {
    item.checked = !item.checked
  }
}

// The sortedList computed property sorts the listItems array based on the checked property.
const sortedList = computed(() =>
  [...listItems.value].sort((a, b) => (a.checked ? 1 : 0) - (b.checked ? 1 : 0)),
)

// Preserving changes to the list
const setToStorage = (items: Item[]) => {
  localStorage.setItem('list-items', JSON.stringify(items)) // list-items is the same as listItems
}

const getFromStorage = (): Item[] | [] => {
  const stored = localStorage.getItem('list-items')
  if (stored) {
    return JSON.parse(stored)
  }
  return []
}
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
