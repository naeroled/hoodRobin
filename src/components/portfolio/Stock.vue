<template>
<div class="col-sm-6 col-md-4 stock">
    <div class="panel panel-success">
        <div class="panel-heading">
            <h3 class="panel-title">
                {{ stock.name }}
                <small>(Price: {{ stock.price }} | Quantity: {{ stock.quantity }})</small>
                </h3>
        </div>
        <div class="panel-body">
            <div class="pull-left">
                <input 
                    type="number"
                    class="form-control"
                    placeholder="Quantity"
                    :class="{danger:insufficientQuantity}"

                    v-model="quantity">
            </div>
            <div class="pull-right">
                <button class="btn btn-success"
                    @click="sellStock"
                    :disabled="insufficientQuantity || quantity <= 0">
                    {{ insufficientQuantity ? 'Not Enough' : 'Sell' }}
                </button>
            </div>
        </div>
    </div>

</div>
</template>

<script>
import {mapActions} from 'vuex';


export default {
    props: ['stock'],
    data() {
        return {
            quantity: 0,
            stockPrice: 0
        }
    },
    computed: {
        insufficientQuantity() {
            return this.quantity > this.stock.quantity
        }
    },
    methods: {
        ...mapActions({
            placeSellOrder: 'sellStock'
    }),

        sellStock() {
            const order = {
                stockId: this.stock.id,
                stockPrice: this.stock.price,
                quantity: this.quantity
            };
            console.log(order);
            this.placeSellOrder(order);
        }
    }
}
</script>

<style scoped>

.panel {
    box-shadow: 0 10px 6px -6px #777;
    border-radius: 0px;

}

.panel-heading {
    color: white !important;
    background: black !important;
}
.btn-success {
    background: #20CE99;
    /* border-radius: 0px; */
    box-shadow: 0 7px 6px -6px #777 !important;
}
.danger {
    border: 1px solid red
}
</style>