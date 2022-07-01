<template>
  <div>
    <Head>
      <Title>Favorite repos</Title>
    </Head>

    <LayoutStack gap="small">
      <div v-if="repos.length === 0">No repos marked as favorite yet!</div>

      <UserDetailReposItem
        v-for="repo in repos"
        :key="repo.name"
        :repo="repo"
      />
    </LayoutStack>
  </div>
</template>

<script setup>
let favoritesStateRef = useState("favoriteRepoNames");

let repos = favoritesStateRef.value.map((name) => {
  return {
    name,
    githubUrl: `https://github.com/${name}`,
  };
});
</script>
