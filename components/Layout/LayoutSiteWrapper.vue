<template>
  <div class="site-wrapper">
    <slot />
  </div>
</template>

<style scoped>
.site-wrapper {
  width: var(--wrapper-width);
  max-width: 100%;
  padding: 2rem;
  margin: 0 auto;
}
</style>
