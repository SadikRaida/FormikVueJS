<script setup>
import { reactive } from 'vue'
import Formik from './components/Formik.vue';
import Field from './components/Field.vue';
import HelloWorld from './components/HelloWorld.vue';

const validate = (values) => {
    const errors = {}
    if (!values.name || !/^[a-zA-Z]+$/.test(values.name)) {
        errors.name = 'Nom pas bon'
    }
    if (!/^[A-Z0-9._%+-]+@[A-Z0-9.-]+\.[A-Z]{2,4}$/i.test(values.email)) {
        errors.email = 'format mail pas bon'
    }
    if (!values.select) {
        errors.select = 'Une couleur est nécessaire'
    }
    if (!values.textarea) {
        errors.textarea = 'Une description est nécessaire'
    }
    return errors
}

const initialValue = reactive({
    name: '',
    email: '',
    select: '',
    textarea: '',
});

const onSubmit = (val) => {
    result.value = val.value;
};



const result = reactive({});

</script>

<template>
  <header>
    <div class="wrapper">
      <Formik
        :initialValues="initialValue"
        :onSubmit="onSubmit"
        :validate="validate"
      >
        <template #default="{ errors, handleSubmit, isSubmitting }">
          <form @submit.prevent="handleSubmit">
            <p>Nom</p>
            <Field
              as="input"
              name="name"
              />
              <p>Mail</p>
              <Field
                as="input"
                name="email"
              />
              <p>Choisir une couleur</p>
              <Field name="select" as="select">
            <option value="bleu">bleu</option>
            <option value="blanc">blanc</option>
            <option value="rouge">rouge</option>
            <option value="vert">vert</option>
            <option value="jaune">jaune</option>
            </Field>

            <p> Décrivez-vous </p>
            <Field name="textarea" as="textarea" />
  
          
            
            <button 
            type="submit" 
            :disabled="isSubmitting">
            Submit
          </button>

          <div v-if="errors" >
            <div id="errResponse" v-for="(error, key) in errors" :key="key">
              
              {{ error }}

            </div>
            
          </div>
          <div v-if="result">
            <div id="response" v-for="(value, key) in result" :key="key">
              {{ value }}
            </div>
          </div>
          </form>
        </template>
      </Formik>

    </div>
  </header>


</template>

<style>
.wrapper {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
  background-color: #100202f0;
}

body {
  background-color: #4d38ec !important;
}




form {
  display: flex;
  flex-direction: column;
  width: 400px;
  padding: 20px;
  background-color: rgb(255, 255, 255);
  border-radius: 20px;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
}

form p {
  margin: 0;
  margin-bottom: 5px;
  font-size: 14px;
  color: black;
}

#response {
  color: green;
}

#errResponse {
  color: red;
}

</style>