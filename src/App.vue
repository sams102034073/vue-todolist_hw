<script setup>
import { v4 as uuidv4 } from "uuid"
import { ref, reactive, onBeforeMount } from "vue"
import DeviceInfo from "@/components/headers/Info.vue"
import DeviceItem from "@/components/texts/Item.vue"

const title = "TODO"
const todotext = ref("")
const todotextlist = reactive([])
const StorageKey = "ToDo-List"

const save = (key, data) => {
  localStorage.setItem(key, JSON.stringify(data))
}

const addTodo = () => {
  if (todotext.value !== "") {
    const item = {
      id: uuidv4(),
      title: todotext.value,
    }
    todotextlist.unshift(item)
    console.log(todotextlist)
    save(StorageKey, todotextlist)
    todotext.value = ""
  }
}

const removeItem = (id) => {
  const index = todotextlist.findIndex((todotext) => {
    return todotext.id === id
  })
  todotextlist.splice(index, 1)
  save(StorageKey, todotextlist)
}

onBeforeMount(() => {
  const saveTexts = JSON.parse(localStorage.getItem(StorageKey))
  todotextlist.push(...saveTexts)
})
</script>

<template>
  <main class="sm:mx-10">
    <h1 class="text-6xl py-4 font-thin select-none bg-blue-50 border-b-2 border-slate-500">{{ title }} 管理系統</h1>
    <form>
      <div>
        <br /><label class="text-3xl font-thin select-none">以下 輸入 todo 待辦事項</label><br />
        <div class="flex items-center mt-4 mb-4">
          <input
            type="text"
            placeholder="做點重要的事吧..."
            class="w-full text-2xl focus:outline-none input-lg input input-bordered"
            v-model="todotext"
          />
          <button @click.prevent="addTodo" class="text-xl btn-lg btn btn-neutral">新增</button>
        </div>
      </div>
    </form>
    <section>
      <header>
        <DeviceInfo :todotextlist="todotextlist" />
      </header>

      <ul>
        <!-- <li v-for="item in todotextlist" :key="item.id">{{ item.title }}</li> -->
        <DeviceItem @remove-auo-item="removeItem" v-for="item in todotextlist" :todotext="item"></DeviceItem>
        <!-- <DeviceItem @remove-auo-item="removeItem" v-for="d in todotextlist" :todotext="d" /> -->
      </ul>
    </section>
  </main>
</template>

<style scoped></style>
