<template>
    <div class="card text-white bg-dark mb-3" style="max-width: 25rem;">
        <div class="card-header">Total d'appels : {{ nbappel }}</div>
        <div class="card-header">Periode : {{periode}}</div>
    </div>
</template>

<script>
export default {
  name: 'Appel',
  props : {
    nbappel: String,
    periode: String
  }
}
</script>