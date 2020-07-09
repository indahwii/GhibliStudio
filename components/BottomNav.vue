<template lang="pug">
    .bottom-nav
        nuxt-link.bottom-nav__link(:to="nav.path" v-for="(nav, $index) in navs" :class="{'active': activePath === nav.path}" :key="$index")
            span.icon(:class="nav.icon")
            span.title {{ nav.title }}
</template>

<script>
export default {
    data() {
        return {
            active: 0,
            navs: [
                {icon: 'ti-home', title: 'Home', path: '/'},
                {icon: 'ti-search', title: 'search', path: '/search'},
                {icon: 'ti-heart', title: 'Favorite', path: '/'},
                {icon: 'ti-user', title: 'Profile', path: '/'},
            ]
        }
    },
    computed: {
        activePath() {
            return this.$route.path;
        }
    },
    mounted() {

    },
    methods: {
    }
}
</script>

<style lang="sass">
@import '~/assets/sass/style.sass';
.bottom-nav 
    height: $nav-height
    display: none
    justify-content: space-around
    background-color: $grey
    position: fixed
    bottom: 0
    left: 50%
    transform: translateX(-50%)
    width: 100%
    // max-width: 768px
    z-index: 99

    &__link
        display: flex
        height: $nav-height
        flex-direction: column
        justify-content: center
        align-items: center
        color: $purple
        
        .icon
            transition: 0.2s
            font-size: 20px
            margin-bottom: 2.5px

        .title
            transition: 0.2s
            font-size: 11px

        span
            color: #888888

        &.active span
            color: $purple

@media screen and (max-width: $small)
    .bottom-nav 
        display: flex
</style>