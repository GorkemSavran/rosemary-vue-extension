<template>
  <div class="container">
    <div class="righttopcorner">
      <a id="go-to-options" @click="goToOptions()">
        <img src="../assets/icon.png" />
      </a>
    </div>
    <h1>Rosemary</h1>
    <textarea @keyup="keyHandler" v-model="query" name="search" placeholder="Enter for search..."></textarea>
    <a name="answer">{{ answer === "" ? "..." : answer }}</a>
  </div>
</template>

<script>
export default {
  name: "App",
  data() {
    return {
      loadTimeout: null,
      answer: "",
      query: "",
    };
  },
  methods: {
    keyHandler(e) {
      // Having a second delay to prevent too many AJAX requests
      if (this.loadTimeout) clearTimeout(this.loadTimeout);
      this.loadTimeout = setTimeout(this.loadData, 1000);
      return;
    },
    loadData() {
      var query = this.query;
      this.answer = query;
      // AJAX call
    },
    goToOptions() {
      try {
        if (chrome.storage.local.get(["logged"])) {
          window.location = "main.html";
        }
      } catch (error) {
        // Ignore error
      }
    },
  },
  mounted() {
    var input = document.querySelector("[name=search]");
    input.focus();
  },
};
</script>

<style>
@import url(https://fonts.googleapis.com/css?family=Lato:100);
html,
body {
  /* height: 100%; */
  width: 500px;
}

body {
  background-color: salmon;
  color: #fff;
  font-size: 100%;
  overflow: hidden;
}

.righttopcorner {
  position: absolute;
  top: 10px;
  right: 20px;
  cursor: pointer;
}

.lefttopcorner {
  position: absolute;
  top: 10px;
  left: 20px;
  cursor: pointer;
}

.container {
  -moz-box-sizing: border-box;
  -webkit-box-sizing: border-box;
  box-sizing: border-box;
  height: 100%;
  padding: 2em;
}

textarea {
  -moz-box-sizing: border-box;
  -webkit-box-sizing: border-box;
  box-sizing: border-box;
  background-color: transparent;
  border: 0;
  color: #fff;
  display: block;
  font-family: "Lato";
  font-size: 2rem;
  font-weight: 100;
  height: 100%;
  margin: 0;
  padding: 0;
  outline: 0;
  width: 100%;
}
textarea::-webkit-input-placeholder {
  color: rgba(255, 255, 255, 0.25);
}
textarea:-moz-placeholder {
  color: rgba(255, 255, 255, 0.25);
}
textarea::-moz-placeholder {
  color: rgba(255, 255, 255, 0.25);
}
textarea:-ms-input-placeholder {
  color: rgba(255, 255, 255, 0.25);
}

h1,
h2,
h3,
h4,
h5,
h6 {
  font-family: "Lato";
  font-weight: 100;
}

a {
  -moz-box-sizing: border-box;
  -webkit-box-sizing: border-box;
  box-sizing: border-box;
  background-color: transparent;
  color: #fff;
  /* display: block; */
  font-family: "Lato";
  font-size: 2rem;
  font-weight: bolder;
}
/* a {
  -moz-transition: border 0.2s;
  -o-transition: border 0.2s;
  -webkit-transition: border 0.2s;
  transition: border 0.2s;
  color: #fff;
  border-bottom: 1px solid #fff;
  display: inline-block;
  text-decoration: none;
}
a:hover {
  border-color: rgba(255, 255, 255, 0.25);
} */
</style>
