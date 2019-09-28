<template>
  <div>
    <div v-if="pic" class="result">
      <div class="image">
        <img :src="pic.images.downsized_large.url" :alt="pic.title">
      </div>
      <div class="next">
        <button v-on:click="shuffle">Next</button>
      </div>
    </div>
    <!--ul>
      <li v-for="pic in pics"><img :src="pic.images.fixed_height.url" :alt="pic.title"></li>
    </ul-->
  </div>
</template>

<script>
import { random } from 'lodash';

export default {
  name: 'DisplayGif',

  props: {
    pics: Array
  },

  data: function(){
    return { idx: 0 }
  },

  created: function(){
    this.shuffle();
  },

  methods: {
    shuffle: function(){
      this.idx = random(0, this.pics.length-1)
    }
  },

  computed: {
    pic: function() {

      if(this.idx < 0) {
        this.shuffle();
      }

      return this.pics[this.idx];
    }
  }
}
</script>

<style scoped>

  .result {
    display: block;
    text-align: center;
  }

  .image, .next {
    display: inline-block;
    vertical-align: middle;
  }

  .image {
    width: 60%;
    margin-left: 60px;
    height: 480px;
    position: relative;
  }

  .image img {
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
  }

  .next {
    width: 60px;
  }

  li {
    display: inline-block;
    vertical-align: middle;
  }
</style>
