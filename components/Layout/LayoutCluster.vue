<template>
  <div
    class="cluster"
    :class="{
      'cluster--gap-small': gap == 'small',
      'cluster--gap-large': gap == 'large',
      'cluster--horizontal-right': horizontalAlign == 'right',
      'cluster--horizontal-spaced': horizontalAlign == 'spaced',
      'cluster--horizontal-center': horizontalAlign == 'center',
      'cluster--vertical-top': verticalAlign == 'top',
      'cluster--vertical-bottom': verticalAlign == 'bottom',
      'cluster--vertical-stretch': verticalAlign == 'stretch',
      'cluster--full-width-on-mobile': fullWidthOnMobile,
    }"
  >
    <slot />
  </div>
</template>

<script setup>
defineProps(["gap", "horizontalAlign", "verticalAlign", "fullWidthOnMobile"]);
</script>

<style scoped>
.cluster {
  /* Defined in app.css */
  --cluster-gap-size: var(--layout-cluster-gap-size);

  --cluster-horizontal-gap: var(--cluster-gap-size);
  --cluster-vertical-gap: var(
    --cluster-vertical-gap-size,
    var(--cluster-gap-size)
  );

  display: flex;
  flex-wrap: wrap;
  align-items: center;
  gap: var(--cluster-vertical-gap) var(--cluster-horizontal-gap);
}

.cluster--gap-small {
  --cluster-gap-size: calc(var(--layout-cluster-gap-size) * 0.5);
}

.cluster--gap-large {
  --cluster-gap-size: calc(var(--layout-cluster-gap-size) * 2);
}

.cluster--horizontal-right {
  justify-content: flex-end;
}
.cluster--horizontal-spaced {
  justify-content: space-between;
}
.cluster--horizontal-center {
  justify-content: center;
}

.cluster--vertical-top {
  align-items: flex-start;
}
.cluster--vertical-bottom {
  align-items: flex-end;
}
.cluster--vertical-stretch {
  align-items: stretch;
}

@media all and (max-width: 500px) {
  .cluster--full-width-on-mobile > * {
    width: 100%;
  }
}
</style>
