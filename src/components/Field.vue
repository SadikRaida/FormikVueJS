<template>
    <p>
    <component 
    :is="as" 
    v-if="(typeof props.as === 'string')" 
    @input="values[props.name] = $event.target.value">
        
    <slot></slot>
    </component>
    <component 
    :is="as" 
    v-else v-model="values[props.name]">
        <slot></slot>
    </component>
</p>
</template>



<script setup>
import { inject } from 'vue'

const props = defineProps({
    name: {
        type: String,
        required: true
    },
    as: {
        type: String || Object,
        default: 'input',
        required: true,
    },
})

const values = inject('values');


</script>



