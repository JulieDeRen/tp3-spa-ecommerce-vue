<template>
    <!-- Header-->
    <header class="py-5 fiche-produit">
      <!--<div class="container px-lg-5 my-5">
          <div class="text-center text-center-vertical">
              <h1 class="display-4 fw-bolder">Magasinez avec style !</h1>
          </div>
      </div>-->
    </header>
    <div class="fiche">
      <section class="py-5">
            <div class="container px-4 px-lg-5 my-5">
                <div class="row gx-4 gx-lg-5 align-items-center">
                    <div class="col-md-6"><img class="img-fiche" :src="`${product.photo}`" :alt="product.name" /></div>
                    <div class="col-md-6">
                        <div class="small mb-1">Code: {{ product.id }}</div>
                        <h2 class="display-5 fw-bolder">{{ product.name }}</h2>
                        <div class="fs-5 mb-5">
                            <span class="text-decoration-line-through"></span>
                            <span>$ {{ product.price.toFixed(2) }}</span>
                        </div>
                        <p class="lead">{{ product.description }}</p>
                        <div class="d-flex">
                            <input class="form-control text-center me-3" id="inputQuantity" type="number" style="max-width: 3rem" v-model.number="product.quantity"/>
                            <button class="btn btn-outline-dark flex-shrink-0" type="button" @click="addTo(product.name, productIndex)">
                                <i class="bi-cart-fill me-1"></i>
                                Ajouter au panier
                            </button>
                        </div>
                        <hr>
                        <router-link class="btn btn-success"  :to="{name: 'edit-product', params: {id: product.id} }">Modifier</router-link>
                    </div>
                </div>
            </div>
      </section>
      <ul class="liste liste-fiche-produit">
        <li class="bottom carteprod"></li>
      </ul>
    </div>
</template>

<script>
export default {
  props: ['inventory', 'addTo'],
  computed: {
    product () {
      const product = this.inventory.find((p) => {
        return p.name === this.$route.params.id
      })
      return product
    },
    productIndex () {
      const index = this.inventory.findIndex((p) => {
        return p.name === this.$route.params.id
      })
      return index
    }
  }
}
</script>
