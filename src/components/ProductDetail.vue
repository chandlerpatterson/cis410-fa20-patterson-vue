<template>
    <div>
        <div class="card">
            <div class="card-body">
                <h2 class="text-primary">{{product.Title}}</h2>
                <br/>
                <p>Description: <br/> <strong>{{product.Description}}</strong></p>
                <p>Price: <br/> <strong>{{formattedPrice}}</strong></p>
            </div>
        </div>
        <br/>

        <router-link v-if="auth" :to="`/products/${this.$route.params.pk}/review`">
        <button type="button" class="btn btn-success">Add a Review</button>
        </router-link>
         <router-link v-else :to="`/signin`">
            <button type="button" class="btn btn-outline-success">Please Sign In to Add a Review</button>
        </router-link>
        <br/>
        <br/>
        <router-view></router-view>
    </div>
</template>

<script>
export default {
    computed:{
        product(){
            var products = this.$store.state.products;
            var thisProduct = products.find((aProduct)=> aProduct.ProductPK == this.$route.params.pk)
            return thisProduct
        },
        formattedBPrice(){
            return new Intl.NumberFormat("en-US",{
                style: 'currency',
                currency: 'USD'
            }).format(this.product.Price)
        },
        auth(){return this.$store.state.token}
    }
}
</script>

<style scoped>
</style>