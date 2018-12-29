<template>
    <div class="container">
        <div class="jumbotron p-3 p-md-5 text-white rounded bg-dark">
                <div class="col-md-6 px-0">
                    <h3 v-html="product.name"></h3>
                </div>
            </div>
        <div class="row">
            <div class="col-md-12">
                <img class="img-fluid" :src="product.image" :alt="product.name">
                <p></p>
                <h3 class="title" v-html="product.name"></h3>
                <p class="text-muted">{{product.description}}</p>
                <h4>
                    <span class="small-text text-muted float-left">$ {{product.price}}</span>
                    <!-- <span class="small-text float-left">Available Quantity: {{product.units}}</span> -->
                </h4>
                <br>
                <hr>
                <router-link :to="{ path: '/checkout?pid='+product.id }" class="col-md-4 btn btn-sm btn-primary float-left">Buy Now</router-link>
            </div>
        </div>
    </div>
</template>
<script>
    export default {
        data(){
            return {
                product : []
            }
        },
        beforeMount(){
            axios.get(`/api/products/${this.$route.params.id}`)
            .then(response => {
                this.product = response.data
            })
            .catch(error => {
                console.error(error);
            })       
        }
    }
</script>
<style scoped>
    .small-text {
        font-size: 18px;
    }
    .title {
        font-size: 36px;
    }
</style>