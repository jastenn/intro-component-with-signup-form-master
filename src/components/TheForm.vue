<template>
  <Pricing>
    <div>
      <span style="font-weight: 700;">Try it free 7 days</span>
      then $20/mo. thereafter
    </div>
  </Pricing>

  <form :class="$style.form" @submit="submitHandler">
    <div
      :class="$style.formControl"
      v-for="(input, idx) in inputFields"
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

    <SubmitButton @clicked="submitHandler">Claim your free trial</SubmitButton>
  </form>
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
      console.log(v$.value);
      v$.value.$touch();
      e.preventDefault();
    };

    return { v$, state, submitHandler };
  },

  data() {
    return {
      inputFields: [
        {
          name: 'firstName',
          placeholder: 'First Name',
          type: 'text',
        },
        {
          name: 'lastName',
          placeholder: 'Last Name',
          type: 'text',
        },
        {
          name: 'email',
          placeholder: 'Email Address',
          type: 'text',
        },
        {
          name: 'password',
          placeholder: 'Password',
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
  border: 1px solid var(--neutral-dark);
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
</style>
