<template>
    <div class="col-sm-6 col-md-4">
        <div class="panel panel-success">
            <div class="panel-heading">
                <h3 class="panel-title">
                    {{ stock.name }}
                    <small>(Price: {{ stock.price }})</small>
                </h3>
            </div>
            <div class="panel-body">
                <div class="pull-left">
                    <input
                        :class="{danger: insufficientFunds}"
                        type="number"
                        class="form-control"
                        placeholder="Quantity"
                        v-model="quantity">
                </div>
                <div class="pull-right">
                    <button
                        class="btn btn-success"
                        @click="buyStock"
                        :disabled="insufficientFunds || quantity <= 0 || !Number.isInteger(quantity * 1)"
                        >{{ buttonText }}
                    </button>
                </div>
            </div>
        </div>
    </div>
</template>

<style>
    .danger {
        border: 1px solid red;
    }
    .pull-left {
        width: 175px;
    }
</style>

<script>
    export default {
        props: ['stock'],
        data() {
            return {
                quantity: 0
            }
        },
        methods: {
            buyStock() {
                const order = {
                    stockId: this.stock.id,
                    stockPrice: this.stock.price,
                    quantity: this.quantity * 1
                };
                this.$store.dispatch('buyStock', order);
                this.quantity = null;
            }
        },
        computed: {
            insufficientFunds () {
                return this.quantity * this.stock.price > this.funds;
            },
            funds () {
                return this.$store.getters.funds;
            },
            buttonText () {
                return (this.insufficientFunds ? 'Insufficient Funds' : 'Buy')
            }
        },
    }
</script>