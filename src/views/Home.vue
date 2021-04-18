<template>
<div class="home">
      <div class="section-title">
          <h2>Administration</h2>
      </div>
  
      <div class="columns">
          <div class="column is-half">
              <router-link to="/adminproduct">
                <div class="card">
                  <div class="card-image">
                    <figure class="image is-1by1">
                      <img src="@/assets/img/shopping.jpg" alt="Placeholder image">
                    </figure>
                  </div>
                </div>
              </router-link> 
          </div>
          <div class="column is-half">
              <a>
                <div class="card">
                <div class="card-image">
                  <figure class="image is-1by1">
                    <img src="@/assets/img/event.png" alt="Placeholder image">
                  </figure>
                </div>
              </div>
              </a> 
          </div>
      </div>
      <div class="columns">
          <div class="column is-half">
              <a>
                <div class="card">
                <div class="card-image">
                  <figure class="image is-1by1">
                    <img src="@/assets/img/partenariat.jpg" alt="Placeholder image">
                  </figure>
                </div>
              </div>
              </a> 
          </div>
          <div class="column is-half">
              <a>
                <div class="card">
                <div class="card-image">
                  <figure class="image is-1by1">
                    <img src="@/assets/img/contact.jpg" alt="Placeholder image">
                  </figure>
                </div>
              </div>
              </a> 
          </div>
      </div>
</div>
</template>

<script>
// @ is an alias to /src
import axios from 'axios'
export default {
  name: 'Home',
  mounted(){
    console.log(process.env.VUE_APP_MY_ENV_VARIA)
  }
}
</script>

<style lang="scss" scoped>
.section-title{
  margin: 50px auto;
}

.column .card{
  margin: 30px auto;
  width: 300px;
}
</style>
