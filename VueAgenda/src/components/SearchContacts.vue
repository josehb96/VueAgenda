<script setup>

    // imports
    import { reactive, ref } from 'vue'
    
    //
    import { useListContacts } from '../composables/useListContacts';

    // emits
    const emit = defineEmits(['filterContact'])    

    // states
    const bgBtn = ref('blue') 
    const stylesBtn = reactive({
        background: 'blue',
        color: 'blank'
    })

    const kword = ref('') 

    // composables
    // De esta forma ya podemos utilizar en este componente la variable y la función definidas en el composable 
    const { msjEmpy, showEmpy } = useListContacts() // Se crea una copia sólamente para el ámbito de este componente

    // methods 
    const isFocus = () => {
        // bgBtn.value = 'red'
        stylesBtn.background = 'grey'
        stylesBtn.color = 'white'
    }

    const filtrarDatos = () => {
        showEmpy('Pruebe otra palabra')
        emit('filterContact', kword.value) 
    }     

</script>

<template>
    <div class="flex items-center">
        <input 
            type="text" 
            class="block flex-1 border-0 bg-white py-1.5 pl-1 text-gray-900 placeholder:text-gray-400 focus:ring-0 sm:text-sm sm:leading-6" 
            placeholder="buscar.."
            @focus="isFocus"
            @input="filtrarDatos"
            v-model="kword"> <!-- Enviamos un parámetro a través del emit en la línea de arriba -->
        <button 
            class="bg-blue-500 py-1.5 px-5" 
            :style="stylesBtn"
            @click="$emit('searchContacts')"
        >Buscar</button>
    </div>
    <p class="text-red-500">{{ msjEmpy }}</p>
</template>