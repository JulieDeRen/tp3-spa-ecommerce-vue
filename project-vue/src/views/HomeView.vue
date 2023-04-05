<template>
    <!-- Header-->
    <header class="py-5 header">
        <img class="hero" src="/img/HeroBanner/pinkhair_1920.jpg" alt="floating">
        <div class="container px-lg-5 my-5">
            <div class="text-center text-center-vertical">
                <h1 class="display-1 fw-bolder">Magasinez avec style !</h1>
            </div>
        </div>
    </header>
        <!-- Section-->
        <ul class="liste">
            <li class="carteprod" v-for="(product, i) in inventory" :key="i">
                <!-- Product image-->
                <img :src="`${product.photo}`" :alt="product.name" @click="$router.push({ name: 'product', params: {id: product.name}})">
                <!-- Product details-->
                <!-- Product name-->
                <div class="info">
                    <router-link :to="{name: 'product', params: {id: product.name}}">
                        <h5 class="fw-bolder">{{product.name}}</h5>
                    </router-link>
                    <!-- Product price-->
                    $ {{ (product.price).toFixed(2)}}
                    <!-- Product actions-->
                    <input class="form-control qt" type="number" v-model.number="product.quantity"/>
                    <a class="btn btn-outline-dark mt-auto" @click="addTo(product.name, i)">Ajouter</a>
                </div>
            </li>
            <li class="filler carteprod"></li>
            <li class="bottom carteprod"></li>
        </ul>
</template>

<script>
export default {
  props: ['inventory', 'addTo']
}
</script>
