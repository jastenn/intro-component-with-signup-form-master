<template>
  <div class="container">
    <Header />
    <Form />
  </div>
  <Attribution />
</template>

<script>
import Header from './components/TheHeader.vue';
import Form from './components/Form.vue';
import Attribution from './components/Attribution.vue';

export default {
  name: 'App',
  components: {
    Header,
    Form,
    Attribution,
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

  background: var(--primary-red) url('./assets/bg-intro-mobile.png') center;
  box-sizing: border-box;
}

.container {
  width: 88%;
  max-width: 69.38rem;
  margin: 5.5rem auto 3rem auto;
}

@media (min-width: 51.75em) {
  body {
    background-image: url('./assets/bg-intro-desktop.png');
  }
  .container {
    display: flex;
    justify-content: space-between;
    align-items: center;
  }
  .container > * {
    width: 48%;
  }
}
</style>
