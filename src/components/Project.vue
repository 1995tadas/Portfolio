<template>
  <section id="project">
    <h1 class="title">{{ lang.projects }}</h1>
    <div class="project-items">
      <div class="project-row">
        <div class="project-item" v-for="(project, projectKey) in projects" :key="project.title">
          <div class="project-top">
            <img class="project-mockup" :src="getImgUrl(project['image-link'])">
            <h2 class="project-title">{{ project['title'] }}</h2>
          </div>
          <div class="project-about">
            <ul class="project-description">
              <li v-for="item in project['description']" :key="item">{{ item }}</li>
            </ul>
            <div class="project-links">
              <a v-for="(link, type) in projects[projectKey].links" @mouseenter="jumpingText(type, projectKey)"
                 @mouseleave="clearTimeouts" class="project-link"
                 target="_blank"
                 :href="link"
                 :key="link">
                <button :title="lang['link_' + type]">
                  <template v-if="desktopWidth">
                    <span :class="{'jump': index === parseInt(jumpingLetter[projectKey+type])}"
                          v-for="(letter, index) in stringToArray(lang[type])"
                          :key="index">{{ letter }}</span>
                  </template>
                  <span v-else>{{ lang[type] }}</span>
                </button>
              </a>
            </div>
          </div>
        </div>
      </div>
      <h1 class="soon">{{ lang.soon }}</h1>
    </div>
  </section>
</template>

<script>
export default {
  name: 'Projects',
  props: {
    lang: {
      type: Object,
      required: true,
    }
  },
  watch: {
    lang() {
      this.setProjectsTranslations(this.lang);
    }
  },
  created() {
    this.setProjectsTranslations(this.lang);
  },
  data() {
    return {
      projects: [
        {
          'image-link': 'corona-mockup.png',
          'links': {
            'code': 'https://github.com/1995tadas/corona',
            'live': 'http://tadassapitavicius.com/corona',
          }
        },
        {
          'image-link': 'hangman-mockup.png',
          'links': {
            'code': 'https://github.com/1995tadas/hangman',
            'live': 'http://tadassapitavicius.com/hangman',
          }
        },
        {
          'image-link': 'movie-api-mockup.png',
          'links': {
            'code': 'https://github.com/1995tadas/movie-api',
            'live': 'http://tadassapitavicius.com/movies',
          }
        }
      ],
      jumpingLetter: {},
      timeOuts: [],
      desktopWidth: window.innerWidth > 768,
    }
  },
  methods: {
    getImgUrl(link) {
      return require('../assets/images/' + link);
    },
    setProjectsTranslations(lang) {
      const projectsLength = this.projects.length;
      for (let i = 0; i < projectsLength; i++) {
        this.projects[i].title = lang.descriptions['project' + (i + 1)].title;
        this.projects[i].description = lang.descriptions['project' + (i + 1)].paragraph;
      }
    },
    stringToArray(string) {
      return string.split('');
    },
    jumpingText(text, key) {
      let letters = this.lang[text].split('');
      for (let index in letters) {
        this.timeOuts.push(setTimeout(() => {
          this.$set(this.jumpingLetter, key + text, index);
        }, index * 200))
      }
    },
    clearTimeouts() {
      let timeOutsLength = this.timeOuts.length;
      for (let i = 0; i < timeOutsLength; i++) {
        clearTimeout(this.timeOuts[i]);
        this.jumpingLetter = {};
      }
    }
  }
}
</script>
