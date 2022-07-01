<template>
  <div>
    <div v-if="repos != null">
      <LayoutStack gap="small">
        <UserDetailReposItem
          v-for="repo in repos"
          :key="repo.name"
          :repo="repo"
        />
      </LayoutStack>
    </div>
  </div>
</template>

<script setup>
let props = defineProps(["reposUrl"]);

let repos = useState("repos");

let { data } = await useFetch(props.reposUrl);

if (data.value) {
  repos.value = data.value.map((item) => {
    let { full_name: name, html_url: githubUrl } = item;

    return { name, githubUrl };
  });
}
</script>
