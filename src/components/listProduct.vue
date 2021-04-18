<template>
  <div class="admin-product">
    <h3>{{ productItem.title }}</h3>
                <div class="col-xs-12 admin-actions">
                    <a @click.prevent="liked(productItem.id, productItem.liked)" :id="productItem.id" :class="{ liked : productItem.liked == true }" class="btn admin-btn btn-light" title="favori"><i class="fas fa-heart"></i></a>
                    <a :href="getUpdateUrl(productItem.id)" class="btn admin-btn btn-warning" title="Modifier produit de base">Modifier le produit <i class="fas fa-exchange-alt"></i></a>
                    <router-link :to="{ name: 'managemodel', params: { id : productItem.id, productname : productItem.title }}" class="btn admin-btn btn-primary">Gestion des modèles</router-link>
                    

                    <button class="is-primary admin-btn check-delete" @click="isActive = !isActive" title="Supprimer"><i class="fas fa-trash-alt" ></i></button>
                    <div class="control-delete" v-if="isActive" >
                        <form action="index.php?route=deleteproduct" method="POST" class="delete-form" >
                        <p class="go-delete">Etes vous sur ?</p>
                        <p>{{ message }}</p>
                            <button class="button is-danger go-delete confirm-delete" @click.prevent="deleteProduct(productItem.id, productItem.filename)" name="submit">Oui <i class="fas fa-trash-alt"></i></button>
                            <button class="stop-delete go-delete button is-info" @click.prevent="isActive = false" >Non</button>
                        </form>
                    </div>
                </div>
    
  </div>
</template>

<script>
import axios from 'axios'
export default {
  name: 'list-product',
  props:{
    productItem: {
      type: Object,
      required: true
    }
  },
  data(){
    return{
      showActions: false,
            isActive: false,
            message: ''
    }
  },
  methods: {
      getModel(id) {
          return "index.php?route=addmodel&productId=" + id + ""
      },
      getUpdateUrl(id) {
          return "index.php?route=updateproduct&productId=" + id + ""
      },
      handleShow(e) {
          e.target.classList.toggle("active");
          this.showActions = !this.showActions;
      },
      deleteProduct(id, filename) {
          let formData = new FormData();
          formData.append('id', id);
          formData.append('filename', filename);
          axios.post('index.php?route=deleteproduct', formData)
              .then((res) => res.data)
              .then((res) => {
                  if (res.isSuccess) {
                      this.message = res.message;
                      location.reload();
                  } else {
                      this.message = res.message
                  }
              })
              .catch(error => console.log(error));

      },
      async liked(id, likeStatus) {
          let newLike;
          if (likeStatus == 1) {
              newLike = 0;
          } else if (likeStatus == 0) {
              newLike = 1;
          }

          let formData = new FormData();
          formData.append('id', id);
          formData.append('liked', newLike);
          await axios.post('index.php?route=getlike', formData)
              .then((res) => console.log('Liked'))
              .then(() => {
                  axios.get('index.php?route=api/products')
                      .then((res) => res.data)
                      .then((res) => this.products = Object.values(res))
                      .catch(error => console.log(error));
              })

          .catch(error => console.log(error));
      }
  },
}
</script>

