<template>
    <aside class="cart-container">
        <div class="cart">
          <h1 class="cart-title spread px-4 px-lg-5">
            <span>
              Mon Panier
              <i class="bi-cart-fill me-1"></i>
            </span>
            <button class="cart-close" @click="toggle">&times;</button>
          </h1>
          <div class="cart-body px-4 px-lg-5">
            <p class="center" v-if="!Object.keys(cart).length"><em>Votre panier est vide.</em></p>
            <table class="cart-table">
              <thead>
                <tr>
                  <th><span class="sr-only">Image</span></th>
                  <th>Produit</th>
                  <th>Prix</th>
                  <th>Quantité</th>
                  <th>Total</th>
                  <th><span class="sr-only">Retirer</span></th>
                </tr>
              </thead>
              <tbody>
                <tr v-for="(quantity, key, i) in cart" :key="i">
                    <!--<td><img :src="'img/100/'+getPhoto(key)" :alt="key" /></td>-->
                    <td><img class="img-cart" :src="`${getPhoto(key)}`" :alt="key" /></td>
                    <td>{{ key }}</td>
                    <td>${{getPrice(key)}}</td>
                    <td class="center">{{ quantity }}</td>
                    <td>${{(getPrice(key)*quantity).toFixed(2)}}</td>
                    <td class="center">
                      <button class="btn btn-light cart-remove" @click="remove(key)">
                        &times;
                      </button>
                    </td>
                  </tr>
              </tbody>
            </table>
            <div class="spread">
              <span><strong>Total:</strong> $ {{ calculateTotal() }}</span>
              <button class="btn btn-success">Payer</button>
            </div>
          </div>
          <ul class="liste">
            <li class="carteprod"></li>
            <li class="carteprod"></li>
            <li class="carteprod"></li>
            <li class="carteprod"></li>
            <li class="carteprod"></li>
            <li class="carteprod"></li>
            <li class="carteprod"></li>
            <li class="carteprod"></li>
            <li class="filler carteprod"></li>
            <li class="bottom carteprod"></li>
        </ul>
        </div>
      </aside>
</template>

<script>
export default {
  props: ['toggle', 'cart', 'inventory', 'remove'],
  methods: {
    getPrice (name) {
      const product = this.inventory.find((p) => {
        return p.name === name
      })
      return product.price.toFixed(2)
    },
    getPhoto (name) {
      const product = this.inventory.find((p) => {
        return p.name === name
      })
      return product.photo
    },
    calculateTotal () {
      const total = Object.entries(this.cart).reduce((acc, curr) => { return acc + (curr[1] * this.getPrice(curr[0])) }, 0)
      return total.toFixed(2)
    }
  }
}

</script>
