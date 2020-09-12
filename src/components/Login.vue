<template>
  <div>
    <form id="login_form">
      <h1>Login</h1>
      <hr />
      <label id="icon" for="name">
        <i class="fas fa-envelope"></i>
      </label>
      <input v-model="email" type="text" name="email" id="email" placeholder="Email" required />
      <label id="icon" for="name">
        <i class="fas fa-user"></i>
      </label>
      <input
        v-model="password"
        type="password"
        name="password"
        id="password"
        placeholder="Password"
        required
      />
      <center>
        <p>
          <b
            v-show="wrongPassword"
            style="color: red"
            id="wrong_password"
          >Invalid login or password.</b>
        </p>
      </center>
      <hr />
      <div class="btn-block">
        <button id="login_submit" @click.prevent="login">Login</button>
      </div>
    </form>
  </div>
</template>

<script>
import axios from "axios";
export default {
  data() {
    return {
      email: "",
      password: "",
      wrongPassword: false,
    };
  },
  async login() {
    let response = await axios.post("http://127.0.0.1:8000/login", {
      email: this.email,
      password: this.password,
    });
    json = JSON.parse(response.data);
    if (response.status === 200) {
      if (json.code === 3003) {
        this.wrongPassword = true;
      } else {
        chrome.storage.local.set({ logged: true }, function () {
          console.log("Logged in is " + true);
        });
      }
    }
  },
};
</script>
