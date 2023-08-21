<script setup>
import { ref } from "vue";
import { RouterLink, RouterView } from 'vue-router'
import HelloWorld from './components/HelloWorld.vue'

const message = ref('Does not request yet');

const RequestToBackEnd = () => {
  console.warn("バックエンドにリクエストを送ります")
  fetch('http://127.0.0.1:5000') //バックエンドのURL,エンドポイントを指定
    .then((response) => {
      console.log(response)
      return response.json();
    }).then((data) => {
      console.log(data)
      message.value = data.message;
    }).catch((error) => {
      console.error(error);
    })
}

</script>

<template>
  <header>
    <img alt="Vue logo" class="logo" src="@/assets/logo.svg" width="125" height="125" />

    <div class="wrapper">
      <HelloWorld msg="FUCK YOU" />

      <nav>
        <RouterLink to="/">うんこ</RouterLink>
        <RouterLink to="/about">Poop</RouterLink>
      </nav>
    </div>
  </header>
  <div id="FlaskTestArea">
    <h1>Flask Test Area</h1>
    <p>{{ message }}</p>
    <button @click="RequestToBackEnd()">Request to my backend env</button>
  </div>

  <!--<RouterView />-->
</template>

<style scoped>
header {
  line-height: 1.5;
  max-height: 100vh;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

nav {
  width: 100%;
  font-size: 12px;
  text-align: center;
  margin-top: 2rem;
}

nav a.router-link-exact-active {
  color: var(--color-text);
}

nav a.router-link-exact-active:hover {
  background-color: transparent;
}

nav a {
  display: inline-block;
  padding: 0 1rem;
  border-left: 1px solid var(--color-border);
}

nav a:first-of-type {
  border: 0;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }

  nav {
    text-align: left;
    margin-left: -1rem;
    font-size: 1rem;

    padding: 1rem 0;
    margin-top: 1rem;
  }
}
</style>
