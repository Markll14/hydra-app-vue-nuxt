<template>
  <div class="carousel">
    <component
      :is="slickComp"
      ref="slick" 
      :options="slickOptions"
    >
      <nuxt-link v-for="card in imageUrl" :to="'/explore'" :key="card.id">
        <img class="carousel__img" :src="card" alt="">
      </nuxt-link>
        

    </component>
  </div>
</template> 

<script> 
import {db} from '@/firebase/init.js'
import '../../node_modules/slick-carousel/slick/slick.css';
import '../../node_modules/slick-carousel/slick/slick-theme.css';
  export default {
    data: () => ({
      imageUrl: [],
        'slickComp': '',
        slickOptions: {
            slidesToShow: 3,
            infinite: true,
            slidesToScrol: 1,
            dots: true,
            centerMode: true
        }
    }),
    components: {
        Slick: () => import('vue-slick'),
        db
    },
    mounted: function () {
        this.$nextTick(function () {
           this.slickComp = 'Slick'
        })
    },
      created(){
        this.$store.state.loadedCards.forEach( (doc) => {

          this.imageUrl.push(doc.imageurl[0])
        })
        
    },
        methods: {
        next() {
            this.$refs.slick.next();
        },
 
        prev() {
            this.$refs.slick.prev();
        }
    }
  }
</script>

<style lang="scss" scoped>

    .carousel {
        overflow: hidden;

        &__img {
          height: 20rem;
          width: 40rem;
        }
    }

</style>


