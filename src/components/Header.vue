<template>
    <div :class="{'fixed':isFixed && desktop}">
        <a class="flag" href="#" @click.prevent="changeLang">
            <img :src="'https://www.countryflags.io/'+ (setLang === 'english'?'lt':'gb') +'/flat/32.png'">
        </a>
        <a class="hamburger" @click.prevent="mobileMenu = !mobileMenu" :class="{hide:desktop}" href="">
            <i class="fas fa-bars"></i>
        </a>
        <nav class="header" :class="{hide:!desktop && !mobileMenu}">
            <a href="#home" :class="{hide:!desktop}">{{lang.home}}</a>
            <a @click="mobileMenu = !mobileMenu" href="#project">{{lang.projects}}</a>
            <a @click="mobileMenu = !mobileMenu" href="#about"> {{lang.about}}</a>
            <a class="close" @click.prevent="mobileMenu = !mobileMenu" :class="{hide:desktop}" href="#">
                <i class="fas fa-arrow-up"></i>
            </a>
        </nav>
    </div>
</template>

<script>

    export default {
        name: 'Header',
        data() {
            return {
                isFixed: false,
                setLang: "english",
                desktop: window.innerWidth >= 768,
                mobileMenu: false
            }
        },
        props: {
            lang: Object
        },
        beforeMount() {
            this.checkDesktop();
            this.$root.$emit('language', this.lang);
            addEventListener('resize', () => {
                this.desktop = innerWidth >= 768;
                this.checkDesktop();
            })

        },
        methods: {
            checkDesktop() {
                if (this.desktop) {
                    window.addEventListener('scroll', this.scroll);
                } else {
                    window.removeEventListener('scroll', this.scroll)

                }
            },
            scroll() {
                this.isFixed = window.top.scrollY > 40;
            },
            changeLang() {
                if (this.setLang === 'english') {
                    this.setLang = "lithuanian"
                } else if (this.setLang === 'lithuanian') {
                    this.setLang = "english"
                }
                this.$root.$emit('language', this.setLang);
            }
        }
    }

</script>

<style scoped lang="scss">
    @import url('https://fonts.googleapis.com/css2?family=Lato&display=swap');
    @import '../assets/scss/variables';

    .header {
        font-family: 'Lato', sans-serif;
        text-align: right;
        padding: 10px;
        position: absolute;
        top: 10px;
        right: 10px;
        transition: 0.5s linear;
        box-sizing: border-box;
        @media (max-width: $breakpoint-tablet) {
            top: 0;
            right: 0;
            padding: 0;
            display: flex;
            flex-direction: column;
            max-width: 100%;
            min-width: 100%;
            text-align: center;
            transition: none;
            .close {
                padding: 10px 0 0;
                font-size: 40px;
                border: none;
            }
        }

        a {
            color: $primary-color;
            border: 3px solid $secondary-color;
            margin-left: 10px;
            text-decoration: none;
            padding: 5px 20px;
            border-radius: 5px;
            font-size: 1.2em;

            &:first-child {
                margin-left: 0;
            }

            &:hover {
                opacity: 0.5;
            }

            &:active {
                color: $active-color;
            }

            @media (max-width: $breakpoint-tablet) {
                padding: 20px 0;
                margin: 0;
                border-radius: 0;
                border: none;
                border-bottom: 3px dashed $tertiary-color;
                font-size: 2em;
                color: $primary-color;
                background-color: $secondary-color;
                &:hover {
                    opacity: 1;
                    background-color: $hover-color;
                }
            }
        }
    }

    .fixed {
        position: sticky;
        top: 0;
        padding: 30px;
        background-color: $primary-color;

        a {
            color: $text-color;
        }
    }

    .flag {
        position: absolute;
        left: 10px;
        top: 10px;
    }

    .hamburger {
        position: absolute;
        top: 10px;
        right: 20px;
        font-size: 38px;
        color: $secondary-color;

        &:hover {
            color: $hover-color;
        }
    }

    .hide {
        display: none;
    }
</style>
