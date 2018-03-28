<template>
  <div class="slider" v-bind:style="{width: sliderWidth + 'px' }">
    <div class="slides-inner" ref="carouselslider" v-bind:style="{width: innerWidth+'px', marginLeft:- +slidesInnerMarginLeft +'px', visibility: active }">
        <Slide v-bind:style="{width: singleWidth+'px' }" v-for="slide in slides" :key="slide.index" v-bind:slide="slide"></Slide>
    </div>
    <ul class="points">
    <div v-if="pointsWrap = pointsWrap" ref="pointsWrap" :style="{height: pointsWrapHeight +'px' }" class="pointsWrap pull-left">
           <div> <span @click="prevSlide" class="nxtpre glyphicon glyphicon-chevron-left"></span></div>
      </div>      
    <div class="dots"><li v-if="point = point" v-for="(slide,index) in slides" v-bind:class="[index === currentIndex ? 'active' : '']"><a v-bind:class="{point:point}" v-on:click="goToSlide(index)"> {{ index+1 }} </a></li></div>
    <div ref="pointsWrap" v-if="pointsWrap = pointsWrap" :style="{height: pointsWrapHeight +'px' }" class="pointsWrap pull-right">
      <div><span @click="nextSlide" class="nxtpre glyphicon glyphicon-chevron-right"></span></div>
      </div>
  </ul>
  </div>
</template>

<script>
import Slide from './Slide'
export default {
  name: 'HelloWorld',
  props:{
    itemsPerSlide: {
      default: 1,
    },
    sliderWidth: {
      default: 1000,
    },
    autoplay: {
      default:3000
    },
    bulletPoint: {
      default:false
    }
  },
  data () {
    return {
      msg: 'Welcome to Your Vue carousel Slider App.',
      slides: [
                {src:'static/images/slide1.jpg', alt:'Slide 1'},
                {src:'static/images/slide2.jpg', alt:'Slide 2'},
                {src:'static/images/slide3.jpg', alt:'Slide 3'},
                {src:'static/images/slide4.jpg', alt:'Slide 4'},
                {src:'static/images/slide5.jpg', alt:'Slide 5'}
      ],
      innerWidth: 0,
      bullet:0,
      point: false,
      active: 'visible',
      singleWidth: 0,
      pointsWrap:true,
      pointsWrapHeight:0,
      InnerMarginLeft:0,
      currentIndex: 0,
      nextSlideIndex: 0,
      prevSlideIndex: 0
    }
  },
  created: function() {
  window.addEventListener('load', () => {
    this.pointsWrapHeight = this.$el.clientHeight
  })
  },
  computed : {
    slidesInnerMarginLeft () {
      return this.currentIndex * this.singleWidth
    },
  },
  methods: {
    getHeight: function() {
      console.log(this.$el.clientHeight)
    },
    prevSlide() {
      if (this.currentIndex === 0) {
        return
      }
      this.currentIndex--
    },
    onResize(event) {
      if (this.$parent.$el.clientWidth < this.sliderWidth) {
          let singleWidth = this.$parent.$el.clientWidth/this.itemsPerSlide
          this.singleWidth = singleWidth
          this.innerWidth = singleWidth * this.slides.length
    }
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
    console.log(this)
    if (this.bulletPoint) {
      this.point = true
    }
    if (this.$parent.$el.clientWidth < 650) {
      this.point = false
      this.pointsWrap = false
    }
    if (this.$parent.$el.clientWidth < this.sliderWidth) {
    let singleWidth = this.$parent.$el.clientWidth/this.itemsPerSlide
    this.singleWidth = singleWidth
    this.sliderWidth = this.$parent.$el.clientWidth
    this.innerWidth = singleWidth * this.slides.length
    } else {    
    let singleWidth = this.$el.clientWidth/this.itemsPerSlide
    this.singleWidth = singleWidth
    this.innerWidth = singleWidth * this.slides.length
   }
    setInterval(this.loadData, this.autoplay)
    window.addEventListener('resize', this.onResize)
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.slides-inner{
  transition: margin 0.6s ease-out;
}.dots {
    position: absolute;
    width: 100%;
    bottom: 0;
}
.slider {
    overflow: hidden;
    margin: 0 auto;
    position: relative;
}
.slider .nxtpre.glyphicon-chevron-right {
    float: right;
    right: 5px;
}.slider .nxtpre.glyphicon-chevron-left {
    float: left;
    left: 5px;
}.pointsWrap div {
    display: table-cell;
    vertical-align: middle;
}.pointsWrap {
    display: table;
}
.nxtpre{
  color: #fff;
  font-size: 35px;
  padding: 0;
  background: transparent !important;
  border: 0;
}.points .active .point {
    background: #ffffff;
}
.slider .points a.point {
    float: none;
    padding: 5px;
    font-size: 0;
    border-radius: 50%;
    margin: 0 3px;
    border: 2px solid;
}

.slider.full{
  width: 100% !important;
}
ul.points {
    margin: 0;
    padding: 0;
    position: absolute;
    bottom: 5px;
    width: 100%;
}ul.points li {
    list-style: none;
    display: inline-flex;
}
</style>
