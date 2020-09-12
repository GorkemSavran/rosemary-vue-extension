<template>
  <form id="register_form">
    <h1>Registration</h1>
    <hr />
    <!-- <div class="account-type">
          <input type="radio" value="none" id="radioOne" name="account" checked/>
          <label for="radioOne" class="radio">Personal</label>
          <input type="radio" value="none" id="radioTwo" name="account" />
          <label for="radioTwo" class="radio">Company</label>
        </div>
    <hr>-->
    <center>
      <p>
        <b v-show="userExist" style="color: red" id="user_exist">User already exists.</b>
      </p>
    </center>
    <label id="icon" for="name">
      <i class="fas fa-envelope"></i>
    </label>
    <input v-model="email" type="text" name="email" id="email" placeholder="Email" required />
    <label id="icon" for="name">
      <i class="fas fa-user"></i>
    </label>
    <input v-model="name" type="text" name="name" id="name" placeholder="Name" required />
    <label id="icon" for="name">
      <i class="fas fa-unlock-alt"></i>
    </label>
    <input
      v-model="password"
      type="password"
      name="password"
      id="password"
      placeholder="Password"
      required
    />
    <hr />
    <!-- <div class="gender">
          <input type="radio" value="none" id="male" name="gender" checked/>
          <label for="male" class="radio">Male</label>
          <input type="radio" value="none" id="female" name="gender" />
          <label for="female" class="radio">Female</label>
        </div>
    <hr>-->
    <div class="btn-block">
      <p>
        By clicking Register, you agree on our
        <a href>Privacy Policy</a>.
      </p>
      <!-- <button id="register_submit" type="submit">Register</button> -->
      <button id="register_submit" @click.prevent="register">Register</button>
    </div>
  </form>
</template>

<script>
import axios from "axios";
export default {
  name: "Register",
  data() {
    return {
      name: "",
      email: "",
      password: "",
      userExist: false,
    };
  },
  methods: {
    async register() {
      let response = await axios.post("http://127.0.0.1:8000/register", {
        email: this.email,
        password: this.password,
      });
      json = JSON.parse(response.data);
      if (response.status === 200) {
        if (json.code === 3033) {
          this.userExist = true;
        } else {
          chrome.storage.local.set({ logged: true }, function () {
            console.log("Logged in is " + true);
          });
        }
      }
    },
  },
};
</script>

<style>
</style>