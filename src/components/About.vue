<template>
    <section id="about">
        <span class="title">{{lang.about}}</span>
        <div class="about-content">
            <div class="main-column">
                <p>
                    <span v-for="about in lang.about_text" :key="about">{{about}}</span>
                </p>
            </div>
            <div class="right-column right-top-column">
                <h1>{{lang.skills}}</h1>
                <ul>
                    <li><span>{{lang.back}}:</span> PHP, MySql</li>
                    <li><span>{{lang.front}}:</span> HTML5, Css3, Javascript (ES5-ES6)</li>
                    <li><span>{{lang.frame}}:</span> Laravel, CodeIgniter, VueJs</li>
                    <li><span>{{lang.library}}:</span> Bootstrap, JQuerry, Materialize, Inkline</li>
                    <li><span>{{lang.other}}:</span> Axios, RESTful API, MVC, OOP, Vue-cli, Webpack</li>
                    <li><span>{{lang.tools}}:</span> Npm, Composer, PHPStorm, Photoshop, Docker, Git</li>
                </ul>
            </div>
            <div class="right-column right-bottom-column">
                <h1>{{lang.links}}</h1>
                <ul>
                    <li>
                        <a target="_blank" href="https://github.com/1995tadas">
                            <i class="fab fa-github"></i> Github
                        </a>
                    </li>
                    <li>
                        <a target="_blank" href="#">
                            <i class="fas fa-file"></i> {{lang.resume}}
                        </a>
                    </li>
                    <li>
                        <a target="_blank" href="https://www.linkedin.com/in/tadas-sapitavi%C4%8Dius-20bb62167/">
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
        }
    }
</script>

<style scoped lang="scss">
    @import '../assets/scss/variables';
    @import url('https://fonts.googleapis.com/css2?family=Oxygen+Mono&display=swap');
    @import '../assets/scss/snipets';

    #about {
        padding: 20px 10px 10px;
        @media(min-width: $breakpoint-tablet) {
            padding: 55px 20px 20px;
        }
        background-image: linear-gradient(to right, skyblue, gray);
        text-align: center;
        font-family: 'Oxygen Mono', monospace;
        box-sizing: border-box;


        .about-content {
            box-sizing: border-box;
            width: 100%;
            height: 100%;
            margin: 0 auto;
            padding: 10px;
            display: grid;

            @media (max-width: $breakpoint-tablet) {
                grid-template-rows: 2fr 2fr 1fr;
            }
            @media(min-width: $breakpoint-tablet) {
                grid-template-columns: 1fr 1fr;
                grid-template-areas:"main-column right-top-column "
                                    "main-column right-bottom-column ";
            }

            .right-column {
                text-decoration: none;
                padding-top: 40px;
                color: $primary-color;
                font-size: 2vw;
                @media(min-width: $breakpoint-tablet) {
                    padding-left: 50px;
                    font-size: 1.1vw;
                }

                h1 {
                    padding: 10px 10%;
                    border-width: 3px;
                    border-color: $primary-color;
                    border-style: solid none;
                    display: inline;
                    color: #3f3e41;
                }

                ul {
                    padding: 0 10px;
                    list-style: none;
                    margin: 20px 0 0;
                    @media(min-width: $breakpoint-tablet) {
                        margin: 50px 0 0;
                    }
                }
            }

            .right-top-column {
                @media(min-width: $breakpoint-tablet) {
                    grid-area: right-top-column;
                }

                ul {
                    text-align: left;

                    li {
                        display: flex;
                        justify-content: space-between;
                        @media(min-width: $breakpoint-tablet) {
                            padding-top: 20px;
                        }
                        padding-top: 5px;
                        border-bottom: 5px solid $text-color;

                        span {
                            color: $tertiary-color;
                            font-size: 1.5em;
                            font-weight: 900;
                        }
                    }
                }
            }

            .right-bottom-column {
                @media(min-width: $breakpoint-tablet) {
                    grid-area: right-bottom-column;
                }

                ul {
                    text-align: center;
                    font-size: 1.2em;

                    @media(max-width: $breakpoint-tablet) {
                        padding-top: 40px;
                        font-size: 2em;
                    }

                    li {
                        display: inline;
                        padding-left: 10px;

                        &:first-child {
                            padding-left: 0;
                        }

                        a {
                            color: $secondary-color;
                            text-decoration: none;

                            &:active {
                                color: $active-color;
                            }

                            &:hover {
                                color: $hover-color;
                            }
                        }
                    }
                }
            }

            .main-column {
                text-align: justify;
                color: $primary-color;
                display: flex;
                justify-content: center;
                align-items: center;
                font-size: 3vw;
                @media(min-width: $breakpoint-tablet) {
                    font-size: 1.5vw;
                    width: 100%;
                    padding-right: 10px;
                    grid-area: main-column;
                    text-align: left;
                    border-right: 5px solid $text-color;
                }

                p {
                    line-height: 1.5em;

                    span {
                        display: block;
                    }
                }
            }
        }
    }
</style>
