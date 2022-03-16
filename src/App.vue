<template>
  <form @submit="mySubmit">
    <div>
      <input v-model="usernameValue" type="text" placeholder="Prénom" />
    </div>
    <button>Envoi</button>
  </form>
</template>

<script setup lang="ts">
import { useField, useForm } from 'vee-validate';
import { z } from 'zod';
import { toFieldValidator } from '@vee-validate/zod';

const { handleSubmit } = useForm();

const mySubmit = handleSubmit(
  (values, actions) => {
    console.log(values);
  },
  (errors) => {
    console.log(errors);
  }
);

const { value: usernameValue, errorMessage } = useField(
  'username',
  toFieldValidator(z.string().min(5, { message: 'Trop court !' }))
);
</script>

<style scoped lang="scss"></style>
