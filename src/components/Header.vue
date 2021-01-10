<template>
  <div :class="{'fixed':isFixed && largeWidth}">
    <a class="flag" href="#" @click.prevent="changeLang">
      <img :src="'https://www.countryflags.io/'+ (setLang === 'english'?'lt':'gb') +'/flat/32.png'">
    </a>
    <a class="hamburger" @click.prevent="mobileMenu = !mobileMenu" :class="{hide:largeWidth}" href="">
      <i class="fas fa-bars"></i>
    </a>
    <nav class="header" :class="{hide:!largeWidth && !mobileMenu}">
      <a href="#home" :class="{hide:!largeWidth}">{{ lang.home }}</a>
      <a @click="mobileMenu = !mobileMenu" href="#project">{{ lang.projects }}</a>
      <a @click="mobileMenu = !mobileMenu" href="#about"> {{ lang.about }}</a>
      <a class="close" @click.prevent="mobileMenu = !mobileMenu" :class="{hide:largeWidth}" href="#">
        <i class="fas fa-arrow-up"></i>
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
      largeWidth: window.innerWidth > 768,
      mobileMenu: false
    }
  },
  props: {
    lang: Object
  },
  beforeMount() {
    this.IfLargeWidth();
    this.$root.$emit('language', this.lang);
    addEventListener('resize', () => {
      this.largeWidth = innerWidth > 768;
      this.IfLargeWidth();
    })

  },
  methods: {
    IfLargeWidth() {
      if (this.largeWidth) {
        window.addEventListener('scroll', this.scroll);
      } else {
        window.removeEventListener('scroll', this.scroll)

      }
    },
    scroll() {
      this.isFixed = window.top.scrollY > 40;
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
