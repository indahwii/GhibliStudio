<template lang="pug">
  .wrapper
    Header
    section.sec-1
      .banner
        img(data-src="images/default-2.jpg" v-lazy-load="")
      .desc
        h2.title-desc {{ snapshot.title}}
        p.pt-2 {{ snapshot.description }}
      
        h4.text-bold.pt-2 People :
        span(v-for="people in peoples") {{ people.name }}. 
      
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
         snapshot: {},
         peoples: [],
      }
    },
    computed: {
    },
    mounted() {
       this.getSnapshot();
       this.getPeoples();
    },
    methods: {
        back() {
            this.$router.back()
        },
        getSnapshot() {
          this.$axios.get("https://ghibliapi.herokuapp.com/films/"+this.$route.query.id, {
          })
          .then(response => {
                const {status, data} = response;

                if (status === 200) {
                    this.snapshot = data;
                }
          });
        },
        getPeoples() {
          this.$axios.get("https://ghibliapi.herokuapp.com/people", {
          })
          .then(response => {
                const {status, data} = response;

                if (status === 200) {
                    this.peoples = data;
                }
          });
        }
    }
}
</script>

<style lang="sass" scoped>
  @import '~/assets/sass/style.sass';

  .wrapper 
    .banner
      img 
        width: 100%
    .desc
      margin-top: $gap2

      .title-desc
        font-weight: 700
        color: $purple

    .text-bold
      font-weight: bold
</style>