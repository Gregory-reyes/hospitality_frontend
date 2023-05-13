<template>
    <div class="logIn_user">
        <div class="container_logIn_user">
        <h2>Iniciar Sesión</h2>

        <form v-on:submit.prevent="processLogInUser">
            <label id="user_username"> Username:
                   <input type="text" v-model="user.username" placeholder="Usuario" required> 
            </label>
            <br>
            <label id="user_password"> Password:
                   <input type="password" v-model="user.password" placeholder="Contraseña" required> 
            </label>
            <br>
            <button type="submit"> Iniciar Sesion </button>  
        </form>
        </div>
    </div>
</template>

    <script>
    import axios from 'axios'; //Importamos axios para hacer peticiones al servidor
    export default { //Exportamos el componente
    
        data: function(){   //Data es una funcion que retorna un objeto
        return {
            user: {
                username:"",
                password:""
                }
            }
        },
    methods: {  //Metodos del componente
        processLogInUser: function(){   //Funcion que se ejecuta cuando se envia el formulario
            axios.post("https://hospitality-backend.herokuapp.com/login/",
            this.user, {headers: {}})  //Headers es un objeto que contiene los encabezados de la peticion
            
            .then((result) => { //Se ejecuta cuando la peticion es exitosa
                let dataLogIn = {
                    username: this.user.username,
                    token_access: result.data.access,
                    token_refresh: result.data.refresh,
                    }
                this.$emit('completedLogIn', dataLogIn) //Emitimos un evento al componente padre
                })
            .catch((error) => {
                if (error.response.status == "401")
                alert("ERROR 401: Credenciales Incorrectas.");
                });
            }
        }
    }
    </script>

    <style>
    .logIn_user{
        margin: 0;
        padding: 0%;
        height: 100%;
        width: 100%;
        display: flex;
        justify-content: center;
        align-items: center;
        }
    .container_logIn_user { /*Estilos del componente*/
        border: 3px solid #283747;
        border-radius: 10px;
        width: 25%;
        height: 60%;
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
        }
    .logIn_user h2{
        color: #283747;
        }
    .logIn_user form{   /*Estilos del formulario*/
        width: 70%;
        }
    .logIn_user input{  
        height: 40px;
        width: 100%;
        box-sizing: border-box;
        padding: 10px 20px;
        margin: 5px 0;
        border: 1px solid #283747;
        }
    .logIn_user button{ 
        width: 100%;
        height: 40px;
        color: #E5E7E9;
        background: #77a8d9;
        border: 1px solid #E5E7E9;
        border-radius: 5px;
        padding: 10px 25px;
        margin: 5px 0;
        }
    .logIn_user button:hover{   /*Estilos del boton cuando el cursor esta encima*/
        color: #E5E7E9;
        background: crimson;
        border: 1px solid #283747;
        }
    </style>