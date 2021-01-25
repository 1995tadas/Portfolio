<template>
  <section id="home">
    <div class="home-content">
      <div class="introduction">
        <h3 class="rolling-greeting">
          <span class="placeholder">!</span>
          <span v-for="(letter, index) in rollingGreeting" :key="index">{{ letter }}</span>
        </h3>
        <h1 class="rolling-name">
          <span class="half-name" v-for="(half, index) in rollingName" :key="index">
            <span v-for="(letter, index) in half" :key="index">{{ letter }}</span>
          </span>
        </h1>
        <h2>{{ lang.position }}</h2>
        <h3>{{ lang.from }}</h3>
        <ul class="link-icons">
          <li>
            <a target="_blank" href="https://github.com/1995tadas" title="Github">
              <i class="fab fa-github"></i> Github
            </a>
          </li>
          <li>
            <a target="_blank"
               href="https://drive.google.com/file/d/1437xK86dXMVXq4Wmk21Ulgaa3wVvQof9/view?usp=sharing"
               :title="lang.resume">
              <i class="fas fa-file"></i> {{ lang.resume }}
            </a>
          </li>
          <li>
            <a target="_blank" href="https://www.linkedin.com/in/tadas-sapitavi%C4%8Dius-20bb62167/" title="LinkedIn">
              <i class="fab fa-linkedin"></i> LinkedIn
            </a>
          </li>
        </ul>
      </div>
    </div>
  </section>
</template>

<script>
export default {
  name: 'Home',
  props: {
    lang: Object
  },
  data() {
    return {
      rollingGreeting: [],
      rollingName: [],
      timeOuts: [],
    }
  },
  mounted() {
    window.addEventListener('load', () => {
      this.runAnimations(this.lang);
    })
  },
  watch: {
    lang() {
      this.runAnimations(this.lang);
    }
  },
  methods: {
    runAnimations(lang) {
      this.rollGreeting(lang.greeting);
      this.rollName(lang.name);
    },
    rollGreeting(greeting) {
      const timeOutsLength = this.timeOuts.length;
      if (timeOutsLength) {
        for (let i = 0; i < timeOutsLength; i++) {
          clearTimeout(this.timeOuts[i]);
        }

        this.timeOuts = []
      }

      this.rollingGreeting = [];
      this.timeOuts.push(setTimeout(() => {
        for (let key in greeting) {
          this.timeOuts.push(setTimeout(() => {
            this.rollingGreeting.push(greeting.charAt(key));
          }, key * 100));
        }
      }, 500));
    },
    rollName(name) {
      if (this.rollingName.length) {
        let el = document.querySelector(".rolling-name");
        el.classList.remove("rolling-name");
        el.offsetWidth;
        el.classList.add("rolling-name");
        this.rollingName = [];
      }

      let lastSpaceIndex = name.lastIndexOf(' ');
      let firstHalf = name.slice(0, lastSpaceIndex);
      let secondHalf = name.slice(lastSpaceIndex);
      this.rollingName = [firstHalf.split(''), '   ', secondHalf.split('')];
    }
  }
}
</script>
