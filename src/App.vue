<template>
  <div id="app">
    <Header :lang="this.lang"/>
    <Home :lang="this.lang"/>
    <Project :lang="this.lang"/>
    <About :lang="this.lang"/>
  </div>
</template>

<script>
import ltu from './lang/ltu.js'
import eng from './lang/eng.js'
import Header from './components/Header.vue';
import Home from './components/Home.vue'
import Project from './components/Project.vue'
import About from './components/About.vue'

export default {
  name: 'App',
  components: {
    Header,
    Home,
    Project,
    About
  },
  data() {
    return {
      lang: ltu
    }
  },
  created() {
    this.$root.$on('language', language => {
      if (language === "english") {
        this.lang = eng;
      } else if (language === "lithuanian") {
        this.lang = ltu;
      }
    });
  }
}
</script>
