<template>
  <div class="wrapper">
    <h1 class="title">timon</h1>
    <p class="sub-title">Lorem ipsum dolor sit amet consectetur.</p>
    <ul class="satan">
      <li class="item first"></li>
      <li class="item"></li>
      <li class="item"></li>
      <li class="item"></li>
      <li class="item"></li>
    </ul>
    <p class="main-text">Lorem ipsum dolor sit, amet consectetur adipisicing elit.</p>

<!-- <div>
      <full-page ref="fullpage" :options="options" id="fullpage">
        <div class="section">First section ...</div>
        <div class="section">Second section ...</div>
      </full-page>
</div> -->

  </div>
</template>

<script>
//import { RouterLink, RouterView } from 'vue-router'
import { gsap } from "gsap";
import { Draggable } from "gsap/Draggable";
import {ScrollTrigger} from "gsap/ScrollTrigger";

import 'vue-fullpage.js/dist/style.css';
//import VueFullPage from 'vue-fullpage.js';

gsap.registerPlugin(ScrollTrigger);
gsap.registerPlugin(Draggable);
// import HelloWorld from './components/HelloWorld.vue'
export default {
    data () {
      return {
      //   options: {
      //   menu: '#menu',
      //   anchors: ['page1', 'page2', 'page3'],
      //   sectionsColor: ['#41b883', '#ff5f45', '#0798ec'],
      // },
      }
    },
    methods:{

      testScroll(){
        let sections = gsap.utils.toArray(".item"),
        currentSection = sections[0];

        ScrollTrigger.normalizeScroll(true);

        gsap.defaults({overwrite: 'auto', duration: 0.5});

        // stretch out the body height according to however many sections there are. 
        gsap.set("body", {height: (sections.length * 100) + "%"});

        // create a ScrollTrigger for each section
        sections.forEach((section, i) => {
          ScrollTrigger.create({
          // use dynamic scroll positions based on the window height (offset by half to make it feel natural)
            start: () => (i - 0.5) * innerHeight,
            end: () => (i + 0.5) * innerHeight,
            // when a new section activates (from either direction), set the section accordinglyl.
            onToggle: self => self.isActive && setSection(section),
            markers: true,
            scrub: true,
            //snap: {snapTo: 0.8, duration: 0, delay: 0, ease: "power1.inOut"}
          });
        });

        // gsap.utils.toArray("[data-speed]").forEach(el => {
        //   gsap.to(el, {
        //     y: function() {return (1 - parseFloat(el.getAttribute("data-speed"))) * (ScrollTrigger.maxScroll(window) - (this.scrollTrigger ? this.scrollTrigger.start : 0))},
        //     ease: "none",
        //     scrollTrigger: {
        //       trigger: el,
        //       start: "top center",
        //       end: "max",
        //       invalidateOnRefresh: true,
        //       scrub: true
        //     }
        //   });
        // });

      function setSection(newSection) {
        if (newSection !== currentSection) {
          gsap.to(currentSection, {autoAlpha: 0})
          gsap.to(newSection, {autoAlpha: 1});
          currentSection = newSection;
        }
    }

    // handles the infinite part, wrapping around at either end....
    ScrollTrigger.create({
      start: 1,
      end: () => ScrollTrigger.maxScroll(window) - 1,
      onLeaveBack: self => self.scroll(ScrollTrigger.maxScroll(window) - 2),
      onLeave: self => self.scroll(2)
        }).scroll(2);
      },
    },
    mounted(){

      this.testScroll();
    }
}
  
</script>

<style lang="scss">

html, body {
  height: 100%;
}
body { 
  font-size: 18px;
  font-weight: 300;
}

#app{
  padding: 0 !important;
  margin: 0;
}
.wrapper{
  .title,
  .sub-title,
  .main-text{
    position: fixed;
    z-index: 999;
  }
  .title{
    font-size: clamp(5rem,20vw,10rem);
    font-weight: 900;
    text-transform: uppercase;
    top: 10px;
    left: 20px;
  }
  .sub-title{
    top: 110px;
    left: 20px;
  }
  .main-text{
    top: 90vh;
    left: 20px;
    max-width: 200px;
  }
  ul{
    list-style: none;
    padding: 0;
    //scroll-snap-type: y mandatory;
    //overflow: hidden;
    li{
      // overflow-y: scroll;
     // scroll-snap-align: start;
      position: fixed;
      width: 100%;
      height: 100%;
      top: 0;
      left: 0;
      &:nth-child(1){
        background-color: red;
      }
      &:nth-child(2){
        background-color: blue;
      }
      &:nth-child(3){
        background-color: green;
      }
      &:nth-child(4){
        background-color: yellow;
      }
      &:nth-child(5){
        background-color: purple;
      }
      &:not(.first) {
      opacity: 0;
      visibility: hidden;
      //transform: scale(0.8);
    } 
    }
  }
}

</style>
