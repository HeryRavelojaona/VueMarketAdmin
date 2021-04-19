<template>
<div class="admin-products">
            <div class="section-title">
                <h2>Produits</h2>
            </div>
            <div class="add-new-product">
                <a href="index.php?route=addproduct" class="btn btn-primary text-message-for-all">Ajouter un nouveau produit <i class="fas fa-plus-circle"></i></a>
            </div>
    <div class="content">
        <div class="search">
            <input type="search" placeholder="Recherche" v-model="searchKey" />
        </div>
         <p v-if="search.length == 0">Pas de résultat</p>
        <div class="product-items" >
            <list-product v-for="product, id in search" :product-item="product" :key="id" class="product-item"/>    
        </div>
    </div>
</div>

</template>
<script>
// @ is an alias to /src
import axios from 'axios'
import ListProduct from '../components/listProduct.vue'
export default {
  name: 'AdminProducts',
  components:{
    ListProduct
  },
  data(){
    return{
      products: [],
            searchKey: '',
            showActions: false,
            isActive: false,
            message: ''
    }
  },
  
  computed: {
        search() {
            return (
                this.products.filter(product =>
                    product.title.toLowerCase().includes(this.searchKey.toLowerCase()))
            )
        }
    },
  async mounted() {
        await axios.get(process.env.VUE_APP_API_PRODUCTS)
            .then((res) => res.data)
            .then((res) => this.products = Object.values(res))
            .catch(error => console.log(error));

        
    },
  
}
</script>
<style lang="scss" scoped>


</style>
