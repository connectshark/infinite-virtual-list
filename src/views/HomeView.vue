<template>
<div class=" absolute top-0 left-0 p-3 rounded-2xl bg-slate-900/60 backdrop-blur-lg">
  <p>列表總數量: {{ data.length }}</p>
  <p>已載入列表數量: {{ list.length }}</p>
</div>
<main v-bind="containerProps" class="h-screen pt-2">
  <ul v-bind="wrapperProps" class="mx-auto max-w-sm">
    <li v-for="{ data, index } in list" :key="index" class="mb-6 font-bold p-4 rounded-lg bg-slate-600">
      <div class=" text-2xl font-bold leading-loose">{{data}}!!</div>
      <p class="leading-loose">Row Index: {{ index }}</p>
    </li>
  </ul>
</main>
</template>

<script setup>
import { ref } from 'vue'
import { useVirtualList, useInfiniteScroll } from '@vueuse/core'


const data = ref(Array.from(Array(50).keys(), () => 'Hello'))

const { list, containerProps, wrapperProps } = useVirtualList(
  data,
  {
    itemHeight: 112+24
  }
)

useInfiniteScroll(
  containerProps.ref,
  () => {
    data.value.push(...Array.from(Array(10).keys(), () => 'Hello'))
  }
)
</script>