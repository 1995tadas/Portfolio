<template>
  <div :class="{'fixed-header':isFixed && desktopWidth}">
    <template v-if="!(desktopWidth || mobileMenu)">
      <a class="flag" href="#" @click.prevent="changeLang">
        <img :src="'https://www.countryflags.io/'+ (setLang === 'english'?'lt':'gb') +'/flat/32.png'">
      </a>
      <a class="hamburger" @click.prevent="mobileMenu = !mobileMenu" href="">
        <i class="fas fa-bars"></i>
      </a>
    </template>
    <nav class="header" v-show="mobileMenu || desktopWidth">
      <a @click="isFixed = !isFixed" href="#home" v-show="desktopWidth && isFixed">{{ lang.home }}</a>
      <a @click="!desktopWidth?mobileMenu = !mobileMenu:null" href="#project">{{ lang.projects }}</a>
      <a @click="!desktopWidth?mobileMenu = !mobileMenu:null" href="#about"> {{ lang.about }}</a>
      <a class="close" v-if="!desktopWidth" @click.prevent="mobileMenu = !mobileMenu" href="#">
        <i class="far fa-window-close"></i>
      </a>
    </nav>
  </div>
</template>

<script>
export default {
  name: 'Header',
  data() {
    return {
      isFixed: false,
      setLang: "lithuanian",
      desktopWidth: window.innerWidth > 768,
      mobileMenu: false
    }
  },
  props: {
    lang: Object
  },
  beforeMount() {
    this.addScrollListener();
    this.$root.$emit('language', this.lang);
    addEventListener('resize', () => {
      this.desktopWidth = innerWidth > 768;
      this.addScrollListener();
    })

  },
  methods: {
    addScrollListener() {
      if (this.desktopWidth) {
        window.addEventListener('scroll', this.scroll);
      } else {
        window.removeEventListener('scroll', this.scroll)
      }
    },
    scroll() {
      this.isFixed = window.top.scrollY > 100;
    },
    changeLang() {
      if (this.setLang === 'english') {
        this.setLang = 'lithuanian'
      } else if (this.setLang === 'lithuanian') {
        this.setLang = 'english'
      }

      this.$root.$emit('language', this.setLang);
    }
  }
}
</script>
