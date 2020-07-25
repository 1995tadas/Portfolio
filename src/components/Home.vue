<template>
    <section id="home">
        <div class="home-content">
            <div class="introduction">
                <h3>{{lang.greeting}}</h3>
                <h1>{{lang.name}}</h1>
                <h2>{{lang.position}}</h2>
                <h3>{{lang.from}}</h3>
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
    @import url('https://fonts.googleapis.com/css2?family=Staatliches&display=swap');
    @import '../assets/scss/variables';

    #home {
        height: 100Vh;
        background: rgba(135, 206, 235, 0.2) url("../assets/urban-metro-subway-65777.jpg") no-repeat center;
        background-size: cover;
        background-blend-mode: lighten;

        .home-content {
            text-shadow: 1px 10px 50px;
            font-family: 'Staatliches', cursive;
            width: 100%;
            height: 100%;
            margin: 0 auto;
            box-sizing: border-box;

            .introduction {
                height: 100%;
                display: flex;
                align-items: center;
                justify-content: center;
                flex-direction: column;
                color: $primary-color;
                box-sizing: border-box;

                h1 {
                    margin: 40px 0 0;
                    font-size: 5vw;
                    @media(max-width: $breakpoint-tablet) {
                        font-size: 10vw;
                    }
                }

                h2 {
                    margin: 40px 0;
                    font-size: 4vw;
                    @media(max-width: $breakpoint-tablet) {
                        font-size: 8vw;
                    }
                }

                h3 {
                    margin: 0;
                    font-size: 2.5vw;
                    @media(max-width: $breakpoint-tablet) {
                        font-size: 5vw;
                    }
                }
            }
        }
    }
</style>
