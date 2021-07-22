<template>
  <input :class="$style.input" @keyup="inputHandler" />
</template>

<script>
export default {
  setup(props, { emit }) {
    const inputHandler = (e) => {
      const el = e.target;
      console.log(el.value);
      emit(`update:input`, el);
    };
    return {
      inputHandler,
    };
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
  border: 1px solid var(--neutral-dark);
}
</style>
