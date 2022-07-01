<template>
  <div>
    <LayoutStack>
      <form @submit="submitForm">
        <label for="user-search">Search for Github username:</label>
        <input
          type="search"
          class="user-search"
          name="user-search"
          :value="searchText"
          @input="onType"
        />
      </form>

      <UserSearchResults :search-text="searchText" />
    </LayoutStack>
  </div>
</template>

<script setup>
// We store the search text in the URL, to make this persist on reload
let searchText = ref(useRoute().query.searchText || null);

let timeout;

function onType(event) {
  let search = event.target.value;

  if (timeout) {
    clearTimeout(timeout);
  }

  // debounce this to ensure we do not call this too often, while typing
  timeout = setTimeout(() => {
    searchText.value = search;

    // Put the search on the URL
    useRouter().replace({ query: { searchText: search } });
  }, 500);
}

async function submitForm(event) {
  event.preventDefault();
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
