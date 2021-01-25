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