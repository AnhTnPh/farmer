<template>
  <section id="about-section" :class="{'px-12 lg:px-32 py-16 relative':!isMobile, 'w-full flex flex-col mt-4 lg:px-4 px-4' : isMobile }">
    <div class="w-full flex flex-col">
      <span :class="{'text-7xl font-bold': !isMobile, 'text-3xl font-bold' : isMobile}" style="color: #ff4655;">Game</span>
    </div>
    <div id="app" class="wrapper" v-cloak v-bind:class="{ 'is-previous': isPreviousSlide, 'first-load': isFirstLoad }">
      <div class="slide-wrapper" v-for="(slide, index) in slides" :key="index"
        v-bind:class="{ active: index === currentSlide }"
        v-bind:style="{ 'z-index': (slides.length - index), 'background-image': 'url(' + slide.bgImg + ')' }"
        v-on:mouseover="stopRotation" v-on:mouseout="startRotation">
        <div class="w-full text-center" style="position: absolute;top: 50%;" v-if="isMobile">
            <span class="text-white font-bold text-5xl font-semibold">{{ slide.title }}</span>
        </div>
        <div class="slide-inner" >
          <div class="slide-bg-text">
            <p>{{ slide.headlineFirstLine }}</p>
            <p class="text-white">{{ slide.title }}</p>
          </div>
          <!-- <div class="slide-rect-filter">
            <div class="slide-rect" v-bind:style="{ 'border-image-source': 'url(' + slide.rectImg + ')' }"></div>
          </div> -->
          <div class="slide-content">
            <h1 class="slide-content-text">
              <p>{{ slide.headlineFirstLine }}</p>
              <p class="text-white">{{ slide.headlineSecondLine }}</p>
            </h1>
            <!-- <a class="slide-content-cta" style="display: flex;" @click="openLinkServer">Tham gia</a> -->
          </div>
          <h2 class="slide-side-text text-white"><span class="text-white">{{ slide.sublineFirstLine }} / </span><span class="text-white">{{ slide.sublineSecondLine }}</span>
          </h2>
        </div>
      </div>
      <div class="controls-container">
        <button class="controls-button" v-for="(slide, index) in slides" :key="index"
          v-bind:class="{ active: index === currentSlide }" v-on:click="updateSlide(index)" v-on:mouseover="stopRotation"
          v-on:mouseout="startRotation">{{ slide.headlineFirstLine }} {{ slide.title }}</button>
      </div>
      <div class="pagination-container">
        <span class="pagination-item" v-for="(slide, index) in slides" :key="index"
          v-bind:class="{ active: index === currentSlide }" v-on:click="updateSlide(index)" v-on:mouseover="stopRotation"
          v-on:mouseout="startRotation"></span>
      </div>
    </div>
  </section>
</template>

