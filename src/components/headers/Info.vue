<script setup>
import { computed } from "vue"

const props = defineProps({
  todotextlist: {
    type: Array,
    required: true,
    default: [],
  },
})

const textsCount = computed(() => props.todotextlist.length)
const noText = computed(() => textsCount.value === 0)
</script>

<template>
  <h3 v-if="noText">目前無任何 todo 待辦事項</h3>
  <h3 v-else>目前共計 {{ textsCount }} 項事項需處理</h3>
</template>
