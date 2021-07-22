<template>
  <Pricing>
    <div>
      <span style="font-weight: 700;">Try it free 7 days</span>
      then $20/mo. thereafter
    </div>
  </Pricing>

  <form :class="$style.form" @submit="submitHandler">
    <InputText
      v-for="(input, idx) in inputFields"
      :key="idx"
      :name="input.name"
      :type="input.type"
      :placeholder="input.placeholder"
      :value="input.value"
      @update:input="updateInputState"
    />
    <SubmitButton @clicked="submitHandler"
      >Claim your free trial</SubmitButton
    >
  </form>
</template>

<script>
import { ref } from '@vue/reactivity';
import { useVuelidate } from '@vuelidate/core';
import Pricing from './BasePricing.vue';
import InputText from './FormInputText.vue';
import SubmitButton from './BaseButton.vue';

export default {
  components: {
    Pricing,
    InputText,
    SubmitButton,
  },

  setup() {
    const v$ = useVuelidate();
    const state = ref({
      firstName: '',
      lastName: '',
      email: '',
      password: '',
    });

    const updateInputState = (el) => {
      state.value = {
        ...state.value,
        [el.name]: el.value,
      };
    };

    const submitHandler = (e) => {
      e.preventDefault();
      console.log(`First Name: ${state.value.firstName}`);
      console.log(`Last Name: ${state.value.lastName}`);
      console.log(`Email:  ${state.value.email}`);
      console.log(`Password: ${state.value.password}`);
    };

    return { v$, state, updateInputState, submitHandler };
  },

  data() {
    return {
      inputFields: [
        {
          name: 'firstName',
          placeholder: 'First Name',
          value: this.state.firstName,
          type: 'text',
        },
        {
          name: 'lastName',
          placeholder: 'Last Name',
          value: this.state.lastName,
          type: 'text',
        },
        {
          name: 'firstName',
          placeholder: 'Email Address',
          value: this.state.email,
          type: 'email',
        },
        {
          name: 'password',
          placeholder: 'Password',
          value: this.state.password,
          type: 'password',
        },
      ],
    };
  },
};
</script>

<style module>
.form {
  width: 100%;
  background-color: white;
  border-radius: 0.875em;
  padding: 1.5rem 1.5rem;

  box-shadow: 0 0.5em rgba(0, 0, 0, 0.15);
}

.form > * + * {
  margin-top: 1rem;
}
</style>
