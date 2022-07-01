<template>
  <div
    class="stack"
    :class="{
      'stack--gap-small': gap == 'small',
      'stack--gap-xsmall': gap == 'xsmall',
      'stack--gap-large': gap == 'large',
    }"
  >
    <slot />
  </div>
</template>

<script setup>
defineProps(["gap"]);
</script>

<style scoped>
.stack {
  /* Defined in app.css */
  --stack-gap-size: var(--layout-stack-gap-size);
  display: flex;
  flex-direction: column;
  gap: var(--stack-gap-size) 0;
}

.stack--gap-xsmall {
  --stack-gap-size: calc(var(--layout-stack-gap-size) * 0.25);
}

.stack--gap-small {
  --stack-gap-size: calc(var(--layout-stack-gap-size) * 0.5);
}

.stack--gap-large {
  --stack-gap-size: calc(var(--layout-stack-gap-size) * 2);
}
</style>
