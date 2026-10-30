<template>
  <div class="center-wrapper">
   
<nav>

<button @click="menu = !menu">
  Menu ☰
</button>



<ul v-if="menu">
 <li> <router-link to="/">Rynek krypto</router-link> </li>
<li><router-link to="/partnership">Usługi</router-link> </li>
 <li><router-link to="/contact">Kontakt</router-link> </li>
 <li><router-link to="/form">Formularz</router-link></li>
</ul>

</nav>
</div>

</template>

<script setup lang="ts">
import {ref} from 'vue'

const menu = ref(false)



</script>

<style lang="scss" scoped>
.center-wrapper {
  display:flex;
  justify-content: start;
  position: relative;
  text-decoration: none;

}

button {
  background-color: white;
  border: 0.5px solid black;

}

nav {
background-color: #ffffff;
box-shadow: 2px -2px 50px rgba(0,0,0,0.1);
padding: 10px;
  width: 100%;

}

nav > ul  {
  list-style-type: none;
  font-size: 17px;
}
a:visited {
 text-decoration: none;
 color: black;
}



</style>