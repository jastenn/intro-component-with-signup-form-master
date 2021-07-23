<template>
  <div :class="$style.col2">
    <Pricing>
      <div>
        <span style="font-weight: 700;">Try it free 7 days </span>
        then $20/mo. thereafter
      </div>
    </Pricing>
    <form :class="$style.form" @submit="submitHandler">
      <div
        :class="$style.formControl"
        v-for="(input, idx) in inputForms"
        :key="idx + 1"
      >
        <input
          :class="$style.input"
          :name="input.name"
          :type="input.type"
          :placeholder="input.placeholder"
          v-model="state[input.name]"
          @input="v$[input.name].$reset()"
        />
        <div :class="$style.error" v-if="v$[input.name].$error">
          <IconError :class="$style.errorIcon" />
          <i
            :class="$style.errorText"
            v-for="(error, idx) in v$[input.name].$errors"
            :key="idx * 51"
          >
            {{ error.$message }}
          </i>
        </div>
      </div>
      <SubmitButton @clicked="submitHandler"
        >Claim your free trial</SubmitButton
      >
      <p :class="$style.helperText">
        By clicking the button, you are agreeing to our
        <a href="#"> Terms and Services</a>
      </p>
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
import SubmitButton from './BaseButton.vue';
import IconError from './icon/IconError.vue';

import { inputForms } from '../data/inputForms';

export default {
  components: {
    Pricing,
    SubmitButton,
    IconError,
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

.input {
  display: block;
  padding: 1rem 1.125rem;
  width: 100%;
  border-radius: 0.4em;
  border: 1px solid rgba(0, 0, 0, 0.2);
  caret-color: var(--accent);

  font-family: inherit;
  font-size: inherit;
  font-weight: 600;
}

.input:focus {
  outline: none;
  border: 1px solid var(--accent);
}

.formControl {
  position: relative;
}

.error {
  margin: 0;
  padding: 0;
  display: flex;
}

.errorIcon {
  position: absolute;
  right: 1rem;
  top: 50%;
  transform: translateY(-87%);
}

.errorText {
  color: var(--primary-red);
  font-weight: 500;
  font-size: 0.687rem;
  margin-left: auto;
}

.helperText {
  color: var(--neutral-light);
  font-size: 0.6875rem;
  text-align: center;
  width: 80%;
  margin: 1.5em auto 0 auto;
}

.helperText > a {
  font-weight: 700;
  color: var(--primary-red);
  text-decoration: none;
}

@media (min-width: 51.75em) {
  .form {
    padding: clamp(1.5rem, 3vw, 2.5rem);
  }
}
</style>
