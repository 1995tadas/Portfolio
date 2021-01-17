<template>
  <section id="about">
    <h1 class="title">{{ lang.about }}</h1>
    <div class="about-content">
      <div class="main-column">
        <p>
          <span v-for="about in lang.about_text" :key="about">{{ about }}</span>
        </p>
      </div>
      <div class="right-column">
        <div class="right-top-column">
          <h2 class="section-title">{{ lang.skills }}</h2>
          <ul class="section-content">
            <li><span>{{ lang.back }}:</span> PHP, MySql</li>
            <li><span>{{ lang.front }}:</span> HTML5, Css3, Javascript (ES5-ES6)</li>
            <li><span>{{ lang.frame }}:</span> Laravel, VueJs</li>
            <li><span>{{ lang.library }}:</span> Bootstrap, Scss</li>
            <li><span>{{ lang.other }}:</span> Axios, RESTful API, MVC, OOP, Webpack</li>
            <li><span>{{ lang.tools }}:</span> Composer, PHPStorm, Photoshop, Git</li>
          </ul>
        </div>
        <div class="right-bottom-column">
          <h2 class="section-title">{{ lang.links }}</h2>
          <ul class="section-content">
            <li>
              <a target="_blank" href="https://github.com/1995tadas" title="Github">
                <i class="fab fa-github"></i> Github
              </a>
            </li>
            <li>
              <a target="_blank"
                 href="https://drive.google.com/file/d/1dZB8nSyTOY8OIqUaYMmtf2NkwTe4QVcW/view?usp=sharing" :title="lang.resume">
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
    </div>
  </section>
</template>

<script>
export default {
  name: 'Home',
  props: {
    lang: Object
  }
}
</script>