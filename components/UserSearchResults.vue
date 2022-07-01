<template>
  <div>
    <div v-if="isLoading">
      <p>Loading users...</p>
    </div>

    <div v-else-if="Array.isArray(users) && users.length === 0">
      <span>No users found for given search!</span>
    </div>

    <div v-else-if="users !== null">
      <LayoutStack gap="xsmall">
        <div v-for="user in users" :key="user.id">
          <NuxtLink :to="'/user/' + user.login">
            {{ user.login }}
          </NuxtLink>
        </div>
      </LayoutStack>
    </div>

    <div v-else>
      <p>Start typing to search for users...</p>
    </div>
  </div>
</template>

<script setup>
let props = defineProps(["searchText"]);

let users = useState("usersSearch");
let isLoading = ref(false);

users.value = await searchUsers(props.searchText);

// We do not use watchEffect here, as this conflicts when having a search on the URL (=on initial load)
// Instead, we initialize `users.value` above, which will be skipped on client due to `useState()`.
// Then, only when it _changes_ we use `watch` to re-fetch data (incl. setting `isLoading`)
watch(props, async () => {
  isLoading.value = true;

  users.value = await searchUsers(props.searchText);

  isLoading.value = false;
});

async function searchUsers(search) {
  if (!search) {
    return null;
  }

  const { data } = await useFetch(
    `https://api.github.com/search/users?q=${encodeURIComponent(search)}`,
    { pick: ["items"] }
  );

  return data.value.items;
}
</script>

<style scoped>
.user-search {
  display: block;
  width: 100%;
  -webkit-appearance: none;
  border: 1px solid grey;
  padding: 0.25rem 0.5rem;
  border-radius: 0.25rem;
}
</style>
