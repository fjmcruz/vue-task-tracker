<template>
  <footer>
    <p>Copyright @2022</p>
    <router-link to="/about">About</router-link>
  </footer>
</template>

<script>
export default {
  name: "FooterComponent",
};
</script>

<style scoped>
a {
  color: #333;
}

footer {
  margin-top: 20px;
  text-align: center;
}
</style>
