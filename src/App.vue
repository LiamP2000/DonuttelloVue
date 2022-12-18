<script setup>
import { isFunctionType } from '@vue/compiler-core';
import DonutCard from './components/DonutCard.vue'
</script>

<script>
let localUrl = "http://localhost:3000";
let remoteUrl = "https://donuttello-api.onrender.com";
let apiUrl = remoteUrl;

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
      showChangePasswordBox: false,
      loggedIn: loggedIn,
      jwtToken: jwtToken,
      donuts: [],
    }
  },
  async created() {
    // Get all donuts from API
    let response = await fetch(apiUrl + "/donuts")
    let json = await response.json()
    this.donuts = json.data
  },
  methods: {
    clickChangePassword () {
      if(this.showChangePasswordBox){
        this.showChangePasswordBox = false;
      }else{
        this.showChangePasswordBox = true;
      }
    },
    async clickLogout(){
      // delete everything (including token) from localstore
      localStorage.clear()
      // reload page
      location.reload()
    },
    async clickSavePassword() {
      // http://localhost:3000/users/changePassword
      let jwtToken = localStorage.getItem("token")
      let passwordObj = {
          oldPassword: this.$refs.oldPassword.value,
          newPassword: this.$refs.newPassword.value,
          confirmPassword: this.$refs.confirmPassword.value
      }

      let result = await fetch(apiUrl + "/users/changePassword", {
        method: "PUT",
        headers: {
          "Content-type": "application/json",
          "Authorization": jwtToken
        },
        body: JSON.stringify(passwordObj)
      })
      let json = await result.json()

      if(json.status == "success"){
        this.showChangePasswordBox = false
      }else{
        this.$refs.changePasswordError.innerText = json.message
      }
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
        this.$refs.wrongLogin.innerText = json.message
        return
      }else{
        // login success
        localStorage.setItem("token", json.data)
        this.loggedIn = true
      }
    }
  }
}
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
      <p class="span__error" ref="wrongLogin"></p>
      <button class="btn login__btn" @click="clickLogin">Login</button>
    </div>
    <div v-else>
      <h1>Donut orders</h1>
      <div v-if='showChangePasswordBox'>
        <label class="pw__label" for="oldPassword">Old Password</label>
        <input type="password" id="oldPassword" name="oldPassword" ref="oldPassword" />
        <br/>
        <label class="pw__label" for="newPassword">New Password</label>
        <input type="password" id="newPassword" name="newPassword" ref="newPassword" />
        <br/>
        <label class="pw__label" for="confirmPassword">Confirm Password</label>
        <input type="password" id="confirmPassword" name="confirmPassword" ref="confirmPassword" />
        <p class="span__error" ref="changePasswordError"></p>
        <br/>
        <button class="btn change_password__btn" @click="clickSavePassword">Save</button>
      </div>
      <button class="btn password__btn" @click="clickChangePassword">Change password</button>
      <button class="btn login__btn" @click="clickLogout">Logout</button>
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
.span__error {
  color: red;
}

.pw__label {
  margin-right: 20px;
}

.change_password__btn {
  width: 5rem;
  margin: 20px;
}

.btn {
  border: none;
  border-radius: 40px;
  width: 5rem;
  height: 1.6rem;
  cursor: pointer;
  color: white;
  color: #F7F249;
  background-color: #E72C70;
}

.login__btn {
    width: 5rem;
}

.password__btn {
    width: 10rem;
    margin-right: 20px;
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
