<script setup>
import { ref } from 'vue'

defineEmits(['hola', 'adios']);

const props = defineProps({
    titulo: String,
    valorInicial: {
        type: Number,
        default: 0
    }
})
const count = ref(props.valorInicial);
</script>
<template>
    <h1>{{ titulo ?? 'titulo por defecto' }}</h1>
   <button @click="count++">You clicked me {{ count }} times.</button>
  <button @click="$emit('hola')">Hola</button>
</template>