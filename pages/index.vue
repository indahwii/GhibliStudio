<template lang="pug">
  .wrapper
    Header
    section.body
      carousel.banner(items="1" :nav="false")
        img(src="images/logo.svg" )
        img(src="images/1.jpg" )
        img(src="images/2.jpeg" )
      .flex-bt.pt-2
        h2.text-title Trending
      .film-group(class="row columns is-multiline")
        .div(class="column is-4" v-for="films in snapshot.slice(0, 5)")
          nuxt-link.film-item(:to="'/profile?id='+films.id")
            .film-item__head
              img(data-src="images/film.jpg" v-lazy-load="")
              h5 {{films.release_date }}
            .film-item__body
              h3 {{ films.title }}
              h5 {{films.director }} / {{films.director }}
              .scored
                span.ti-heart  
                | {{ films.rt_score }}
      BottomNav
</template>

<script>
import carousel from 'v-owl-carousel';
import Header from '~/components/Header';
import BottomNav from '~/components/BottomNav';

export default {
    components: {
      Header,
      carousel,
      BottomNav
    },
    filters: {
    },
    data() {
      return {
        snapshot: [],
      }
    },
    computed: {
    },
    mounted() {
       this.getSnapshot();
    },
    methods: {
        getSnapshot() {
          this.$axios.get("https://ghibliapi.herokuapp.com/films", {
          })
          .then(response => {
                const {status, data} = response;

                if (status === 200) {
                    this.snapshot = data;
                    this.species = data.species;
                }
          });
        }
    }
}
</script>

<style lang="sass" scoped>
  @import '~/assets/sass/style.sass'
  
  .wrapper 
    .owl-theme .owl-nav
      display: none !important

    .banner
        width: 100%
        margin: 0 auto
        text-align: center
        padding-top: 10px
        img 
          margin: 0 auto
          width: 95%
          max-height: 500px

        @media screen and (max-width: $small)
          img 
            width: 100%


    .film-group 
        .film-item 
          margin-top: $gap1
          width: 100%
          height: 210px
          background-color: white
          border-radius: 5px
          display: flex
          justify-content: space-between
          box-shadow: 0px 0px 15px rgba(0, 0, 0, 0.1)

          &__head
            width: 40%
            background-color: $purple
            border-radius: 5px 0px 0px 5px

            h5
              color: #fff
              font-size: 16px
              text-align: center

            img 
              width: 100%
              height: 170px

            @media screen and (max-width: $small)
              img 
                width: 100%
                height: 150px
    

          &__body
            width: 60%
            padding: $gap1
            color: $purple

            h3 
              font-weight: 600
              font-size: 18px
              color: $purple

            h5
              color: #000

            .scored
              margin-top: $gap3
              font-weight: bold
              font-size: 25px

              .ti-heart
                font-weight: 700
                color: red
                margin-right: 5px

    .text-bold
      font-weight: bold
      
    
</style>