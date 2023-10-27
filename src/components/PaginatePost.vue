<script setup>

defineProps(['ini', 'fin', 'maxLength'])

const emit = defineEmits(['next', 'prev'])


const activarSiguiente = () => {
    console.log("Me diste siguiente");
    emit("next");
}

</script>

<template>
    <div class="btn-group" role="group" aria-label="Basic example">
        <button 
            @click="emit('prev')" 
            type="button" 
            class="btn btn-outline-primary"
            :disabled="ini <= 0"
            >Previus

            {{ ini }}
        </button>
        <button 
            @click="activarSiguiente" 
            type="button" 
            class="btn btn-outline-primary"
            :disabled="fin >= maxLength"
            >Next

            {{ fin }}
        </button>
    </div>
</template>