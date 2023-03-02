<template>
  <div id="app">

  <h1 class="site-title">{{ title }}</h1>
  <span class="site-description">{{ currentDate }}</span>
  

<!-- entry list-->

<ul v-if="entries" class="entry-list">
  <li class="entry-item" v-for="entry in entries" :key="entry.id" >
  <span class="entry-daytime">{{ entry[0] }} Uhr, {{ entry[1].replaceAll("/", ".") }}</span><br />
  <h3 class="entry-title">{{ entry[2] }}</h3>
  <span class="entry-description">{{ entry[3] }}</span><br />
</li>
<!-- <li class="entry-item">
  <li class="entry-item"></li>
  <span class="entry-daytime">{{ currentDate }}</span><br />
  <h3 class="entry-title">{{ title }}</h3>
  <span class="entry-description">{{ currentDate }}</span><br />
</li> -->

</ul>

<h1 v-else>Zur Zeit kein Ereignis</h1>

   

<!-- footer -->

<footer>
        <div class="row">
            <div class="column"><img src="assets/STZH_SEB_Logo.png" alt=""></div>
            <div class="column"><img src="assets/Opportunity.png" alt=""></div>
            <div class="column footer-right"><img class="footer-right" src="assets/images/SAG_Logo_De.png" alt=""></div>
          </div>

    </footer>

</div>

</template>

<script>
// import HelloWorld from './components/HelloWorld.vue'

export default {
  name: 'App',
  data() {
    return {
      title: "Welcome to Opportunity",
      currentDate: "",
      entries: [],
    };
  },
  methods: {
    getData() {
      this.entries = [
        ["08:30" , "event 0" , "title 0" , "description 0"],
        ["09:30" , "event 1" , "title 1" , "description 1"]
      ];
    },
    updateCurrentDate() {
      let today = new Date();
      this.currentDate = `${today.getDate()}.${today.getMonth() +1}.${today.getFullYear()}`;
    },
    refreshData() {
      this.updateCurrentDate();
      this.getData();

  },
  },
  mounted() {
    this.refreshData();
    setInterval(this.refreshData,180000000);
  },
};
</script>

<style>
  @import url('https://fonts.googleapis.com/css2?family=Inter:wght@500;900&display=swap%22');

/* body{ min-height:100vh; margin:0; position:relative; } */
#app {
  font-family: Inter, Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  /* text-align: center; */
  /* color: #0F05A0; */
  margin-top: 37px;
  margin-left: 40px;
  background: #E8EFF4;
  /* position: relative; */

}

/*  body::after {
content: '';
display: block;
height: 130px;  
}
*/

h1 {
    font-weight: 900;
    font-size: 62px;
    color: #323D4A;

}

.site-description {
    font-weight: 500;
    font-size: 62px;
  color: #9AA7B1
  
}

ul {
  list-style-type: none; /* Remove bullets */
  font-size: 28px;
   /* Remove padding */
  /* margin-top:  37px; */
  line-height: 6px;
}

li {
  width: 88%;
  height: 180px;
  background: #0F05A0;

}

.entry-daytime {
    font-weight: 900;
    padding-top:  37px;
  color: #EB5E00;
  
  /* margin-left:  40px; */
}

h3 {
    font-weight: 700;
  color: #FFBFAB;
  

}

.entry-description {
    font-weight: 100;
  color: #FFBFAB;

}

footer {
    /* margin-bottom: -100px; */
    display:flex;
    justify-content: space-between;
    box-sizing: border-box;
    bottom: 0px;
    left: 0;
    position: fixed;
    /* height: 130px; */
    padding: 40px;
    width: 99%;
    background-color: #ffffff;
    /* clear: both; */
    
}

.column {
float: left;
width: 33.33%;
}

/* Clear floats after the columns */
/* .row:after {
content: "";
display: table;
clear: both;
} */

img {

height: 50px;


}

.footer-right {
float: right;
}


</style>
