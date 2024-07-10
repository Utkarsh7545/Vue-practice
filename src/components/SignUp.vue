<template>
    <img class="logo" src="../assets/restaurant_logo.webp" />
    <h1>Sign Up</h1>
    <div class="register">
        <input type="text" v-model="name" placeholder="Enter Name" />
        <input type="email" v-model="email" placeholder="Enter Email" />
        <input type="password" v-model="password" placeholder="Enter Password" />
        <button v-on:click="signUp">Sign Up</button>
    </div>
</template>

<script>

import axios from 'axios';
export default {
    name : 'SignUp',
    data(){
        return{
            name:'',
            email:'',
            password:''
        }
    },
    methods:{
        async signUp(){
            console.warn("signUp", this.name, this.email, this.password);
            let result = await axios.post("http://localhost:3000/users",{
                name:this.name,
                email:this.email,
                password:this.password
            });
            console.warn(result);
            if(result.status == 201){
                localStorage.setItem("user-info", JSON.stringify(result.data));
                this.$router.push({name:'Home'})
            }
        }
    }
}
</script>

<style>
.logo{
    width: 180px;
}
.register input{
    display: block;
    height: 30px;
    width: 280px;
    margin: auto;
    padding-left: 10px;
    margin-block: 10px;
    border: 1px solid #d39016;
}
.register button{
    height: 30px;
    width: 295px;
    border: 1px solid #cb8f1f;
    color: white;
    background-color: #dd9510;
    cursor: pointer;
}
</style>