<template>
<div class="blocMedia">
            <div class="socialTitle">
                <img src="../assets/icon-left-font.png">
            </div>
            <div id="formBloc">
                <form>
                    <input v-model = "login.front_pseudo" v-if = "mode == 'create'" placeholder="Pseudo">
                    <input v-model = "login.front_email" placeholder="Adresse e-mail">
                    <input v-model = "login.front_password" placeholder="Mot de passe">
                    <button id="btnConect" v-if = "mode == 'login'" @click="btnConect" >Se connecter</button>
                    <button v-else id="btnSignUp" @click="btnSignUp">Creer un compte</button>
                    <a v-if = "mode == 'create'" @click="connectAccount" href="#"><p>Se connecter</p></a>
                    <a href="#"><p>Mot de passe oublié ?</p></a>
                    <a v-if = "mode == 'login'" @click="createAccount" href="#"><p>Creer un compte</p></a>
                    <div id="trait"></div>
                    <router-link to="/PageAccueil">Page suivante</router-link>
                </form>  
            </div>
        </div>
</template>

<script>
import axios from "axios";
export default {
  name: 'HelloWorld',
    data() {
    return {
      login:{
          front_password:"",
          front_pseudo: "", 
          front_email: ""},
      mode : "login",
      front_pseudo :"",
      front_email : "",
      front_password: "",
    };
  },
 methods: {
    connectAccount(){
        this.mode = "login";
    },
    createAccount(){
        this.mode = "create";
    },
btnConect(){
        axios.post('http://localhost:3000/api/login', this.login)
            .then(response => {
                    const token =  response.data.token;
                    const userId = response.data.userId;
                    const level = response.data.level;
                    localStorage.setItem("access_token", token),
                    localStorage.setItem("userId", userId),
                    localStorage.setItem("level", level)
                    this.$router.push("/PageAccueil");
                    
                    console.log(this.login)
                });
            },
btnSignUp(){
        axios.post('http://localhost:3000/api/signup', this.login)
            .then(response => {
                    const token =  response.data.token;
                    const userId = response.data.userId;
                    const level = response.data.u_role;
                    localStorage.setItem("access_token", token),
                    localStorage.setItem("userId", userId),
                    localStorage.setItem("level", level)
                    console.log(this.login)
                });
            }
    }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Lato:wght@300&display=swap');
body{
    margin : 0px;
    padding: 0px;
    margin: 0px;
    background-color: #FBF9FF;

}
a{ 
text-decoration: none; }

.bgImage{
    background: url(../assets/logo.png);
    position: relative;
}
.blocMedia, input, button {
    font-family: 'Lato';
}
.blocMedia{
 width: 700px;
 margin: 200px auto;
 display: flex;
 justify-content: space-between;
}
.socialTitle {
    margin-right: 30px;
    width: 300px;
   
}
.socialTitle img{
   object-fit: cover;
    width: 300px;
   
}
#formBloc{
    background-color: #FFD7D7;
    width: 400px;
    margin: auto;
    padding: 0 15px 10px;
    border-radius: 20px;
    box-shadow: 20px 10px 5px 3px rgba(0,0,0,0.23);
}
form p {
    color: #4E5166;
    margin-top: 7px;
    margin-bottom: 15px;
    margin-left: 122px;
    font-weight: bold;
    font-style: italic;
}
form p:hover{
    text-decoration: underline;
    cursor: pointer;
}

#trait{
    height: 1px;
    opacity: 0.5;
    width: 80%;
    background-color: #B5B5B5;
    margin: 2px auto;
    margin-bottom: 15px;
    
}
#btnConect {
    border: none;
    width: 350px;
    padding: 15px 10px;
    margin: 10px 0px 0px 12px;
    border-radius: 8px;
    background-color:#4E5166;
    color: white;
    font-weight: bold;
}
#btnConect:hover{
    background-color: #90E795;
    color: white;
    cursor: pointer;
    transition: 0.7s ease-in-out;
}
#btnSignUp{
    border: none;
    width: 250px;
    padding: 15px 10px;
    margin: 10px 0px auto 18%; 
    border-radius: 8px;
    font-weight: bold;
    background-color:#FBEAA2;
    color: #424242;

}
#btnSignUp:hover{
    background-color: #FACC8E;
    color: white;
    cursor: pointer;
    transition: 0.7s ease-in-out;
}
input {
    border: none;
    width: 350px;
    padding: 15px 10px;
    margin: 10px 0px;
    border-radius: 8px;
    border: solid 1px #E5E6E4;
}
@media all and (max-width: 1080px){
    .blocMedia{width: 100%; display: block; margin: 0px;}
    .socialTitle{width: 100%;}
    #formBloc{width: 80%;}
    #btnConect{width: 250px;}
    .socialTitle img{ width: 200px }
    .socialTitle{ width: 200px }
    input{ width: 80%; }
}

</style>

