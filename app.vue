<template>
  <div>
    <NuxtLayout>
      <HeaderBar />

      <LayoutSiteWrapper>
        <NuxtPage />
      </LayoutSiteWrapper>
    </NuxtLayout>
  </div>
</template>

<script setup>
useHead({
  titleTemplate: (titleChunk) => {
    return titleChunk ? `${titleChunk} - Github Explorer` : "Github Explorer";
  },
});

let favorites = useCookie("favoriteRepoNames", {
  // 2 weeks in seconds
  maxAge: 60 * 60 * 24 * 2,
  default: () => [],
});

// We store this as a useState so we can easily access it everywhere
// Without having to re-define the cookie config all the time
let favoritesStateRef = useState("favoriteRepoNames");
favoritesStateRef.value = favorites;
</script>
