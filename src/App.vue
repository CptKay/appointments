<template>

  <h1 class="site-title">{{ title }}</h1>
  <span class="site-description">{{ currentDate }}</span>
  

<!-- entry list-->

<ul v-if="entries && entries.length" class="entry-list">
  <li class="entry-item" v-for="entry in entries" :key="entry.id" >
  <!-- 
    <span class="entry-daytime">{{ entry[0]+++ }} Uhr, {{ entry[1].replaceAll("/", ".") }}</span><br />
  <h3 class="entry-title">{{ entry[2] }}</h3>
  <span class="entry-description">{{ entry[3] }}</span><br /> 
-->

<EventEntry :entry="entry" />
</li>
</ul>

<h1 v-else>Zur Zeit kein Ereignis</h1>

   

<!-- footer -->

<footer>
        
            <a href="https://www.stadt-zuerich.ch/sd/de/index/ueber_das_departement/organisation/seb.html"><img src="../src/assets/STZH_SEB_Logo.png" alt=""></a>
            <a href="https://opportunity.stiftung-sag.ch/"><img src="../src/assets/Opportunity.png" alt=""></a>
            <a href="https://www.stiftung-sag.ch/de/willkommen/"><img class="footer-right" src="../src/assets/SAG_Logo_De.png" alt=""></a>
          

    </footer>

</template>

<script>
import EventEntry from './components/EventEntry.vue'

import axios from "axios";

export default {
  name: 'App',
  components: { EventEntry },
  data() {
    return {
      title: "Welcome to Opportunity",
      currentDate: "",
      /* sheet_id: "1CR1UKN0LAPNs6lWbfA2gBI2FazmWdVSFIzIwi5TG5Z4",
      api_token: "AIzaSyA-qeDXOhEeQDA0vQf7LgkF7DQtGnAtmAU", */
      sheet_id: "1-KaU9mi6Av4fYc7vjZxkMr0wpxT8SuldCIldW-YphxA",
      api_token: "AIzaSyCuQ7WL9T-Urn0BeWuYjvvVHFPsIrDBl7U",
      entries: [],
    };
  },
  computed: {
	gsheet_url() {
return `https://sheets.googleapis.com/v4/spreadsheets/${this.sheet_id}/values:batchGet?ranges=A2%3AE100&valueRenderOption=FORMATTED_VALUE&key=${this.api_token}`;
},
},
 
  methods: {
    /* getData() {
      this.entries = [
        ["08:30" , "event 0" , "title 0" , "description 0"],
        ["09:30" , "event 1" , "title 1" , "description 1"]
      ];
    }, */

    getData() {
      axios.get(this.gsheet_url).then((response) => {
        // this.entries = response.data.valueRanges[0].values;
        const rows = response.data.valueRanges[0].values;
    const currentDate = new Date();
    const filteredRows = rows.filter(row => {
      const dateParts = row[1].split("/");
      const rowDate = new Date(`${dateParts[2]}-${dateParts[1]}-${dateParts[0]}`);
      return rowDate >= currentDate;
      });
      this.entries = filteredRows.sort((row1, row2) => {
      const dateParts1 = row1[1].split("/");
      const dateParts2 = row2[1].split("/");
      const date1 = new Date(`${dateParts1[2]}-${dateParts1[1]}-${dateParts1[0]}`);
      const date2 = new Date(`${dateParts2[2]}-${dateParts2[1]}-${dateParts2[0]}`);
      return date1 - date2;
    });
  });

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
    setInterval(this.refreshData,18000000);
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
  margin-top: 37px;
  margin-left: 07%;
  }

 body {
background: #E8EFF4;
display: block;
height: 130px;  
}

h1 {
    font-weight: 900;
    font-size: 62px;
    color: #323D4A;
}

.site-description {
    font-weight: 500;
    font-size: 62px;
    line-height: 1px;
  color: #9AA7B1
  }

ul {
  list-style-type: none; /* Remove bullets */
  font-size: 28px;
  margin:0;
  /* margin-bottom:150px; */
  padding:0;
}

li {
  width: 88%;
  margin-top: 2.5%;
  padding: 2.5%;
  background: #0F05A0;
}

.entry-daytime {
    font-weight: 900;
    padding-top:  37px;
  color: #EB5E00;
}

h3 {
    font-weight: 700;
  color: #FFBFAB;
  line-height: 5px;
  }

.entry-description {
    font-weight: 100;
  color: #FFBFAB;
  line-height: auto;
}

footer {
  display: flex;
  justify-content: space-between;
  position: fixed;
  bottom: 0;
  left: 0;
  width: 100%;
  padding: 40px;
  background: #FFF;   
}

img {
height: 50px;
}
</style>
