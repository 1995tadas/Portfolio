<template>
  <section id="home">
    <div class="home-content">
      <div class="introduction">
        <h3 class="rolling-greeting">
          <span v-for="(letter, index) in rollingGreeting" :key="index">{{ letter }}</span>
        </h3>
        <h1 class="rolling-name">
          <span class="half-name" v-for="(half, index) in rollingName" :key="index">
            <span v-for="(letter, index) in half" :key="index">{{ letter }}</span>
          </span>
        </h1>
        <h2>{{ lang.position }}</h2>
        <h3>{{ lang.from }}</h3>
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
<style scoped lang="scss">
.rolling-greeting span {
  &:last-child {
    opacity: 1;
    animation: fadeIn 1s;
  }
}

@keyframes fadeIn {
  0% {
    opacity: 0.2;
  }
  100% {
    opacity: 1;
  }
}

.rolling-name {

  .half-name {
    display: inline-block;

    &:first-child {
      &::after {
        content: "\00a0";
      }

      transform: translateX(-100px);
    }

    &:last-child {
      transform: translateX(100px);
    }

    animation: slideIn 0.5s ease-in-out forwards;

    @keyframes slideIn {
      100% {
        transform: translateX(0);
      }
    }

    span {
      &:last-child {
        display: inline-block;
        animation: 0.5s stretch 0.5s forwards;
      }

      @keyframes stretch {
        50% {
          transform: scaleX(1);
        }
        90% {
          transform: scaleX(3);
        }
        100% {
          color: #d76464;
        }
      }
    }
  }
}

</style>
