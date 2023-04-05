<template>
        <!-- Navigation-->
      <main>
        <nav class="navbar navbar-expand-lg navbar-light bg-light">
            <div class="container px-4 px-lg-5">
                <a class="navbar-brand" href="#">Mesfringues.com</a>
                <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarSupportedContent" aria-controls="navbarSupportedContent" aria-expanded="false" aria-label="Toggle navigation"><span class="navbar-toggler-icon"></span></button>
                <div class="collapse navbar-collapse" id="navbarSupportedContent">
                    <ul class="navbar-nav me-auto mb-2 mb-lg-0 ms-lg-4">
                        <li class="nav-item">
                          <router-link class="nav-link active" aria-current="page" to="/">Accueil</router-link>
                        </li>
                        <li class="nav-item">
                          <router-link class="nav-link" :to="{name: 'about'}">À propos</router-link>
                        </li>
                        <li class="nav-item">
                          <router-link class="nav-link" to="/new-product">Ajouter un produit</router-link>
                        </li>
                    </ul>
                    <form class="d-flex">
                        <button class="btn btn-outline-dark" type="button" @click="toggleSideBar">
                            <i class="bi-cart-fill me-1"></i>
                            Panier
                            <span class="badge bg-dark text-white ms-1 rounded-pill"> {{ totalQuantity }}</span>
                        </button>
                    </form>
                </div>
            </div>
        </nav>
        <Router-view
        :inventory = "inventory"
        :addTo = "addToCart"
        :addInv = "addInventory"
        :removeInv = "removeInventory"
        :remItem = "removeItem"
        :updateInv = "updateInventory"
        />
      </main>
        <footer>
          <nav class="navbar navbar-expand-lg navbar-light bg-light text-center">
            <div class="container px-4 px-lg-5 text-center">
                <a class="navbar-brand" href="#">Mesfringues.com</a>
                <div class="collapse navbar-collapse" id="navbarSupportedContent">
                    <ul class="navbar-nav me-auto mb-2 mb-lg-0 ms-lg-4 ul-footer">
                        <li class="nav-item">
                          <router-link class="nav-link active" aria-current="page" to="/">Accueil</router-link>
                        </li>
                        <li class="nav-item">
                          <router-link class="nav-link" :to="{name: 'about'}">À propos</router-link>
                        </li>
                        <li class="nav-item">
                          <router-link class="nav-link" to="/new-product">Ajouter un produit</router-link>
                        </li>
                    </ul>
                </div>
            </div>
        </nav>
        </footer>
        <Sidebar
        v-if="showSideBar"
        :toggle = "toggleSideBar"
        :cart = "cart"
        :inventory = "inventory"
        :remove = "removeItem"
        :addTo = "addToCart"
        />
</template>

<script>
import Sidebar from '@/components/SideBar.vue'
// import inventory from '@/product.json'
import ProductDataService from '@/services/ProductDataService'

export default {
  components: {
    Sidebar
  },
  data: () => {
    return {
      showSideBar: false,
      inventory: [],
      cart: {}
    }
  },
  methods: {
    toggleSideBar () {
      this.showSideBar = !this.showSideBar
    },
    addToCart (product, index) {
      if (!this.cart[product]) this.cart[product] = 0
      this.cart[product] += this.inventory[index].quantity
      this.inventory[index].quantity = 0
    },
    removeItem (name) {
      delete this.cart[name]
    },
    addInventory (product) {
      this.inventory.push(product)
    },
    removeInventory (index) {
      this.inventory.splice(index, 1)
    },
    updateInventory (index, data) {
      this.inventory[index].name = data.name
      this.inventory[index].photo = data.photo
      this.inventory[index].price = data.price
      this.inventory[index].description = data.description
      this.inventory[index].type = data.type
    }
  },
  computed: {
    totalQuantity () {
      return Object.values(this.cart).reduce((acc, curr) => {
        return acc + curr
      }, 0)
    }
  },
  mounted () {
    ProductDataService.getAll()
      .then(response => {
        this.inventory = response.data
        console.log(response.data)
      })
  }
}
</script>
