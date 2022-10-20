<template>
  <div>
    <Navbar />
    <h1>API Tracking route</h1>
    <p class="title">Choisissez une période pour commencer</p>
    <div class="date">
      <ChooseDate class="date1" @chooseDate="chooseDate2" />
      <ChooseDate class="date2" @chooseDate="chooseDate2" />
    </div>
    <div class="card-deck">
      <Appel  v-bind:nbappel="nbappel" v-bind:periode="periode" />
    </div>
    <!--
    <div class="graphconnexion">
      <GraphConnexion/>
    </div>
    <div class="graphroute">
      <GraphRoute/>
    </div>
    -->
  </div>
</template>

<script>
import axios from 'axios'
import Appel from '../components/Appel.vue'
import GraphConnexion from '../components/GraphConnexion.vue'
import GraphRoute from '../components/GraphRoute.vue'
import ChooseDate from '../components/ChooseDate.vue'
import Navbar from '../components/Navbar.vue'

export default {
  name: 'IndexPage',
  components: {
    Appel,
    GraphConnexion,
    GraphRoute,
    ChooseDate,
    Navbar
  },
  data () {
    return {
      nbappel: 0,
      periode: 0
    }
  },
  methods: {
    /*connexion à l'API à l'aide du token de connexion*/
    fetchItems: function () {
      axios.get('https://api-buildings.homeys.io/api/tracking', {
        headers: {
          'Authorization': 'Bearer ' + this.process.env.Tokenconnexions
        }
      })
        .then(response => {
          this.nbappel = response[0].count
          this.periode = response[0].date
        })
        .catch(error => {
          console.log(error)
        })
    },
    created () {
      this.fetchItems()
    }
  }
}
</script>

<style scoped> 
/* title h1 and class title */
h1 {
  text-align: center;
}
.title {
  text-align: center;
}

/* card deck */
.card-deck {
  display: flex;
  flex-flow: row wrap;
  justify-content: center;
  align-items: center;
  align-content: center;
}

/* date */
.date {
  align-content: center;
}
</style>
