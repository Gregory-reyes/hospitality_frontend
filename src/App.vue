<template>
    <div id="app" class="app">
      <div class="header">
        <h1>Hospital happy Pets</h1>   <!--Estaran presente durante su inicio-->
          <nav>
            <button v-if="is_auth" v-on:click="loadHome" > Inicio </button>
            <button v-if="is_auth" v-on:click="loadAccount"> Cuenta </button>
            <button v-if="is_auth" v-on:click="logOut"> Cerrar Sesión </button>
            <button v-if="!is_auth" v-on:click="loadLogIn"> Iniciar Sesión </button>  <!--Estaran presentes durante su inicio-->
            <button v-if="!is_auth" v-on:click="loadSignUp"> Registrarse </button> 
          </nav>
      </div>
    </div>
      <div class="main-component"> 
        <router-view
        v-on:completedLogIn= "completedLogIn"
        v-on:completedSignUp= "completedSignUp"
        v-on:logOut="logOut"
        >
        </router-view>
      </div>
      <div class="footer">
        <h2>Derechos de autor reservados Hospitality®</h2>
      </div>    
  </template>

  <script>
    export default {
      
      data: function(){
        return{
        is_auth: false
        }
      },
      components: {
      },
      
      methods:{
        verifyAuth: function() {  //Verifica si el usuario esta logeado
        this.is_auth= localStorage.getItem("isAuth") || false;

        if(this.is_auth == false)
            this.$router.push({name:"logIn"});
          else
            this.$router.push({name:"home"});
        },

      loadLogIn: function(){
        this.$router.push({name: "logIn"}) //Redirecciona a la pagina de inicio de sesion
        },
      loadSignUp: function(){
        this.$router.push({name: "signUp"}) //Redirecciona a la pagina de registro
        },

      completedLogIn: function(data) {}, //Funciones que se ejecutaran cuando se complete el inicio de sesion o el registro
      completedSignUp: function(data) {}, //Se ejecutaran en el componente hijo
      },

      created: function(){ //Se ejecuta cuando se crea el componente
        this.verifyAuth()
      }
      }
  </script>

  <style>
    body{
      margin: 0 0 0 0;
    }
    .header{  /*Estilos de los componentes*/
      margin: 0%;
      padding: 0;
      width: 100%;
      height: 10vh;
      min-height: 100px;
      background-color: #77a8d9 ;
      color:#E5E7E9 ;
      display: flex;
      justify-content: space-between;
      align-items: center;
    }
    .header h1{ 
      width: 20%;
      text-align: center;
      }
    .header nav {  
      height: 100%;
      width: 20%;
      display: flex;
      justify-content: space-around;
      align-items: center;
      font-size: 20px;
    }
    .header nav button{
      color: #E5E7E9;
      background: #77a8d9;
      border: 1px solid #E5E7E9;
      border-radius: 5px;
      padding: 10px 20px;
    }
    .header nav button:hover{
      color: #283747;
      background: #E5E7E9;
      border: 1px solid #E5E7E9;
    }
    .main-component{ /*Estilos del componente principal*/
      height: 75vh;
      margin: 0%;
      padding: 0%;
      background: #FDFEFE ;
    }
    .footer{ 
      margin: 0;
      padding: 0;
      height: 10vh;
      min-height: 100px;
      background-color: #77a8d9;
      color: #FDFEFE;
    }
    .footer h2{
      width: 100%;
      height: 100%;
      display: flex;
      justify-content: center;
      align-items: center;
    }
  </style>