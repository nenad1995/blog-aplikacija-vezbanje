<template>
  <div name="app">
    <nav>
      <h3>Navbar</h3>
      <ul>
        <li>
          <router-link :to="{ name: 'posts' }">
            Postovi
          </router-link>
        </li>
        <li>
          <router-link :to="{ name: 'add' }">
            Dodaj Post
          </router-link>
        </li>
      </ul>
    </nav>
    <router-view />
  </div>
</template>

<script>
export default {
  name: 'app',
  components: {}
}
</script>
