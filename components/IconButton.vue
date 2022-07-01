<template>
  <button type="button" class="icon-button">
    <slot />
  </button>
</template>

<style scoped>
.icon-button {
  display: flex;
  justify-content: center;
  align-items: center;
  -webkit-appearance: none;
  border: 0;
}
</style>
