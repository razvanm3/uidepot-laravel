<template>
    <div>
        <div class="container">
            <div class="jumbotron p-3 p-md-5 text-white rounded bg-dark">
                <div class="col-md-6 px-0">
                    <h1 class="display-4 font-bold">uidepot.test</h1>
                    <p class="lead my-3">Uidepot is an e-commerce platform for selling bootstrap templates; it's built using Laravel and Vue.js.</p>
                    <p class="lead mb-0"><a href="#" class="text-white font-weight-bold">I hope you like it!</a></p>
                </div>
            </div>
        <div class="row mb-2">
            <div class="col-md-6" v-for="(product,index) in products" @key="index">
                
                <div class="card flex-md-row mb-4 shadow-sm h-md-250">
                    <div class="card-body d-flex flex-column align-items-start">
                    <router-link :to="{ path: '/products/'+product.id}"><strong class="d-inline-block mb-2 text-primary">Bootstrap</strong></router-link>
                    <router-link :to="{ path: '/products/'+product.id}">
                    <h3 class="mb-0">
                        <span v-html="product.name"></span>
                    </h3></router-link>
                    <div class="mb-1 text-muted"><span>$ {{product.price}}</span></div>
                    <!-- <p class="card-text mb-auto">Great Bootstrap 4 Template</p> -->
                    <router-link :to="{ path: '/products/'+product.id}"><span>Buy Now</span></router-link>
                    </div>
                    <router-link :to="{ path: '/products/'+product.id}"><img class="card-img-right img-fluid" :src="product.image" :alt="product.name"></router-link>
                </div>
                
            </div>
        </div>
        </div>
    </div>
</template>
<script>
    export default {
        data(){
            return {
                products : []
            }
        },
        mounted(){
            axios.get("api/products/")
            .then(response => {
                this.products = response.data
            })
            .catch(error => {
                console.error(error);
            })       
        }
    }
</script>
<style scoped>
    .small-text {
        font-size: 14px;
    }
    .product-box {
        border: 1px solid #cccccc;
        padding: 10px 15px;
    }
    .hero-section {
        height: 30vh;
        background: #ababab;
        align-items: center;
        margin-bottom: 20px;
        margin-top: -20px;
    }
    .title {
        font-size: 60px;
        color: #ffffff;
    }
</style>