<template>
    <div>
        <h1>Sign Up</h1>
        <form @submit.prevent="onSubmit">
            <div class="form-group"><label for="fname-input">First Name</label> <input type="text" id="fname-input" required="required" placeholder="Enter First Name" class="form-control" v-model="firstName"></div> 

            <div class="form-group"><label for="lname-input">Last Name</label> <input type="text" id="lname-input" required="required" placeholder="Enter Last Name" class="form-control" v-model="lastName"></div> 

            <div class="form-group"><label for="email-input">Email Address</label> <input type="email" id="email-input" required="required" placeholder="Enter Email Address" class="form-control" v-model="email"> 
            <small v-if="dupEmail" class="from-text text-danger">Please Choose a Different Email.</small>
            </div> 

            <div class="form-group"><label for="password-input">Password</label> <input type="password" id="password-input" placeholder="Enter Password" required="required" value="asdfasdf" class="form-control" v-model="password">

            </div> <button type="submit" class="btn btn-primary">Submit</button> <p id="error-signup" class="text-danger">{{errorMessage}}</p>

            </form>
    </div>
</template>

<script>
import axios from 'axios';
export default {
    data(){
        return {
            firstName:'',
            lastName:'',
            email:'',
            password:'',
            errorMessage:'',
            dupEmail: false
        }
    },
    methods:{
        onSubmit(){

            const myFormData = {
                firstName: this.firstName,
                lastName: this.lastName,
                email: this.email,
                password: this.password
            }
            //console.log(myFormData)

            axios.post("/customers", myFormData)
            .then((myResponse)=>{
                //console.log(myReponse)
                this.$router.replace('/signin?signupsuccess=true')
                })
                .catch((myError)=>{
                    if(myError.response.status === 409){
                        this.dupEmail = true
                    }else{
                        this.errorMessage = "Cannot Sign You Up, Please Try Again Later."
                    }
                })
        }
    }
}
</script>

<style scoped>

</style>