<template>
  <div :class="$style.col2">
    <Pricing>
      <div>
        <span style="font-weight: 700;">Try it free 7 days </span>
        then $20/mo. thereafter
      </div>
    </Pricing>
    <form :class="$style.form" @submit="submitHandler">
      <InputText
        v-for="(input, idx) in inputForms"
        :key="idx + 1"
        :input="input"
        :vuelidate="v$"
        v-model.trim="state[input.name]"
      />
      <SubmitButton @clicked="submitHandler">
        Claim your free trial
      </SubmitButton>
      <Terms />
    </form>
  </div>
</template>

<script>
import { computed } from 'vue-demi';
import { reactive } from '@vue/reactivity';
import { useVuelidate } from '@vuelidate/core';
import {
  maxLength,
  minLength,
  required,
  email,
  alpha,
} from '@vuelidate/validators';

import Pricing from './BasePricing.vue';
import InputText from './FormTextInput.vue';
import SubmitButton from './BaseButton.vue';
import Terms from './FormTerms.vue';

import { inputForms } from '../data/inputForms';

export default {
  components: {
    Pricing,
    InputText,
    SubmitButton,
    Terms,
  },

  setup() {
    const state = reactive({
      firstName: '',
      lastName: '',
      email: '',
      password: '',
    });

    const rules = computed(() => ({
      firstName: {
        required,
        alpha,
      },
      lastName: {
        required,
        alpha,
      },
      email: {
        email,
        required,
      },
      password: {
        required,
        minLength: minLength(6),
        maxLength: maxLength(18),
      },
    }));

    const v$ = useVuelidate(rules, state);

    const submitHandler = (e) => {
      e.preventDefault();

      v$.value.$touch();
      if (v$.value.$error) return;

      console.log('Form is Valid');
      console.log(state);

      v$.value.$reset();
      state.firstName = '';
      state.lastName = '';
      state.email = '';
      state.password = '';
    };

    return { v$, state, submitHandler, inputForms };
  },
};
</script>

<style module>
.form {
  width: 100%;
  background-color: white;
  border-radius: 0.875em;
  padding: clamp(1.5rem, 5vw, 2.5rem);

  box-shadow: 0 0.5em rgba(0, 0, 0, 0.15);
}

.form > * + * {
  margin-top: 1rem;
}

@media (min-width: 51.75em) {
  .form {
    padding: clamp(1.5rem, 3vw, 2.5rem);
  }
}
</style>
