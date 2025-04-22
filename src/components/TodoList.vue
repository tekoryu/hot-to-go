<script lang="ts" setup>
import ListItem from './ListItem.vue'
import { ref, Ref } from 'vue'

type Item = {
  title: string
  checked?: boolean
}

const listItems: Ref<Item[]> = ref([
  { title: 'Make a todo list app', checked: true },
  { title: 'Predict the Weather', checked: false },
  { title: 'Play some tunes', checked: false },
  { title: 'Make a todo list app', checked: false },
  { title: 'Make a todo list app', checked: false },
  { title: 'Pump some iron', checked: false },
  { title: 'Track my expenses', checked: false },
  { title: 'Organize a game night', checked: false },
  { title: 'Learn a new language', checked: false },
  { title: 'Publish my work', checked: false },
])
</script>

<template>
  <ul>
    <li :key="key" v-for="(item, key) in listItems">
      <ListItem :isChecked="item.checked">{{ item.title }}</ListItem>
    </li>
  </ul>
</template>

<style scoped>
ul {
  list-style: none;
  margin: 0.4rem;
}
</style>
