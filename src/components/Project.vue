<template>
    <section id="project">
        <span class="title">{{lang.projects}}</span>
<!--        <div class="project-items">-->
<!--            <div v-for="n in 4" :key="n" class="project_item"></div>-->
<!--        </div>-->
        <h1>{{lang.soon}}</h1>
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
        height: 100vh;
        text-align: center;
        padding: 55px 20px 20px;
        box-sizing: border-box;
        @media (max-width: $breakpoint-tablet) {
            padding-top: 20px;
        }
        /* .project-items {
            margin: 20px 0;
            height: 90%;
            display: flex;
            flex-wrap: wrap;
            @media (max-width: $breakpoint-tablet){
                height: 45%;
            }
            .project_item {
                border: 1px solid  $text-color;
                background-color: $secondary-color;
                height: 50%;
                width: 100%;
                &:first-child {
                    border-radius: 30px 30px 0 0;
                }
                &:last-child {
                    border-radius: 0 0 30px 30px;
                }
                box-sizing: border-box;
                @media (min-width: $breakpoint-tablet){
                    width: 50%;
                    &:first-child {
                        border-radius: 50px 0 0 0;
                    }
                    &:nth-child(2) {
                        border-radius: 0 50px 0 0;
                    }
                    &:last-child {
                        border-radius: 0 0 50px 0;
                    }
                    &:nth-last-child(2){
                        border-radius: 0 0 0 50px;
                    }
                }
            }
        }
         */
    }
</style>
