<template>
    <div id="app">
        <Header :lang=this.lang />
        <Home :lang=this.lang />
        <Project :lang=this.lang />
        <About :lang=this.lang />
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
                lang: eng
            }
        },
        created() {
            this.$root.$on('language', data => {
                if (data === "english") {
                    this.lang = eng;
                } else if (data === "lithuanian") {
                    this.lang = ltu;
                }
            });
        }
    }
</script>

<style type="scss">

    html {
        scroll-behavior: smooth;
    }

    html, body {
        margin: 0;
        padding: 0;
    }

    #app {
        font-family: Avenir, Helvetica, Arial, sans-serif;
        -webkit-font-smoothing: antialiased;
        -moz-osx-font-smoothing: grayscale;
    }
</style>
