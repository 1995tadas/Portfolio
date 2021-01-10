<template>
  <section id="project">
    <span class="title">{{ lang.projects }}</span>
    <div class="project-items">
      <div class="project-row">
        <div class="project-item" v-for="project in projects" :key="project.title">
          <img class="project-mockup" :src="getImgUrl(project['image-link'])">
          <div class="project-about">
            <p>{{ project['title'] }}</p>
            <ul>
              <li v-for="item in project['description']" :key="item">{{ item }}</li>
            </ul>
            <div class="project-links">
              <a target="_blank" :href="project['code-link']">
                <button>{{ lang.code }}</button>
              </a>
              <a target="_blank" :href="project['live-link']">
                <button>{{ lang.live }}</button>
              </a>
            </div>
          </div>
        </div>
      </div>
      <h1>{{ lang.soon }}</h1>
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
          'code-link': 'https://github.com/1995tadas/corona',
          'live-link': 'https://covid-statistika.herokuapp.com/',
        },
        {
          'image-link': 'hangman-mockup.png',
          'code-link': 'https://github.com/1995tadas/hangman',
          'live-link': 'https://tadas-hangman.herokuapp.com/',
        },
        {
          'image-link': 'movie-api-mockup.png',
          'code-link': 'https://github.com/1995tadas/movie-api',
          'live-link': 'https://tadas-moviesearch.herokuapp.com/',
        }
      ],
    }
  },
  methods: {
    getImgUrl(link) {
      return require('../assets/images/' + link);
    },
    setProjectsTranslations(lang) {
      const projectsLength = this.projects.length;
      for (let i = 0; i < projectsLength; i++) {
        this.projects[i].title = lang.projects_descriptions['project' + (i + 1)].title;
        this.projects[i].description = lang.projects_descriptions['project' + (i + 1)].paragraph;
      }
    }
  }
}
</script>
