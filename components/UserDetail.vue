<template>
  <div>
    <div v-if="errorMessage">
      An error ocurred when loading the user: {{ errorMessage }}
    </div>
    <div v-else-if="user">
      <Head>
        <Title>User: {{ user.login }}</Title>
      </Head>

      <LayoutStack gap="large">
        <div>
          <LayoutCluster gap="large">
            <div>
              <img :src="user.avatarUrl" alt="" class="avatar-image" />
            </div>

            <div>
              <LayoutStack>
                <div>
                  {{ user.login }}

                  <span v-if="user.name"> ({{ user.name }}) </span>
                </div>

                <div v-if="user.bio">
                  <p>
                    {{ user.bio }}
                  </p>
                </div>

                <div>
                  <a :href="user.githubUrl">View on GitHub</a>
                </div>
              </LayoutStack>
            </div>
          </LayoutCluster>
        </div>

        <div>
          <UserDetailRepos :user-name="userName" :repos-url="user.reposUrl" />
        </div>
      </LayoutStack>
    </div>
  </div>
</template>

<script setup>
let props = defineProps(["userName"]);

let user = useState("userDetails");
let errorMessage = useState("userErrorMessage");

let { data, error } = await useFetch(
  `https://api.github.com/users/${props.userName}`,
  {
    pick: ["avatar_url", "name", "login", "repos_url", "html_url", "bio"],
  }
);

// For whatever reason, error becomes `true` after hydration on the client??
// Actually, error handling should be added to all `useFetch` usages, but for simplicity this is an example
// By storing the error message in `useState` we circumvent the error message from SSR to become `true` on client
if (error.value && !errorMessage.value) {
  errorMessage.value = error.value.toString();
} else if (data.value) {
  let {
    avatar_url: avatarUrl,
    name,
    login,
    repos_url: reposUrl,
    html_url: githubUrl,
    bio,
  } = data.value;

  user.value = { avatarUrl, name, login, reposUrl, githubUrl, bio };
}
</script>

<style scoped>
.avatar-image {
  display: block;
  width: 15rem;
  height: auto;
  border-radius: 50%;
}
</style>
