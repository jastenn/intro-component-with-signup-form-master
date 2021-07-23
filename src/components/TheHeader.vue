<template>
  <header :class="$style.header">
    <h1 :class="$style.primaryHeader">
      Learn to code by watching others
    </h1>
    <p :class="$style.subHeader">
      See how experienced developers solve problems in real-time. Watching
      scripted tutorials is great, but understanding how developers think is
      invaluable.
    </p>
  </header>
</template>

<style module>
.header {
  text-align: center;
  margin-bottom: 3.75rem;
}
.primaryHeader {
  font-size: clamp(1.75rem, 6vw, 3.13rem);
  font-weight: 700;
  margin-bottom: 1.38rem;
}
.subHeader {
  font-size: 1rem;
  font-weight: 400;
}

@media (min-width: 51.75em) {
  .header {
    text-align: unset;
  }
}
</style>
