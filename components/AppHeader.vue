<template>
  <header class="header">
    <h2 class="title">Shapes</h2>
    <ul>
      <li>
        <nuxt-link to="/"> Logout </nuxt-link>
      </li>
    </ul>
  </header>
</template>

<script>
export default {
  name: 'AppHeader',
};
</script>

<style>
.header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  /* margin-bottom: 1rem;
  padding-bottom: 1rem;
   */
   padding:0px 30px
}



.header ul {
  display: flex;
  list-style-type: none;
}

.header a {
  display: inline-block;
  padding: 0.3rem 1rem;
  padding-right: 0.5rem;
  text-decoration: none
}
</style>
