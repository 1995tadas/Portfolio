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
      homeDimensions: {},
      snowflakes: 0,
      snowTypes: ['triangle', 'round', 'square'],
      animationType: ['rotate', 'flip', 'mash']
    }
  },
  mounted() {
    window.addEventListener('load', () => {
      this.resize();
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
      this.blizzard();
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
        let element = document.querySelector(".rolling-name");
        element.classList.remove("rolling-name");
        element.offsetWidth;
        element.classList.add("rolling-name");
        this.rollingName = [];
      }

      let lastSpaceIndex = name.lastIndexOf(' ');
      let firstHalf = name.slice(0, lastSpaceIndex);
      let secondHalf = name.slice(lastSpaceIndex);
      this.rollingName = [firstHalf.split(''), '   ', secondHalf.split('')];
    },
    resize() {
      this.getHomeSizes();
      addEventListener('resize', () => {
        this.getHomeSizes();
      })
    },
    getHomeSizes() {
      const home = document.querySelector(".introduction");
      this.homeDimensions.width = home.offsetWidth;
      this.homeDimensions.height = home.offsetHeight;
    },
    snow() {
      const snow = document.createElement("span");
      snow.classList.add("snow", this.randomArrayItem(this.snowTypes),
          this.randomArrayItem(this.animationType));
      const home = document.querySelector(".introduction");
      home.appendChild(snow);
      const snowWidth = snow.offsetWidth;
      const snowHeight = snow.offsetHeight;
      let top = 0;
      let left = Math.floor(Math.random() * this.homeDimensions.width);
      const drop = setInterval(() => {
        if (top <= this.homeDimensions.height - snowHeight && left <= this.homeDimensions.width - snowWidth) {
          top += Math.floor(Math.random() * 4);
          left += Math.floor((Math.random() * 8) - 4);
          snow.style.visibility = 'visible';
          snow.style.top = top + "px";
          snow.style.left = left + "px";
          if (top >= this.homeDimensions.height - snowHeight || left >= this.homeDimensions.width - snowWidth || left <= 0) {
            this.meltSnow(drop, snow);
          }
        } else {
          this.meltSnow(drop, snow);
        }
      }, 20)
    },
    meltSnow(drop, snow) {
      snow.classList.add('snow-fade');
      clearInterval(drop);
      setTimeout(() => {
        snow.remove();
        this.snowflakes--
      }, 500)
    },
    blizzard() {
      setInterval(() => {
        if (this.snowflakes < 10) {
          this.snow();
          this.snowflakes++
        }

      }, Math.floor((Math.random() * 1000) + 1000))
    },
    randomArrayItem(array) {
      const arrayLength = array.length;
      return array[Math.floor(Math.random() * arrayLength)];
    },
  }
}
</script>
