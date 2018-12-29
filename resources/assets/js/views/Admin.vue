<template>
    <div class="container">
            <div class="jumbotron p-3 p-md-5 text-white rounded bg-dark">
                <div class="col-md-6 px-0">
                    <h1 class="display-4 font-bold">Admin Dashboard</h1>
                </div>
            </div>
            <div class="row">
                <div class="col-md-2">
                    <ul style="list-style-type:none">
                      <li><button type="button" class="btn btn-primary m-1" @click="setComponent('main')">Dashboard</button></li>
                      <li><button type="button" class="btn btn-primary m-1" @click="setComponent('orders')">Orders</button></li>
                      <li><button type="button" class="btn btn-primary m-1" @click="setComponent('products')">Products</button></li>
                      <li><button type="button" class="btn btn-primary m-1" @click="setComponent('users')">Users</button></li>
                    </ul>
                </div>
                <div class="col-md-10">
                    <component :is="activeComponent"></component>
                </div>
            </div>
    </div>
</template>
<script>
    import Main from '../components/admin/Main'
    import Users from '../components/admin/Users'
    import Products from '../components/admin/Products'
    import Orders from '../components/admin/Orders'
    
    export default {
        data(){
            return {
                user : null,
                activeComponent : null
            }
        },
        components : {
            Main, Users, Products, Orders
        },
        beforeMount(){
            this.setComponent(this.$route.params.page)
            this.user = JSON.parse(localStorage.getItem('user'))
            axios.defaults.headers.common['Content-Type'] = 'application/json'
            axios.defaults.headers.common['Authorization'] = 'Bearer ' + localStorage.getItem('jwt')
        },
        methods : {
            setComponent(value){
                switch(value) {
                    case "users":
                        this.activeComponent = Users
                        this.$router.push({name : 'admin-pages', params : {page: 'users'}})
                        break;
                    case "orders":
                        this.activeComponent = Orders
                        this.$router.push({name : 'admin-pages', params : {page: 'orders'}})
                        break;
                    case "products":
                        this.activeComponent = Products
                        this.$router.push({name : 'admin-pages', params : {page: 'products'}})
                        break;
                    default:
                        this.activeComponent = Main
                        this.$router.push({name : 'admin'})
                        break;
                }
            }
        }
    }
</script>
<style scoped>
    .hero-section {
        height: 20vh;
        background: #f0f0f0;
        align-items: center;
        margin-bottom: 20px;
        margin-top: -20px;
    }
    .title {
        font-size: 40px;
        color: #ffffff;
    }
</style>