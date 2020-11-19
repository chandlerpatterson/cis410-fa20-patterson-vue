<template>
    <div>
        <h1>Login</h1>
        <div v-if="this.$route.query.signupsuccess" class="alert alert-success">Thanks for Signing Up, Please Log In Now.</div>
    </div>
</template>

<script>
export default {
    
}
</script>

<style scoped>

</style>