
<template>
  <div class="hello">
    <h1>ALBUM ART AFFINITY</h1>
    <nav>
      <router-link v-if="authenticated" to="/" v-on:click="logout()" replace>Logout</router-link>
      &nbsp;
      <router-link to ="/home">HOME</router-link>
      &nbsp;
      <router-link to ="/about">ABOUT</router-link>
      &nbsp;
      <router-link to ="/genres">MUSIC GENRES</router-link>
      &nbsp;
      <router-link to ="/new">ADD A GENRE</router-link>
    </nav>

    <router-view
    :genres="genres"
    ></router-view>
    <section id="home">
    <img src="./assets/vinyl.png" />
  </section>
  </div>
</template>

<script>
import {
  getGenres
} from './services/api.js';

export default {
  data() {
    return {
      genres: '',
      authenticated: false,
      mockAccount: {
        username: "alchemy",
        password: "codelab"
      }
    }
  },
  created() {
    getGenres()
      .then(genres => {
        this.genres = genres;
      })
      .catch(err => {
        this.error = err;
      });
  },
  mounted() {
    if(!this.authenticated) {
      this.$routed.replace({ name: "login" });
    }
  },
  methods: {
    setAuthenticated(status) {
      this.authenticated = status;
    },
    logout() {
      this.authenticated = false;
    }
  }

};
</script>

<style>
@import url('https://fonts.googleapis.com/css?family=Comfortaa:700|Knewave');

h1 {
  font-family: 'Comfortaa', sans-serif;
  font-weight: bold;
  font-size: 3em;
  letter-spacing: .1em;
  color: #fff;
  padding: 6% 20%;
  text-align: center;
  margin: 0;
  background: linear-gradient(226deg, #d4625f, #e99a57, #e3c94c);
  background-size: 600% 600%;
  -webkit-animation: AnimationName 6s ease infinite;
  -moz-animation: AnimationName 6s ease infinite;
  animation: AnimationName 6s ease infinite;
}

  @-webkit-keyframes AnimationName {
    0%{background-position:0% 22%}
    50%{background-position:100% 79%}
    100%{background-position:0% 22%}
}
@-moz-keyframes AnimationName {
    0%{background-position:0% 22%}
    50%{background-position:100% 79%}
    100%{background-position:0% 22%}
}
@keyframes AnimationName { 
    0%{background-position:0% 22%}
    50%{background-position:100% 79%}
    100%{background-position:0% 22%}
}

#app {
  margin-top: 0px;
}

nav {
  font-family: 'Knewave', cursive;
  font-size: 1.5em;
  letter-spacing: .1em;
  margin: 0;
  padding: 0;
  text-align: center;
}

a {
  padding-top: 18px;
  padding-left: 12px;
  padding-right: 12px;
  padding-bottom: 6px;
}

a:hover {
  background-color: rgba(101, 4, 97, 0.331);
  

}

a:-webkit-any-link {
  text-decoration: none;
  color: rgba(77, 24, 75, 0.817);
}

a:-webkit-any-link:hover{
  color: #fff;
}
</style>
