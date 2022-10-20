<!--Graphique avec plusieurs courbes (une courbe par type de route) représentant le nombre de connexions par jour par type de route.-->
<template>
    <div>
        <h2>Nombre de connexions par jour par type de route</h2>
        <div class="graph">
        <canvas id="myChart" width="400" height="400"></canvas>
        </div>
    </div>
</template>

<script>
import axios from 'axios'
import { Line } from 'vue-chartjs'

export default {
    name: 'GraphRoute',
    extends: Line,
    data () {
        return {
            datacollection: {
                labels: [],
                datasets: [
                    {
                        label: 'Nombre de connexions',
                        backgroundColor: '#f87979',
                        data: []
                    }
                ]
            },
            options: {
                legend: { display: false },
                title: {
                    display: true,
                    text: 'Nombre de connexions par jour par type de route'
                },
                responsive: true,
                maintainAspectRatio: false
            }
        }
    },
    methods: {
        fetchItems: function () {
            axios.get('api-buildings.homeys.io/api/tracking').then(response => {
                for (var i = 0; i < response.data.length; i++) {
                    this.datacollection.labels.push(response.data[i].date)
                    this.datacollection.datasets[0].data.push(response.data[i].nbConnexion)
                }
                this.renderChart(this.datacollection, this.options)
            })
        }
    },
    created () {
        this.fetchItems()
    }
}
</script>

<style scoped>
.graph {
    width: 100%;
    height: 100%;
}
</style>