<template>
    <slot 
        :values="values" 
        :errors="errors" 
        :handleSubmit="handleSubmit" 
        :isSubmitting="isSubmitting">
    </slot>
</template>




<script setup>
import { ref, reactive, provide } from 'vue';

const props = defineProps({
    initialValues: {
        type: Object,
        required: true
    },
    onSubmit: {
        type: Function,
        required: true
    },
    validate: {
        type: Function,
        required: true
    }
});

const isSubmitting = ref(false);
const errors = reactive({});
const values = ref(props.initialValues);

const handleSubmit = (e) => {
    e.preventDefault()
    const formValues = values.value;
    const err = props.validate(formValues);
    
    if (Object.keys(err).length === 0) {
        props.onSubmit(values);
    } else {
        errors.value = err;
    }
}



provide('values', values);
</script>