<script>
export default {
  data() {
    return {
      isMobile: false,
      currentSlide: 0,
      isPreviousSlide: false,
      isFirstLoad: true,
      slides: [
        {
          title: 'Valorant',
          headlineFirstLine: "",
          headlineSecondLine: "",
          sublineFirstLine: "Guide by Farmer",
          sublineSecondLine: "Farmer",
          bgImg: "https://wallpapers.com/images/hd/valorant-player-poster-xbh2vt247ch07ps6.jpg",
          rectImg: "https://i.postimg.cc/vTW0XkvM/slide-rect0.jpg"
        },
        {
          title: 'LOL',
          headlineFirstLine: "",
          headlineSecondLine: "",
          sublineFirstLine: "Guide by Farmer",
          sublineSecondLine: "Farmer",
          bgImg: "https://images.contentstack.io/v3/assets/blt370612131b6e0756/bltd897c9a5cef63006/5f9367dacb9eba781f0846fc/LoL_WR_KV_Banner_1920x1080.jpg",
          rectImg: "https://i.postimg.cc/ryWZ8R2b/slide-rect1.jpg"
        },
        {
          title: 'Naraka',
          headlineFirstLine: "",
          headlineSecondLine: "",
          sublineFirstLine: "Guide by Farmer",
          sublineSecondLine: "Farmer",
          bgImg: "https://s1.gaming-cdn.com/images/products/5952/screenshot/naraka-bladepoint-pc-game-steam-wallpaper-1.jpg?v=1669219755",
          rectImg: "https://i.postimg.cc/3JFLGMRF/slide-rect2.jpg"
        },
        {
          title: 'TFT',
          headlineFirstLine: "",
          headlineSecondLine: "",
          sublineFirstLine: "Guide by Farmer",
          sublineSecondLine: "Farmer",
          bgImg: "https://images.alphacoders.com/124/1245848.jpg",
          rectImg: "https://i.postimg.cc/3JFLGMRF/slide-rect2.jpg"
        },
        {
          title: 'Goose Duck',
          headlineFirstLine: "",
          headlineSecondLine: "",
          sublineFirstLine: "Guide by Farmer",
          sublineSecondLine: "Farmer",
          bgImg: "https://images4.alphacoders.com/129/1297942.jpg",
          rectImg: "https://i.postimg.cc/3JFLGMRF/slide-rect2.jpg"
        },
      ]
    }
  },
  mounted: function () {
    var productRotatorSlide = document.getElementById("app");
    var startX = 0;
    var endX = 0;

    productRotatorSlide.addEventListener(
      "touchstart",
      event => (startX = event.touches[0].pageX)
    );

    productRotatorSlide.addEventListener(
      "touchmove",
      event => (endX = event.touches[0].pageX)
    );

    productRotatorSlide.addEventListener(
      "touchend",
      function () {
        var threshold = startX - endX;

        if (threshold < 150 && 0 < this.currentSlide) {
          this.currentSlide--;
        }
        if (threshold > -150 && this.currentSlide < this.slides.length - 1) {
          this.currentSlide++;
        }
      }.bind(this)
    );
    this.startRotation();
    this.checkDevice();
  },
  methods: {
    checkDevice() {
      if( /Android|webOS|iPhone|iPad|iPod|BlackBerry|IEMobile|Opera Mini/i.test(navigator.userAgent) ) this.isMobile = true;
      else this.isMobile = false;
    },
    openLinkServer() {
      window.open("https://discord.gg/farmer-vn", "_blank");
    },
    updateSlide(index) {
      index < this.currentSlide ? this.isPreviousSlide = true : this.isPreviousSlide = false;
      this.currentSlide = index;
      this.isFirstLoad = false;
    },
    startRotation() {
      this.timer = setInterval(this.next, 5000);
    },
    next() {
      this.currentSlide < this.slides.length - 1 ? this.updateSlide(this.currentSlide + 1) : this.updateSlide(0)
    },
    stopRotation() {
      clearTimeout(this.timer);
      this.timer = null;
    }
  }
}
</script>

<style lang="scss">
html {
  box-sizing: border-box;
}

*,
*:before,
*:after {
  box-sizing: inherit;
}

@mixin media($breakpoint) {
  @media (max-width: $breakpoint) {
    @content;
  }
}

@mixin media-min($breakpoint) {
  @media (min-width: $breakpoint) {
    @content;
  }
}

@mixin media-height($breakpoint) {
  @media (max-height: $breakpoint) {
    @content;
  }
}

// ------------- VARIABLES ------------- //
$whitespace-height: 50px;
$left-offset: 13vw;
$rect-width: 48vh;
$rect-height: 62vh;
$rect-border-width: 5vh;
$control-btn-padding: 1.6rem;
$control-active-btn-offset: .3rem;
$left-offset-small: 9vw;
$rect-height-small: 20vw;
$rect-width-small: 16vw;
$rect-border-width-small: 5vh;

// ------------- GENERAL ------------- //
%callout {
  font-family: 'Montserrat';
  text-transform: uppercase;
  color: #fff;
  letter-spacing: .12rem;
  font-size: .7rem;
  line-height: 1;
}

[v-cloak] {
  opacity: 0;
}

body {
  cursor: default;

  ::selection {
    background-color: rgba(46, 49, 52, .7);
    color: #f5f5f1;
  }

  ::-moz-selection {
    background-color: rgba(46, 49, 52, .7);
    color: #f5f5f1;
  }
}

