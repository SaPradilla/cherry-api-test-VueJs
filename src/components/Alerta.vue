<script setup>
    import { computed } from 'vue'
    const props = defineProps({
        alerta: {
            type: Object,
            required: true
        }
    })

    const isError = computed(() => {
        return props.alerta.tipo === 'error'
    })
</script>

<template>
    <div
        :class="[isError ?  'bg-red-600' : 'bg-green-500']"
        class="text-white w-64 mt-5 mx-auto text-center p-2 uppercase font-bold  rounded-md"
    >
        {{ alerta.mensaje }}
    </div>
</template>

