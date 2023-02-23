<script setup>

 defineProps({
    inicio: Number,
    fin: Number,
    maxLength: Number
 })

const emit = defineEmits(['next', 'prev'])
</script>

<template>
    <div class="btn-group" role="group">
        <button 
            type="button" 
            @click="emit('prev')" 
            class="btn btn-primary"
            :disabled="inicio <= 0"
        >Anterior</button>
        <button 
            type="button" 
            @click="emit('next')" 
            class="btn btn-primary"
            :disabled="fin >= maxLength"
        >Siguiente</button>
    </div>
</template>