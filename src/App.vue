<template>
  <div id="app">
    <header>
      <h1>{{ title }}</h1>
    </header>
    <main>
      <DisplayGif v-bind:pics="pics"/>
    </main>
    <footer>
      <Search label="Input your best phrase" :value="value" v-on:input="input" v-on:tryLuck="tryLuck"/>
    </footer>
  </div>
</template>

<script>
import DisplayGif from './components/DisplayGif.vue'
import Search from './components/Search.vue'

const weekDays = [
  "sunday", "monday", "tuesday", "wednesday", "thursday", "friday", "saturday"
];

export default {
  name: 'app',

  components: {
    DisplayGif,
    Search
  },

  data: function(){
    return {
      pics: [],
      title: "Put gifs in your life and be happier, more productive and a better human being",
      dayOfWeek: new Date().getDay(),
      value: ""
    }
  },

  methods: {
    async search() {
      console.log("searching for " + this.value)
      const response = await fetch(`https://api.giphy.com/v1/gifs/search?api_key=wMovLRQDucFUSRddTHTifdAWNdfp0sOK&limit=20&offset=0&rating=G&lang=en&q=${this.value}`);
      const result = await response.json();
      this.pics = result.data
    },
    input(e) {
      if(e.keyCode === 13) {
        e.preventDefault();
        this.value = e.target.value;
        this.search();
      }
    },
    tryLuck() {
      this.value = `${weekDays[this.dayOfWeek]} ${this.timeOfDay}`;
      this.search()
    }
  },
  computed: {
    timeOfDay: function(){
      const hour = new Date().getHours();
      switch(hour){
        case 6:
        case 7:
        case 8:
        case 9:
        case 10:
          return "morning";
        case 11:
        case 12:
          return "lunch";
        case 13:
        case 14:
        case 15:
        case 16:
          return "day";
        case 17:
        case 18:
        case 19:
        case 20:
        case 21:
          return "evening";
        default:
          return "night";
      }
    }
  }
}
</script>

<style>

html, body {
  margin: 0;
  padding: 0;
}

#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  display: flex;
  flex-flow: column;
  height: 100vh;
  box-sizing: border-box;
}

header {
  flex: 0 0 200px;
  font-size: 1.8vw;
  padding: 0 50px;
}

main {
  flex: 1;
}

footer {
  flex: 0 0 100px;
}

</style>
