<template>
  <div id="logged_page">
    <h1>Logged in.</h1>
    <div class="righttopcorner" @click.prevent="logout">
      <a id="logout_button">
        <img src="../assets/logout48.png" />
      </a>
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  name: "LoggedPage",
  methods: {
    async logout() {
      let response = await axios.get("http://127.0.0.1:8000/logout");
      let json = JSON.parse(response.data);
      if (response.status === 200) {
        console.log(response.data);
        chrome.storage.local.set({ logged: false }, function () {
          console.log("Logged in is " + false);
        });
      }
    },
  },
};
</script>

<style>
</style>