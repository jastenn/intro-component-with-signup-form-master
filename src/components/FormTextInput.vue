<template>
  <div :class="$style.formControl">
    <input
      :class="[errors.length ? $style.invalid : '', $style.input]"
      :name="input.name"
      :type="input.type"
      :placeholder="input.placeholder"
      :value="modelValue"
      @input="inputHandler"
    />
    <InputError v-if="isInvalid" :errors="errors" />
  </div>
</template>

<script>
import { computed } from 'vue-demi';
import InputError from './FormTextInputError.vue';

export default {
  props: {
    input: {
      type: Object,
      required: true,
    },
    vuelidate: {
      required: true,
    },
    modelValue: {
      type: String,
      required: true,
    },
  },
  components: { InputError },
  setup(props, { emit }) {
    const errors = computed(() => props.vuelidate[props.input.name].$errors);
    const isInvalid = computed(() => props.vuelidate[props.input.name].$error);

    const inputHandler = (e) => {
      const {
        vuelidate,
        input: { name },
      } = props;
      const el = e.target;

      emit('update:modelValue', el.value);
      vuelidate[name].$reset();
    };
    return { inputHandler, errors, isInvalid };
  },
};
</script>

<style module>
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

.input.invalid,
.input.invalid::placeholder {
  color: var(--primary-red);
}

.formControl {
  position: relative;
}
</style>
