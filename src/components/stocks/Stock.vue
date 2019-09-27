<template>
<div class="col-sm-6 col-md-4 stock">
    <div class="panel panel-success">
        <div class="panel-heading">
            <h3 class="panel-title">
                {{ stock.name }}
                <small>(Price: {{ stock.price | currency }})</small>
                </h3>
        </div>
        <div class="panel-body">
            <div class="pull-left">
                <input 
                    type="number"
                    class="form-control"
                    placeholder="Quantity"
                    :class="{danger:insufficientFunds}"
                    v-model="quantity">
            </div>
            <div class="pull-right">
                <button class="btn btn-success"
                    @click="buyStock"
                    :disabled="insufficientFunds || quantity <= 0">
                    {{ insufficientFunds ? 'Insufficient Funds' : 'Buy' }}</button>
            </div>
        </div>
        <div class="panel-footer">
            <p>{{ `Funds needed : $${purchaseAmt} `}} </p>
        </div>
    </div>

</div>
</template>

<script>
export default {
    props: ['stock'],
    data() {
        return {
            quantity: 0,
            // stockPrice: 0
        }
    },
    computed: {
        funds() {
            return this.$store.getters.funds;
        },

        purchaseAmt() {
            return this.quantity * this.stock.price;
        },

        lowFunds() {
            return this.funds > 2500;
        },
        insufficientFunds() {
            const amtToSpend = this.quantity * this.stock.price;
            console.log(amtToSpend, this.funds)

            return amtToSpend > this.funds;
        }
    },
    methods: {
        buyStock() {
            const order = {
                stockId: this.stock.id,
                stockPrice: this.stock.price,
                quantity: this.quantity
            };
            console.log(order);
            this.$store.dispatch('buyStock', order);
            this.quantity = 0;
        }
    }
}
</script>

<style scoped>

.danger {
    border: 1px solid red
}
.panel {
    box-shadow: 0 10px 6px -6px #777;
    border-radius: 0px;

}

.panel-heading {
    color: white !important;
    background: #1B1B1D !important;
}
.btn-success {
    background: #20CE99;
    border-radius: 0px;
    border: none;
    box-shadow: 0 7px 6px -6px #777 !important;

}
</style>

