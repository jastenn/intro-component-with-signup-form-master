<template>
  <div class="container">
    <Header />
    <Form />
  </div>
</template>

<script>
import Header from './components/TheHeader.vue';
import Form from './components/TheForm.vue';

export default {
  name: 'App',
  components: {
    Header,
    Form,
  },
};
</script>

<style>
*,
*::before,
*::after {
  padding: 0;
  margin: 0;
  box-sizing: inherit;
}

:root {
  --clr-red: hsl(0, 100%, 74%);
  --clr-green: hsl(154, 59%, 51%);
  --clr-blue: hsl(248, 32%, 49%);
  --clr-dark-blue: hsl(249, 10%, 26%);
  --clr-grayish-blue: hsl(246, 25%, 77%);
  --clr-white: white;

  --primary-red: var(--clr-red);
  --primary-green: var(--clr-green);
  --accent: var(--clr-blue);
  --neutral-dark: var(--clr-dark-blue);
  --neutral-light: var(--clr-grayish-blue);
  --neutral-white: var(--clr-white);
}

html {
  font-size: 100%;
}

body {
  font-family: 'Poppins', sans-serif;
  font-size: 1rem;
  font-weight: 400;
  color: var(--neutral-white);

  background: var(--primary-red) url('./assets/bg-intro-desktop.png');
  box-sizing: border-box;
}

.container {
  width: 88%;
  max-width: 69.38rem;
  margin: 5.5rem auto 0 auto;
}
</style>
