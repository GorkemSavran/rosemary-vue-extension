<template>
  <div>
    <div class="lefttopcorner">
      <img src="../assets/icon96.png" />
    </div>
    <div class="main-block">
      <login v-if="!loggedIn" v-show="formSwitch"></login>
      <register v-if="!loggedIn" v-show="!formSwitch"></register>
      <center>
        <a id="switchForm" href="#" @click="switchForms">
          <p v-show="!formSwitch">Already member? Login now!</p>
          <p v-show="formSwitch">Not yet a member? Register now!</p>
        </a>
      </center>
    </div>
    <logged-page v-if="loggedIn"></logged-page>

    <center>
      <h1 id="report"></h1>
    </center>
  </div>
</template>

<script>
import Login from "@/components/Login.vue";
import LoggedPage from "@/components/LoggedPage.vue";
import Register from "@/components/Register.vue";

export default {
  name: "App",
  components: { Login, LoggedPage, Register },
  data() {
    return {
      loggedIn: null,
      formSwitch: true,
    };
  },
  methods: {
    switchForms() {
      this.formSwitch = !this.formSwitch;
    },
    checkLoggedIn() {
      try {
        chrome.storage.local.get(["logged"], function (items) {
          console.log("logged is +++ " + items["logged"]);
          return items["logged"];
        });
      } catch (err) {
        console.log("logged is ++ " + false);
        return false;
      }
    },
  },
  mounted() {
    this.checkLoggedIn();
    console.log("hey logged is " + logged);
  },
};
</script>

<style>
@import url(https://fonts.googleapis.com/css?family=Lato:100);

body {
  /* height: 100%; */
  width: 500px;
}
html,
body {
  display: flex;
  justify-content: center;
  height: 100%;
  background-color: #121212;
}
body,
div,
h1,
form,
input,
p {
  padding: 0;
  margin: 0;
  outline: none;
  font-family: "Lato";
  font-size: 16px;
  font-weight: 900;

  color: #666;
}
h1 {
  padding: 10px 0;
  font-size: 32px;
  font-weight: bolder;
  text-align: center;
}
p {
  font-size: 12px;
}
hr {
  color: #666;
  opacity: 0.3;
}
.main-block {
  max-width: 340px;
  min-height: 460px;
  padding: 10px 0;
  margin: auto;
  border-radius: 5px;
  border: solid 1px #ccc;
  box-shadow: 1px 2px 5px rgba(0, 0, 0, 0.31);
  background: #fff;
}
form {
  margin: 0 30px;
}
.account-type,
.gender {
  margin: 15px 0;
}
input[type="radio"] {
  display: none;
}
label#icon {
  margin: 0;
  border-radius: 5px 0 0 5px;
}
label.radio {
  position: relative;
  display: inline-block;
  padding-top: 4px;
  margin-right: 20px;
  text-indent: 30px;
  overflow: visible;
  cursor: pointer;
}
label.radio:before {
  content: "";
  position: absolute;
  top: 2px;
  left: 0;
  width: 20px;
  height: 20px;
  border-radius: 50%;
  background: salmon;
}
label.radio:after {
  content: "";
  position: absolute;
  width: 9px;
  height: 4px;
  top: 8px;
  left: 4px;
  border: 3px solid #fff;
  border-top: none;
  border-right: none;
  transform: rotate(-45deg);
  opacity: 0;
}
input[type="radio"]:checked + label:after {
  opacity: 1;
}
input[type="text"],
input[type="password"] {
  width: calc(100% - 57px);
  height: 36px;
  margin: 13px 0 0 -5px;
  padding-left: 10px;
  border-radius: 0 5px 5px 0;
  border: solid 1px #cbc9c9;
  box-shadow: 1px 2px 5px rgba(0, 0, 0, 0.09);
  background: #fff;
}
input[type="password"] {
  margin-bottom: 15px;
}
#icon {
  display: inline-block;
  padding: 9.3px 15px;
  box-shadow: 1px 2px 5px rgba(0, 0, 0, 0.09);
  background: salmon;
  color: #fff;
  text-align: center;
}
.btn-block {
  margin-top: 10px;
  text-align: center;
}
button {
  width: 100%;
  padding: 10px 0;
  margin: 10px auto;
  border-radius: 5px;
  border: none;
  background: salmon;
  font-size: 14px;
  font-weight: bolder;
  color: #fff;
}
button:hover {
  background: #e66e69;
}

.lefttopcorner {
  position: absolute;
  top: 10px;
  left: 20px;
  cursor: pointer;
}

.righttopcorner {
  position: absolute;
  top: 20px;
  right: 20px;
  cursor: pointer;
}
</style>
