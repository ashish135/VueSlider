<template>
  <div class="slider">
    <div class="slides-inner" v-bind:style="{width: innerWidth+'px', marginLeft:- +slidesInnerMarginLeft +'px', visibility: active }">
        <Slide v-bind:style="{width: singleWidth+'px' }" v-for="slide in slides" v-bind:slide="slide"></Slide>
    </div>
    <ul class="pagination">
      <li><a @click="prevSlide" class="btn btn-primary">Prev</a></li>
    <li v-for="(slide,index) in slides" v-bind:class="[index === currentIndex ? 'active' : '']"><a v-on:click="goToSlide(index)"> {{ index+1 }} </a></li><li><a @click="nextSlide" class="btn btn-primary">Next</a></li>
  </ul>
  </div>
</template>

<script>
import Slide from './Slide'
export default {
  name: 'HelloWorld',
  data () {
    return {
      msg: 'Welcome to Your Vue carousel Slider App',
      slides: [
                {src:'static/images/slide1.jpg', alt:'Slide 1'},
                {src:'static/images/slide2.jpg', alt:'Slide 2'},
                {src:'static/images/slide3.jpg', alt:'Slide 3'},
                {src:'static/images/slide4.jpg', alt:'Slide 4'},
                {src:'static/images/slide5.jpg', alt:'Slide 5'}
      ],
      innerWidth: 0,
      bullet:0,
      active: 'visible',
      singleWidth: 0,
      InnerMarginLeft:0,
      currentIndex: 0,
      nextSlideIndex: 0,
      prevSlideIndex: 0
    }
  },
  props:{
    itemsPerSlide: {
      default: 1,
    }
  },
  computed : {
    slidesInnerMarginLeft () {
      return this.currentIndex * this.singleWidth
    }
  },
  methods: {
    prevSlide() {
      if (this.currentIndex === 0) {
        return
      }
      this.currentIndex--
    },
    nextSlide() {
      if (this.currentIndex == this.slides.length-1) {
        return
      }
      this.currentIndex++
    },
    goToSlide(i) {
      this.currentIndex = i
    },
    loadData () {
      if (this.currentIndex === 4) {
        this.active = 'hidden'
        this.currentIndex = 0
        this.active = 'visible'
      } else {
      this.currentIndex++
    }
    }
  },
  components:{
    Slide
  },
  mounted () {
    let singleWidth = this.$el.clientWidth/this.itemsPerSlide
    this.singleWidth = singleWidth
    this.innerWidth = singleWidth * this.slides.length
    setInterval(this.loadData, 3000)
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.slides-inner{
  transition: margin 0.6s ease-out;
}
.slider {
    overflow: hidden;
}
.pagination a{
  cursor: pointer;
}
</style>
