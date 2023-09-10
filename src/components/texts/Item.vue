<script setup>
import { ref, computed } from "vue"
// import { RouterLink } from "vue-router"

const props = defineProps({
  todotext: {
    type: Object,
    required: true,
  },
})
const isChecked = ref(false)

const emits = defineEmits(["remove-auo-item"])

const remove = () => {
  emits("remove-auo-item", props.todotext.id)
}
// const url = computed(() => `/devices/${props.todotext.id}`)
</script>

<template>
  <li class="flex items-center justify-between px-3 py-3 my-3 bg-slate-200">
    <!-- <RouterLink :to="url">{{ todotext.title }}</RouterLink> -->
    <div class="text-lg">
      <label class="space-x-3">
        <input type="checkbox" v-model="isChecked" />
        <span :class="{ completed: isChecked }">{{ props.todotext.title }}</span>
      </label>
    </div>
    <button class="px-2 py-1 text-white bg-black" @click="remove">X</button>
  </li>
</template>

<style scoped>
.completed {
  @apply line-through text-gray-500;
}
</style>
