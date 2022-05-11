<template>
  <nav id="nav">
    <router-link to="/" id="logo-url">
      <img :src="logo" :alt="alt" id="logo" />
    </router-link>

    <router-link to="/">Home </router-link>
    <router-link to="/Pedidos">Pedidos </router-link>
  </nav>
</template>

<script>
export default {
  name: "NavbarApp",

  props: ["logo", "alt"],
};
</script>

<style scoped>
#nav {
  height: 10vh;
  background-color: var(--dark-color);
  border-bottom: 4px solid #111;
  padding: 15px 50px;
  display: flex;
  justify-content: flex-end;
  align-items: center;
}

#nav #logo-url {
  margin: auto;
  margin-left: 0;
}

#logo {
  width: 40px;
  height: 40px;
}

#nav a {
  color: var(--first-color);
  text-decoration: none;
  margin: 12px;
  transition: 0.5s;
}

#nav a:hover {
  color: #fff;
}
</style>