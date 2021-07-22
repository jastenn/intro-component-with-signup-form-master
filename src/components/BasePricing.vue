<template>
  <div :class="$style.pricing">
    <slot></slot>
  </div>
</template>

<script>
export default {};
</script>

<style module>
.pricing {
  text-align: center;
  background-color: var(--accent);
  padding: 1.25em 2em;
  margin-bottom: 1em;
  border-radius: 0.875em;

  box-shadow: 0 0.4em rgba(0, 0, 0, 0.15);
}

@media (max-width: 28.125rem) {
  .pricing {
    padding: 1.25em 1em;
  }
  .pricing > * {
    max-width: 15em;
    margin: 0 auto;
  }
}
</style>
