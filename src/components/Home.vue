<template>
  <section id="home">
    <div class="home-content">
      <div class="introduction">
        <h3>{{ lang.greeting }}</h3>
        <h1>{{ lang.name }}</h1>
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
  }
}
</script>
