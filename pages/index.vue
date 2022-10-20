<template>
  <div>
    <Navbar />
    <h1>API Tracking route</h1>
    <p class="title">Choisissez une période pour commencer</p>
    <div class="card-deck">
      <Appel  nbappel="100" periode="2019"/>
    </div>
    <div class="graphconnexion">
      <GraphConnexion/>
    </div>
    <div class="graphroute">
      <GraphRoute/>
    </div>
  </div>
</template>

<script>
import axios from 'axios'
import Appel from '../components/Appel.vue'
import GraphConnexion from '../components/GraphConnexion.vue'
import GraphRoute from '../components/GraphRoute.vue'
import Navbar from '../components/Navbar.vue'

export default {
  name: 'IndexPage',
  components: {
    Appel,
    GraphConnexion,
    GraphRoute,
    Navbar
  },
  data () {
    return {
      nbappel: 0,
      periode: 0
    }
  },
  methods: {
    fetchItems: function () {
      axios.get('api-buildings.homeys.io/api/tracking').then(response => {
        this.nbappel = response.data.nbappel
        this.periode = response.data.periode
      })
    }
  },
  created () {
    this.fetchItems()
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
</style>
