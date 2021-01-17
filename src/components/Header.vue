<template>
  <div :class="{'fixed-header':isFixed && desktopWidth}">
    <template v-if="!mobileMenu">
      <a class="flag" href="#" @click.prevent="changeLang"
         :title="lang.change + ' ' + lang[oppositeLanguage] + ' ' + lang.language">
        <img :src="'https://www.countryflags.io/'+ (setLang === 'english'?'lt':'gb') + '/flat/64.png'"
             :alt="lang[oppositeLanguage] + ' ' + lang.flag">
      </a>
      <a v-if="!desktopWidth" class="hamburger" @click.prevent="toggleMenu" href="">
        <i class="fas fa-bars"></i>
      </a>
    </template>
    <nav class="header" v-show="mobileMenu || desktopWidth">
      <a @click="isFixed = !isFixed" href="#home" :title="lang.go_to + ' - ' + lang.home.toLowerCase()"
         v-show="desktopWidth && isFixed">
        {{ lang.home }}
      </a>
      <a @click="toggleMenu" href="#project" :title="lang.go_to + ' - ' + lang.projects.toLowerCase()">
        {{ lang.projects }}
      </a>
      <a @click="toggleMenu" href="#about" :title="lang.go_to + ' - ' + lang.about.toLowerCase()">
        {{ lang.about }}
      </a>
      <a class="close" v-if="!desktopWidth" @click.prevent="toggleMenu" href="#">
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
  mounted() {
    this.addScrollListener();
    this.$root.$emit('language', this.lang);
    addEventListener('resize', () => {
      this.desktopWidth = innerWidth > 768;
      this.addScrollListener();
    })
  },
  computed: {
    oppositeLanguage() {
      let oppLanguage = '';
      if (this.setLang === 'english') {
        oppLanguage = 'lithuanian';
      } else if (this.setLang === 'lithuanian') {
        oppLanguage = 'english'
      } else {
        oppLanguage = 'na'
      }

      return oppLanguage;
    }
  },
  methods: {
    addScrollListener() {
      if (this.desktopWidth) {
        window.addEventListener('scroll', this.scroll);
        this.toggleMenu();
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
    },
    toggleMenu() {
      const element = document.querySelector('.introduction');
      if (!this.desktopWidth) {
        this.mobileMenu = !this.mobileMenu;
        if (element.classList.contains('blur')) {
          element.classList.remove('blur');
        } else {
          element.classList.add('blur');
        }
      } else if (element.classList.contains('blur')) {
        element.classList.remove('blur');
        this.mobileMenu = !this.mobileMenu;
      }
    }
  }
}

</script>
