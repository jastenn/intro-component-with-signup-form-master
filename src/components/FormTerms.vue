<template>
  <p :class="$style.helperText">
    By clicking the button, you are agreeing to our
    <a href="#"> Terms and Services</a>
  </p>
</template>

<style module>
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
</style>
