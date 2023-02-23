<script setup>

//defineProps(['title', 'desc', 'colorText'])

defineProps({
    title: String,
    id: Number,
    body: {
        type: String,
        default: "Sin descripcion"
    },
});

const emit = defineEmits(['cambiarFavoritoNombre'])
</script>

<template>
    <div class="card">
        <div class="card-body">
            <h5 
                class="card-title text-black"                
            >{{ id }} {{ title }}</h5>
            <p class="text-black">{{ body }}</p>
            <button 
                @click="emit('cambiarFavoritoNombre', title)" 
                class="btn btn-outline-primary"
            >Favorito</button>
        </div>
    </div>
</template>