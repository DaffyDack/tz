<template>
  <div v-if="rows.length > 0">
    <div>
      <MyInput class="w-full max-w-md" @search="searchModal" />
    </div>
    <label><input type="checkbox" @click="allSelect(sl)" :checked="sl" v-model="sl" class="mr-2 ml-2">Список карт {{
      rows.length }}</label>
    <div class="list">
      <div>
        <draggable :value="rows" tag="ul" class="w-full max-w-md" ghost-class="moving-card" :list="rows" :animation="200">
          <template #item="{ element: meal }">
            <li>
              <transition-group name="user-list">
                <div class="post" :key="meal.id">
                  <label><input type="checkbox" v-modal="selcted" :checked="meal.default"></label>
                  <div>
                    <div><strong>Название:</strong> {{ meal.id }}</div>
                    <div><strong>Описание:</strong> {{ meal.name }}</div>
                  </div>
                  <div class="post__btns">
                    <button @click="editTodo(meal.id)"
                      class="mr-2 flex items-center justify-center rounded-lg bg-blue-700 px-4 py-2 text-sm font-medium text-white hover:bg-blue-800 focus:outline-none focus:ring-4 focus:ring-green-300 dark:bg-green-600 dark:hover:bg-green-700 dark:focus:ring-green-800">
                      Edit
                    </button>
                  </div>
                </div>
              </transition-group>
            </li>
          </template>
        </draggable>
      </div>
      <div>
        <MyMaps/>
      </div>
    </div>
  </div>
  <h2 v-else style="color: red">
    Список карт пуст
  </h2>
</template>

<script setup>
import { ref, computed } from 'vue';
import MyInput from './MyInput.vue'
import MyMaps from './MyMaps.vue'
import draggable from 'vuedraggable';

const sl = true
const emit = defineEmits(['edit', 'delete', 'select', 'search'])

const { rows } = defineProps({
  rows: {
    type: Array,
    required: true
  },
})
const tests = computed(() => {
  return rows.length > 3 ? 'test' : 'no test'
})
const searchModal = (val) => {
  console.log(val)
}
const editTodo = (todoId) => {
  emit('edit', todoId)
}

const allSelect = (id) => {
  emit('select', id)
}

const deleteTodo = (todoId) => {
  emit('delete', todoId)
}

</script>
<style>
.test {
  width: 100px;
  height: 20px;
  border: 1px solid #000;
}

.post {
  padding: 15px;
  border: 2px solid teal;
  margin-top: 15px;
  display: flex;
  align-items: center;
  justify-content: space-between;
}

.post__btns {
  display: flex;
}

.list {
  display: flex;
  flex-wrap: nowrap;
}
</style>
