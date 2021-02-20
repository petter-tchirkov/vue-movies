<template>
  <header class="header">
    <router-link to="/">
      <h1><span>Vue</span>Movies</h1>
    </router-link>
  </header>
  <main class="main">
    <router-view />
  </main>
</template>

<style lang="scss">
* {
  padding: 0;
  margin: 0;
  box-sizing: border-box;
  font-family: "Fira Sans", sans-serif;
  &::selection {
    background: transparentize (#42b883, 0.5);
  }
}
body {
  background-color: #35495e;
}
a {
  text-decoration: none;
}
header.header {
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 15px 16px;
  background-color: #2c3d4e;
  box-shadow: 0 0 6px rgba(0, 0, 0, 0.1);
  h1 {
    color: #fff;
    font-size: 28px;
    font-weight: 700;
    span {
      color: #42b883;
    }
  }
}
</style>
