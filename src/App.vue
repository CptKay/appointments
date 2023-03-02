<template>
  <!-- <img alt="Vue logo" src="./assets/logo.png">
  <HelloWorld msg="Welcome to Your Vue.js App"/> -->

  <h1>Welcome to Opportunity</h1>
   <h2>Date</h2>

<!-- footer -->
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'

export default {
  name: 'App',
  data() {
    return {
      title: "Welcome to Opportunity",
      currentDate:"Date",
      entries: [],
    };
  },
  components: {
    HelloWorld
  }
}
</script>

<style>
 @import url('https://fonts.googleapis.com/css2?family=Inter:wght@500;900&display=swap%22');

#app {
  font-family: Inter, Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  /* color: #0F05A0; */
  margin-top: 60px;
  background: #E8EFF4;
}

#h1 {

}

#h2 {
  color: #9AA7B1
  
}

ul.no-bullets {
  list-style-type: none; /* Remove bullets */
  padding: 0; /* Remove padding */
  margin: 0; /* Remove margins */
}

#rectangle {
  width: 960px;
  height: 180px;
  background: #0F05A0;

}

#time {
  color: #EB5E00
}

#text {
  color: #FFBFAB

}


</style>