.wrapper {
  height: calc(100vh - #{$whitespace-height});
  min-height: 36rem;
  position: relative;

  @include media(630px) {
    height: 100vh;
    min-height: 0;
  }
}

// ------------- SLIDES ------------- //
.slide {
  &-wrapper {
    background-size: cover;
    height: 100%;
    background-position: center center;
    position: absolute;
    width: 100%;
    background-blend-mode: darken;

    // &:nth-child(1) {
    //   background-color: rgba(115, 129, 153, .4);

    //   &:before {
    //     background-color: rgba(115, 129, 153, .25);
    //   }

    //   .slide-content-text {
    //     text-shadow: 2px 5px 45px rgba(85, 96, 113, 0.25);
    //   }
    // }

    // &:nth-child(2) {
    //   background-color: rgba(144, 171, 184, .7);

    //   &:before {
    //     background-color: rgba(144, 171, 184, .3);
    //   }

    //   .slide-content-text {
    //     text-shadow: 2px 5px 45px rgba(121, 142, 152, 0.2);
    //   }
    // }

    // &:nth-child(3) {
    //   background-color: rgba(86, 125, 156, .5);

    //   &:before {
    //     background-color: rgba(86, 125, 156, 0.2);
    //   }

    //   .slide-content-text {
    //     text-shadow: 2px 5px 55px rgba(57, 83, 103, 0.4);
    //   }
    // }

    &:before {
      content: "";
      position: absolute;
      width: 100%;
      height: 100%;
      z-index: 1;
    }
  }

  &-inner {
    position: relative;
    z-index: 2;
    height: 100%;
    overflow: hidden;
  }

  &-bg-text {
    font-family: 'Playfair Display';
    color: #000;
    font-size: 42vh;
    line-height: .8;
    opacity: .03;
    font-weight: 900;
    margin-top: -4rem;
    position: absolute;
    top: 50%;
    left: 5vw;
    transform: translateY(-50%);

    >p:last-child {
      padding-left: 4rem;
    }
  }

  &-content {
    color: #fff;
    margin-top: 5rem;
    position: absolute;
    top: 50%;
    left: calc(#{$left-offset} + (.7) * #{$rect-width});
    transform: translateY(-50%);
    display: flex;
    flex-direction: column;

    @include media(1000px) {
      left: calc(#{$left-offset} + 1rem);
    }

    @include media-height(730px) {
      top: 30%;
      transform: translateY(-30%);
      left: calc(#{$left-offset-small} + (.7) * #{$rect-width-small});
    }

    &-text {
      font-family: 'Playfair Display';
      font-size: 9rem;
      letter-spacing: .2rem;
      line-height: .87;
      font-weight: 700;
      will-change: auto;

      @include media-height(790px) {
        font-size: 7rem;
      }

      @include media(1150px) {
        font-size: 7rem;
      }

      @include media(840px) {
        font-size: 5.5rem;
      }

      @include media(630px) {
        margin-bottom: 5.5rem;
      }

      @include media(500px) {
        font-size: 3.5rem;
      }

      >p:last-child {
        padding-left: 3rem;
      }
    }

    &-cta {
      @extend %callout;
      cursor: pointer;
      align-self: flex-start;
      margin-top: 4.5rem;
      margin-left: calc((.3) * 48vh + 4.5rem);
      padding: .9rem 2.2rem;
      border-left: 1px solid #fff;
      border-right: 1px solid #fff;
      transition: .18s ease-in-out;
      font-weight: 700;

      @include media(1000px) {
        background-color: rgba(255, 255, 255, .3);
        padding-top: 1.2rem;
        padding-bottom: 1.2rem;
      }

      @include media(630px) {
        display: none;
      }

      &:hover {
        color: #000;
        background-color: #fff;
      }
    }
  }

  &-rect {
    height: $rect-height;
    width: $rect-width;
    border-image-slice: 10%;
    position: absolute;
    top: 50%;
    transform: translateY(-50%);
    left: $left-offset;
    border-width: $rect-border-width;
    border-style: solid;
    box-shadow: 2px 2px 90px 30px rgba(41, 50, 61, 0.22);
    will-change: auto;

    @include media-height(790px) {
      left: $left-offset-small;
      height: $rect-height-small;
      width: $rect-width-small;
      border-width: $rect-border-width-small;
    }

    @include media-height(730px) {
      top: 30%;
      transform: translateY(-30%);
    }

    &-filter {
      filter: brightness(110%) contrast(110%) saturate(110%);
    }
  }

  &-side-text {
    @extend %callout;
    position: absolute;
    left: calc(#{$left-offset} - 3rem);
    writing-mode: vertical-rl;
    top: calc((50% - (#{$rect-height} / 2)) + (#{$rect-border-width} / 2));

    @include media-height(790px) {
      left: calc(#{$left-offset-small} - 3rem);
      top: calc((50% - (#{$rect-height-small} / 2)) + (#{$rect-border-width-small} / 2));
    }

    @include media-height(730px) {
      top: calc((40% - (#{$rect-height-small} / 2)) + (#{$rect-border-width-small} / 2));
    }

    >span:first-child {
      font-weight: 700;
    }

    &:after {
      content: "";
      width: 1px;
      background-color: #fff;
      height: 40px;
      display: block;
      position: absolute;
      top: calc(100% + 25px);
      left: 50%;
      transform: translateX(-50%);
    }
  }
}

// ------------- CONTROLS ------------- //
.controls {
  &-container {
    position: absolute;
    z-index: 200;
    display: flex;
    bottom: 0;
    right: 0;
    align-items: flex-end;

    @include media(630px) {
      display: none;
    }
  }

  &-button {
    @extend %callout;
    cursor: pointer;
    background-color: rgba(208, 206, 204, .32);
    border: 0;
    padding: $control-btn-padding 2.2rem;
    flex-basis: 0;
    flex-grow: 1;
    min-width: 15rem;
    transition: .25s ease-in-out;
    outline: 0;

    @include media(730px) {
      padding: 1.2rem 1.4rem;
      min-width: 13rem;
    }

    &:not(.active) {
      &:hover {
        color: #000;
        background-color: #fff;
      }
    }

    &.active {
      cursor: default;
      font-weight: 700;
      background-color: #3b3e45;
      padding-top: $control-btn-padding + $control-active-btn-offset;
      padding-bottom: $control-btn-padding + $control-active-btn-offset;
      margin-bottom: -$control-active-btn-offset;
      position: relative;

      @include media(730px) {
        padding-top: 1.4rem;
        padding-bottom: 1.4rem;
        margin-bottom: -0.15rem;
      }

      &:after {
        content: "";
        background-color: #e3e3e3;
        height: 5px;
        width: calc(100% - 8px);
        position: absolute;
        top: 100%;
        left: 4px;
      }
    }

    &:not(.active)+& {
      border-left: 1px solid rgba(255, 255, 255, .2);
    }
  }
}

// ------------- PAGINATION ------------- //
.pagination {
  &-container {
    position: absolute;
    z-index: 200;
    display: flex;
    flex-direction: column;
    align-items: flex-end;
    right: 2rem;
    top: 50%;
    transform: translateY(-50%);

    @include media(920px) {
      display: none;
    }
  }

  &-item {
    width: 30px;
    height: 1px;
    background-color: rgba(255, 255, 255, .6);
    transition: .18s ease-in-out;

    &+& {
      margin-top: 1rem;
    }

    &.active {
      background-color: #fff;
      position: relative;
      transform: translateX(-.6rem);
      width: 35px;

      &:after {
        content: "";
        height: 4px;
        width: 2px;
        border-radius: 35%;
        background-color: #fff;
        display: inline-block;
        position: absolute;
        right: 0;
        top: 50%;
        transform: translateX(.6rem) translateY(-50%);
      }
    }

    &:not(.active) {
      cursor: pointer;

      &:hover {
        background-color: #fff;
        width: 35px;
      }
    }
  }
}

// ------------- ANIMATION EFFECT ------------- //
$slide-swipe: .9s;
$text-cut-up: .5s;

@keyframes slideLeft {
  from {
    transform: translateX(0);
  }

  to {
    transform: translateX(-100%);
  }
}

@keyframes slideRight {
  from {
    transform: translateX(-100%);
  }

  to {
    transform: translateX(0);
  }
}

@keyframes cutTextUp {
  from {
    clip-path: inset(0 0 -10% 0);
  }

  to {
    clip-path: inset(0 0 100% 0);
  }
}

@keyframes cutTextDown {
  from {
    clip-path: inset(100% 0 0 0);
  }

  to {
    clip-path: inset(-10% 0 -20% 0);
    opacity: 1;
  }
}

@keyframes cutTextDownFromTop {
  from {
    clip-path: inset(0 0 100% 0);
  }

  to {
    clip-path: inset(0 0 -30% 0);
    opacity: 1;
  }
}

@keyframes rectMovement {
  0% {
    transform: translateX(0) rotate(0) translateY(-50%);
  }

  60% {
    opacity: 1;
  }

  100% {
    transform: translateX(calc(-#{$rect-width} + -#{$left-offset})) rotate(12deg) translateY(-50%);
    opacity: 0;
  }
}

@include media-height(730px) {
  @keyframes rectMovement {
    0% {
      transform: translateX(0) rotate(0) translateY(-30%);
    }

    60% {
      opacity: 1;
    }

    100% {
      transform: translateX(calc(-#{$rect-width} + -#{$left-offset})) rotate(12deg) translateY(-30%);
      opacity: 0;
    }
  }
}

@keyframes rectMovementFromRight {
  0% {
    transform: translateX(calc(#{$rect-width})) rotate(12deg) translateY(-50%);
    opacity: 0;
  }

  60% {
    opacity: 1;
  }

  100% {
    transform: translateX(0) rotate(0) translateY(-50%);
    opacity: 1;

    @include media-height(730px) {
      transform: translateX(0) rotate(0) translateY(-30%);
    }
  }
}

@include media-height(730px) {
  @keyframes rectMovementFromRight {
    0% {
      transform: translateX(calc(#{$rect-width})) rotate(12deg) translateY(-30%);
      opacity: 0;
    }

    60% {
      opacity: 1;
    }

    100% {
      transform: translateX(0) rotate(0) translateY(-30%);
      opacity: 1;
    }
  }
}

@keyframes rectMovementRight {
  0% {
    transform: translateX(calc(-#{$rect-width} + -#{$left-offset})) rotate(12deg) translateY(-50%);
  }

  40% {
    opacity: 1;
  }

  100% {
    transform: translateX(0) rotate(0) translateY(-50%);
    opacity: 1;

    @include media-height(730px) {
      transform: translateX(0) rotate(0) translateY(-30%);
    }
  }
}

@include media-height(730px) {
  @keyframes rectMovementRight {
    0% {
      transform: translateX(calc(-#{$rect-width} + -#{$left-offset})) rotate(12deg) translateY(-30%);
    }

    40% {
      opacity: 1;
    }

    100% {
      transform: translateX(0) rotate(0) translateY(-30%);
      opacity: 1;
    }
  }
}

@keyframes fadeIn {
  from {
    opacity: 0;
  }

  to {
    opacity: 1;
  }
}

.slide-wrapper {
  opacity: 0;
  transition-delay: $slide-swipe + $text-cut-up;
  transition-duration: 0s;
  transition-property: opacity;
  will-change: opacity, transform;

  &:not(.active) {
    animation-delay: $text-cut-up;
    animation-name: slideLeft;
    animation-duration: $slide-swipe;
    animation-timing-function: cubic-bezier(0.18, 0.54, 0.52, 0.93);
    pointer-events: none;

    .slide-content-text>p,
    .slide-side-text {
      animation-name: cutTextUp;
      animation-duration: $text-cut-up;
      animation-timing-function: ease-out;
    }

    .slide-rect {
      animation-name: rectMovement;
      animation-duration: $text-cut-up;
      animation-timing-function: ease;
      animation-fill-mode: forwards;
    }
  }

  &.active {
    transition-delay: 0s;
    opacity: 1;

    .slide-content-text>p {
      opacity: 0;
      animation-delay: $text-cut-up + .3s;
      animation-name: cutTextDown;
      animation-duration: $text-cut-up;
      animation-timing-function: ease;
      animation-fill-mode: forwards;
    }

    .slide-rect {
      opacity: 0;
      animation-name: rectMovementFromRight;
      animation-duration: $text-cut-up - .05s;
      animation-timing-function: ease;
      animation-fill-mode: forwards;
      animation-delay: $slide-swipe;
    }
  }

  .is-previous & {
    &:not(.active) {
      animation: none;

      .slide-rect {
        animation: none;
      }
    }

    &.active {
      transform: translateX(-100%);
      animation-fill-mode: forwards;
      animation-delay: $text-cut-up;
      animation-name: slideRight;
      animation-duration: $slide-swipe - .1s;
      animation-timing-function: cubic-bezier(0.18, 0.54, 0.52, 0.93);

      .slide-rect {
        opacity: 0;
        animation-name: rectMovementRight;
        animation-duration: $text-cut-up;
        animation-timing-function: ease-out;
        animation-fill-mode: forwards;
        animation-delay: $slide-swipe;
      }
    }
  }
}

.first-load {

  .slide-wrapper.active .slide-side-text,
  .slide-wrapper.active .slide-content-cta,
  .slide-wrapper.active .slide-rect,
  .controls-container {
    opacity: 0;
    animation-name: fadeIn;
    animation-delay: .3s;
    animation-duration: .3s;
    animation-fill-mode: forwards;
    animation-timing-function: ease-in;
  }

  .slide-wrapper.active .slide-content-text>p {
    animation-name: fadeIn;
    animation-delay: $text-cut-up;
    animation-duration: $text-cut-up + .2s;
  }
  .control-slider {
    display: grid !important;
  }
}</style>