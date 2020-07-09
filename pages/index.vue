<template lang="pug">
  .wrapper
    Header
    section.sec-1
      .banner
        img(src="images/logo.svg")
      .flex-bt.pt-2
        h3.text-title ALL
        h3.text-title Trending
      .film-group(class="row columns is-multiline")
        .div(class="column is-4" v-for="films in snapshot")
          nuxt-link.film-item(:to="'/profile?id='+films.id")
            .film-item__head
              img(src="images/film.jpg")
              h5 {{films.release_date }}
            .film-item__body
              h3 {{ films.title }}
              h5 {{films.director }} / {{films.director }}
              h4.pt-1.ti-heart  {{ films.rt_score }}
    
</template>

<script>
import Header from '~/components/Header';
export default {
    components: {
      Header
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
                }
          });
        },
        getPosts() {
          
        }
    }
}
</script>

<style lang="sass" scoped>
  @import '~/assets/sass/style.sass'

  .wrapper 
    .banner
        width: 100%
        margin: 0 auto
        text-align: center
        // height: 180px
        // background-color: #f5f5f5
        // border: 1px solid #f5f5f5
        // border-radius: 5px

        img 
          width: auto
          height: 180px


    .film-group 
        margin-top: $gap1

        .film-item 
          margin-top: $gap1
          width: 100%
          height: 200px
          background-color: white
          border-radius: 5px
          display: flex
          justify-content: space-between
          box-shadow: 0px 0px 15px rgba(0, 0, 0, 0.1)

          &__head
            width: 40%
            padding: 10px
            background-color: #424874
            border-radius: 5px 0px 0px 5px

            h5
              margin-top: 5px
              color: #fff
              font-size: 16px
              text-align: center

            img 
              width: 100%
              height: auto

          &__body
            width: 60%
            padding: $gap1
            color: #424874


            h3 
              font-weight: 600
              font-size: 18px
              color: #424874
              margin-bottom: $gap1

            h5
              color: #000

            .ti-heart
              font-weight: 600

    .text-bold
      font-weight: bold
    
</style>