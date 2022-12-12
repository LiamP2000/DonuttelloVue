<script setup>
import DonutCard from './components/DonutCard.vue'
</script>

<script>
let localUrl = "http://localhost:3000";
let remoteUrl = "https://donuttello-api.onrender.com";
let apiUrl = localUrl;

export default {
  data() {
    let jwtToken = localStorage.getItem("token")
    let loggedIn = false

    // Is jwt token in localStore?
    if(jwtToken != null){
      // don't show login screen anymore
      loggedIn = true
    }

    return {
      loggedIn: loggedIn,
      jwtToken: jwtToken
    }
  },
  methods: {
    async clickLogout(){
      // delete everything (including token) from localstore
      localStorage.clear()
      // reload page
      location.reload()
    },
    async clickLogin() {
      let loginObj = {
        username: this.$refs.username.value,
        password: this.$refs.password.value
      }

      let result = await fetch(apiUrl + "/users/login", {
        method: "POST",
        headers: {
          "Content-Type": "application/json"
        },
        body: JSON.stringify(loginObj)
      })
      let json = await result.json()

      if(json.status == "error"){
        // user/pass wrong
        alert(json.message)
        return
      }else{
        // login success
        localStorage.setItem("token", json.data)
        this.loggedIn = true
      }
    }
  }
}

// Get all donuts from API
let response = await fetch(apiUrl + "/donuts")
let json = await response.json()
let donuts = json.data
</script>

<template>
  <div class="app">
    <div v-if="!loggedIn">
      <h1>Admin login</h1>
      <label for="username">Username</label>
      <br/>
      <input type="text" ref="username" id="username" name="username" />
      
      <br/>
      <br/>

      <label for="password">Password</label>
      <br/>
      <input type="password" ref="password" id="password" name="password" />
      <br/>
      <br/>
      <button class="login__btn" @click="clickLogin">Login</button>
    </div>
    <div v-else>
      <h1>Donut orders</h1>
      <button class="login__btn" @click="clickLogout">Logout</button>
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
