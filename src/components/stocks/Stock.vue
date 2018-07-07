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
                    <input type="number" class="form-control" v-model="quantity" placeholder="Quantity">
                </div>
                <div class="pull-right">
                    <button class="btn btn-success" @click="buyStock" :disabled="!isBuyable">Buy</button>
                </div>
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
            isBuyable: false
        };
      },
      watch: {
        quantity: function(value)  {
            if(value > 0 && Number.isInteger(parseFloat(value))) {
                this.isBuyable = true;
            } else {
                this.isBuyable = false;
            }
        }
      },
      methods: {
        buyStock() {
            const order = {
                stockId: this.stock.id,
                stockPrice: this.stock.price,
                quantity: parseInt(this.quantity)
            };
            this.$store.dispatch('buyStock', order);
            this.quantity = 0;
        }
      }
    };
</script>
