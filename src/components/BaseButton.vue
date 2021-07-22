<template>
  <button :class="$style.button" @click="clickHandler">
    <slot>123123</slot>
  </button>
</template>

<script>
export default {
  emits: ['clicked'],

  setup(_, { emit }) {
    const clickhandler = () => {
      emit('clicked');
    };

    return {
      clickhandler,
    };
  },
};
</script>

<style module>
.button {
  display: block;
  background-color: var(--primary-green);
  font-family: inherit;
  font-size: inherit;
  font-weight: 600;
  color: var(--neutral-white);
  text-align: center;
  text-transform: uppercase;
  padding: 1rem 1.125rem;

  width: 100%;
  border: none;
  border-radius: 0.4em;
  box-shadow: 0 0.25em #30ba7e, 0 0.325em #49ae84;
  transition: all 150ms ease-out;
}

.button:hover {
  background-color: hsl(154, 73%, 59%);
  box-shadow: 0 0.25em #3ed191, 0 0.325em #5bca9c;
}

.button:active {
  transform: translateY(0.15em);
  box-shadow: 0 0.1em #3ed191, 0 0.125em #5bca9c;
}
</style>
