<template>
    <div>
        <h1>Login</h1>
        <div v-if="this.$route.query.signupsuccess" class="alert alert-success">
            Thanks for Signing Up, Please Log In Now.</div>
     <form @submit.prevent="onSubmit">
            <div class="form-group"><label for="exampleInputEmail1">Email Address</label> 
                <input type="email" id="exampleInputEmail1" required="required" placeholder="Enter Email" class="form-control" v-model="email">
            </div> 

            <div class="form-group"><label for="exampleInputPassword1">Password</label> 
                <input type="password" id="exampleInputPassword1" placeholder="Password" required="required" class="form-control" v-model="password">
            </div> 
            <button type="submit" class="btn btn-primary">Submit</button> 

            <p v-if="credentialsError" class="form-text text-danger">Invalid User Credentials</p>

              <p v-if="loginError" class="form-text text-danger">Unable to Log In, Please Try Again Later.</p>

        </form>
    </div>
</template>

<script>
import axios from 'axios';
export default {
    data(){
        return{
            email: '',
            password: '',
            loginError: false,
            credentialsError: false
        }
    },
    methods:{
        onSubmit(){
            const myFormData={
                email: this.email,
                password: this.password
            };
           //console.log("Form Data: ", myFormData)
           axios.post("/customers/login", myFormData)
           .then(myResponse=>{
               console.log("My Response: ", myResponse)

               this.$store.commit("storeTokenInApp", myResponse.data.token);
               this.$store.commit("storeUserInApp", myResponse.data.user);
               this.$router.replace("/account");
           })
           .catch((myError)=>{
               console.log("My Error", myError.response.data)

               if(myError.response.data == 'Invalid User Credentials'){
                   this.credentialsError = true
               }
               else{
                   this.loginError = true
                }
           })
        }
    }

}
</script>

<style scoped>

</style>