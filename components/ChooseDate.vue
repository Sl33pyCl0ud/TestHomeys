<!-- choose a date in a form and give it like a variable-->
<template>
    <div>
        <form>
            <div class="form-group">
                <label for="date">Choisissez une date</label>
                <input type="date" class="form-control" id="date" v-model="date">
            </div>
            <button type="submit" class="btn btn-primary" @click.prevent="chooseDate">Valider</button>
        </form>
    </div>
</template>

<script>
export default {
    name: 'ChooseDate',
    data () {
        return {
            date: ''
        }
    },
    methods: {
        chooseDate () {
            this.$emit('chooseDate', this.date)
        }
    }
}
</script>

<style scoped>
.form-group {
    width: 20%;
}
.btn {
    margin-left: 110px;
}
</style>