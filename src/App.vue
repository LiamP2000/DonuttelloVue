<script setup>
import DonutCard from './components/DonutCard.vue'
</script>

<script>
export default {
  data() {
    return {
      loggedIn: false
    }
  }
}
let localUrl = "http://localhost:3000/donuts/";
let remoteUrl = "https://donuttello-api.onrender.com/donuts/";
let apiUrl = localUrl;

let response = await fetch(apiUrl)
let json = await response.json()
let donuts = json.data
</script>

<template>
  <div class="app">
    <div v-if="!loggedIn">
      <h1>Admin login</h1>
      <label for="username">Username</label>
      <br/>
      <input type="text" id="username" name="username" />
      
      <br/>
      <br/>

      <label for="password">Password</label>
      <br/>
      <input type="password" id="password" name="password" />
      <br/>
      <br/>
      <button class="login__btn" @click="loggedIn = !loggedIn">Login</button>
    </div>
    <div v-else>
      <h1>Donut orders</h1>
      <div class="donut-cards">
        <DonutCard v-for="(item, index) in donuts" :donut="item" :apiUrl="apiUrl" />
      </div>
    </div>
  </div>
</template>

<style scoped>
input {
  padding: 0.1rem 0.5rem;
  border-radius: 25px;
}

.login__btn {
    border: none;
    border-radius: 40px;
    width: 5rem;
    height: 1.6rem;
	  cursor: pointer;
	  color: white;
	  color: #F7F249;
    background-color: #E72C70;
}

.app {
  font-family: 'Dosis', sans-serif;
  text-align: center;
  color: var(--primary-pink);
}

.donut-cards {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  align-items: center;
  margin: 0 auto;
  width: 100%;
  max-width: 1200px;
}
</style>
