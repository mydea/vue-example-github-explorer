<template>
  <header>
    <nav>
      <ul class="main-nav">
        <li>
          <NuxtLink to="/">User search</NuxtLink>
        </li>
        <li>
          <NuxtLink to="/favorites">Favorite repos</NuxtLink>
        </li>
      </ul>
    </nav>
  </header>
</template>

<style scoped>
header {
  width: 100%;
  background-color: var(--color-primary);
  color: #fff;
}

.main-nav {
  display: flex;
  gap: 0.25rem 2rem;
  padding: 1rem 2rem;
  list-style: none;
  margin: 0 auto;
  width: var(--wrapper-width);
  max-width: 100%;
}

.main-nav a {
  display: block;
  color: #fff;
  font-weight: bold;
  font-size: 1.25rem;
  text-underline-offset: 0.25em;
}
</style>
