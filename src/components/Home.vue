<template>
    <div>
        <h1>Trade or View your Portfolio</h1>
        <h6>You may Save & Load your Data</h6>
        <h6>Click on 'End Day' to begin your new Day</h6>
        <hr>
        <p
        :class="{lowFunds: lowFunds}"
        >Your Funds: {{ funds | currency }}</p>
    </div>
</template>

<script>
export default {
    computed: {
        funds() {
            return this.$store.getters.funds;
        },
        lowFunds() {
            return this.funds < 2500;
        }
    }
}
</script>

<style>
p {
    color: #20CE99
}

.lowFunds {
    color: red
}

</style>

