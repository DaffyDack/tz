<template>
    <!-- <input :value="modelValue" @input="updateInput" class="input" type="text"> -->
    <input @input="updateInput" class="input" type="text">
</template>
  
<script setup>
import { ref, onMounted } from 'vue'
const emit = defineEmits(['search'])

const updateInput = (event) => {
    emit('search', event.target.value)
}


</script>
  
<style scoped>
.input {
    width: 100%;
    border: 1px solid teal;
    padding: 10px 15px;
    margin-top: 15px;
}
</style>