<template>
  <div :class="$style.error">
    <IconError :class="$style.errorIcon" />
    <i :class="$style.errorText" v-for="(error, idx) in errors" :key="idx">
      {{ error.$message }}
    </i>
  </div>
</template>

<script>
import IconError from './icon/IconError.vue';

export default {
  props: {
    errors: {
      type: Array,
      required: true,
    },
  },

  components: {
    IconError,
  },
};
</script>

<style module>
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
