<template>
    <div>
        <h1>Products</h1>
        <hr/>

        <table class="table">
            <thead>
                <tr>
                    <th>Title</th>
                    <th>Description</th>
                    <th>Price</th>
                    <th></th>
                </tr>
            </thead>
            <tbody>
                <tr v-for="thisProduct in products" :key="thisProduct.ProductPK">
                    <th>{{thisProduct.Title}}</th>
                    <td>{{thisProduct.Description}}</td>
                    <td>{{thisProduct.Price}}</td>
                    <td>
                        <router-link :to="`/products/${thisProduct.ProductPK}`">
                        <button type="button" class=" btn btn-primary">Details</button>
                        </router-link>
                    </td>
                    </tr>
            </tbody>
        </table>
    </div>
</template>

<script>
export default {
    computed:{
        products(){return this.$store.state.products}
    }
    
}
</script>

<style scoped>

</style>