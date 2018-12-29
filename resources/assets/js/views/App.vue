<template>
    <div>
    <div class="container">
      <p></p>
      <header class="blog-header py-3">
          <div class="row flex-nowrap justify-content-between align-items-center">
          <div class="col-4 pt-1">
          </div>
          <div class="col-4 text-center">
            <a class="blog-header-logo text-dark" href="#"><img src="https://i.imgur.com/s0dTTG9.png"></a>
          </div>
          <div class="col-4 d-flex justify-content-end align-items-center">
          </div>
          </div>
      </header>
      <hr>
      <div class="nav-scroller py-1 mb-2">
        <nav class="nav d-flex justify-content-center">
         <!--  <a class="p-2 text-muted" href="#">World</a> -->
          <li><router-link :to="{name: 'home'}" class="p-2">Home</router-link></li>
          <li><router-link :to="{ name: 'login' }" v-if="!isLoggedIn" class="p-2">Login</router-link></li>
          <li><router-link :to="{ name: 'register' }" v-if="!isLoggedIn" class="p-2">Register</router-link></li>
          <span v-if="isLoggedIn">
                <router-link :to="{ name: 'userboard' }" v-if="user_type == 0" class="p-2">{{name}} Dashboard</router-link>
                <router-link :to="{ name: 'admin' }" v-if="user_type == 1" class="p-2">{{name}} Dashboard</router-link>
          </span>
          <li class="px-2" v-if="isLoggedIn" @click="logout">Logout</li>
        </nav>
      </div> 
    </div>
    <main class="py-4">
        <router-view @loggedIn="change"></router-view>
    </main>
    <footer class="blog-footer">
      <p>&copy Copyright 2018 uidepot.test</p>
      <p>
        <a href="#">Back to top</a>
      </p>
    </footer>
    </div>
</template>
<script>
    export default {
      data(){
          return {
            name        : null,
            user_type   : 0,
            isLoggedIn  : localStorage.getItem('jwt') != null
          }
      },
      mounted() {
        this.setDefaults()
      },
      methods : {
        setDefaults(){
          if(this.isLoggedIn){
            let user        = JSON.parse(localStorage.getItem('user'))
            this.name       = user.name
            this.user_type  = user.is_admin
          }
        },
        change(){
            this.isLoggedIn = localStorage.getItem('jwt') != null
            this.setDefaults()

        },
        logout(){
            localStorage.removeItem('jwt')
            localStorage.removeItem('user')
            this.change()
            this.$router.push('/')
        }
      }
    }
</script>