<template lang="pug">
  .wrapper
    Header
    section.sec-1
      .banner
        img(src="images/default-2.jpg")
      .desc
        h2.title-desc {{ snapshot.title}}
        p.pt-2 {{ snapshot.description }}
      
      ul(v-for="location in snapshot.locations")
        li {{ location.name }}
      
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
      }
    },
    computed: {
    },
    mounted() {
       this.getSnapshot();
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
                    this.locations = data.locations;
                }
          });
        },
        getLocations() {
          
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
        color: #424874

    .text-bold
      font-weight: bold
</style>