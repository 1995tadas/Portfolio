<template>
  <section id="project">
    <span class="title">{{ lang.projects }}</span>
    <div class="project-items">
      <div class="project-row">
        <div class="project-item">
          <img class="project-mockup" src="../assets/test-mockup.png">
          <div class="project-about">
            <p>{{ lang.project1.title }}</p>
            <ol>
              <li v-for="n in lang.project1.paragraph" :key="n">{{ n }}</li>
            </ol>
            <div class="project-links">
              <a target="_blank" href="https://github.com/1995tadas/tests">
                <button>{{ lang.code }}</button>
              </a>
              <a target="_blank" href="https://tadas-tests.herokuapp.com/">
                <button>{{ lang.live }}</button>
              </a>
            </div>
          </div>
        </div>
        <div class="project-item">
          <img class="project-mockup" src="../assets/hangman-mockup.png">
          <div class="project-about">
            <p>{{ lang.project3.title }}</p>
            <ul>
              <li v-for="n in lang.project3.paragraph" :key="n">{{ n }}</li>
            </ul>
            <div class="project-links">
              <a target="_blank" href="https://github.com/1995tadas/Hangman">
                <button>{{ lang.code }}</button>
              </a>
              <a target="_blank" href="https://tadas-hangman.herokuapp.com/">
                <button>{{ lang.live }}</button>
              </a>
            </div>
          </div>
        </div>
        <div class="project-item">
          <img class="project-mockup" src="../assets/movie-api-mockup.png">
          <div class="project-about">
            <p>{{ lang.project2.title }}</p>
            <ul>
              <li v-for="n in lang.project2.paragraph" :key="n">{{ n }}</li>
            </ul>
            <div class="project-links">
              <a target="_blank" href="https://github.com/1995tadas/MovieApi">
                <button>{{ lang.code }}</button>
              </a>
              <a target="_blank" href="https://tadas-moviesearch.herokuapp.com/">
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
    lang: Object
  }
}
</script>

<style scoped lang="scss">
@import '../assets/scss/variables';
@import '../assets/scss/snipets';

#project {
  min-height: 100vh;
  text-align: center;
  padding: 55px 20px 20px;
  box-sizing: border-box;
  background-color: #b4e7ad;
  @media (max-width: $breakpoint-tablet) {
    padding-top: 20px;
  }

  .project-items {
    margin: 20px 0;
    height: 90%;
    box-sizing: border-box;

    .project-row {
      padding-bottom: 20px;
      display: flex;
      justify-content: space-around;
      box-sizing: border-box;
      flex-wrap: wrap;
      width: 100%;

      .project-item {
        color: $primary-color;
        display: flex;
        justify-content: space-between;
        flex-direction: column;
        align-items: center;
        text-align: left;
        margin-top: 10px;
        padding: 25px 20px;
        background-color: $text-color;
        border-radius: 5px;
        @media (max-width: $breakpoint-tablet) {
          &:not(:first-child) {
            margin-top: 20px;
          }
        }

        &:hover {
          background-color: rgba($text-color, 0.4);
        }

        .project-mockup {
          width: 300px;
          @media(max-width: $breakpoint-tablet) {
            width: 90%;
          }
        }

        .project-about {
          width: 100%;
          @media(max-width: $breakpoint-tablet) {
            font-size: 3vw;
          }

          ol, ul {
            padding-left: 18px;
          }

          .project-links {
            display: flex;
            justify-content: space-between;

            button {
              font-size: 20px;
              font-weight: bold;
              color: $tertiary-color;
              padding: 5px 30px;
              background-color: $text-color;
              border: 3px solid $secondary-color;
              border-radius: 3px;
              cursor: pointer;
              @media(max-width: $breakpoint-tablet) {
                padding: 0 20px;
              }

              &:hover {
                background-color: $secondary-color;
              }
            }
          }
        }
      }
    }
  }
}
</style>
