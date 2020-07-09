<template lang="pug">
    .header
        .header-control
            .child-center
                h3.title-head {{ this.$route.name == "index" ? "Home" : "" }}
                h3.title-head {{ this.$route.name == "profile" ? "Detail" : "" }}
                h3.title-head {{ this.$route.name == "search" ? "Search" : "" }}
</template>

<script>
export default {
    data() {
        return {
            active: 0,
            title: this.$route.name,
        }
    },
    computed: {
        
    },
    mounted() {
        
    },
    methods: {
        back() {
            this.$router.back()
        }
    }
}
</script>
<style lang="sass">
@import '~/assets/sass/style.sass';

.header
    width: 100%
    top: 0
    height: 60px
    background-color: $purple
    overflow: hidden;
    box-shadow: 0px 0px 15px rgba(0, 0, 0, 1)

    .header-control
        display: flex
        justify-content: space-between
        align-items: center
        padding-top: $gap2

        .child-center
            margin: 0 auto
            .title-head
                font-size: 22px
                color: $grey
                font-weight: 600

        button 
            font-size: 20px
            border: none
            padding: 0
            background: none

            span 
                margin-left: 10px
                font-weight: bold
                color: white
</style>