    <template>
        <div class="signUp_user">
            <div class="container_signUp_user">
                <form v-on:submit.prevent="processSignUp"> 
                    <label id="user_username"> Username:
                        <input type="text" v-model="user.username" placeholder="Usuario" required>
                    </label>
                    <label id="user_password"> Password:
                        <input type="password" v-model="user.password" placeholder="Contraseña" required>
                    </label>
                    <label for="user_perfil"> Perfil:
                        <select id="user_perfil" v-model="user.perfil">
                        <option value="SeleccionePerfil">Seleccione una opción</option>
                        <option value="empleado">Empleado</option>
                        <option value="familiar">Familiar</option>
                        <option value="paciente">Paciente</option>                        
                        </select>                        
                    </label>
                    <br>
                    <label id="user_name"> Nombre:
                        <input type="text" v-model="user.name" placeholder="Nombre" required>
                    </label>
                    <label id="user_apellido"> Apellidos:
                        <input type="text" v-model="user.apellidos" placeholder="Apellidos" required>
                    </label>
                    <label id="user_telefono"> Telefono:
                        <input type="" v-model="user.telefono" placeholder="N Telefonico" required>
                    </label>
                    
                    <label for="user_genero"> Genero:
                        <select id="user_genero" v-model="user.genero">
                        <option value="SeleccioneGenero">Seleccione un genero</option>
                        <option value="familiar">Familiar</option>
                        <option value="paciente">Paciente</option>
                        <option value="paciente">Paciente</option>
                        <option value="paciente">Paciente</option>
                        </select>
                    </label>
                    <button type="submit">Registrarse</button>
                </form>    
            </div>
        </div>
    </template>

    <script>
    import axios from 'axios';
    export default { 
        data:function(){
            return{
                user:{
                    username: "",
                    password: "",
                    name: "",
                    apellidos: "",
                    telefono:"",
                    genero:""
                    
                }
            }
        },

        methods:{
            processSignUp:function(){
                axios.post("https://hospitality-backend.herokuapp.com/Usuario/", this.user,{headers:{}})
                .then((result)=>{
                    alert("Registro Exitoso");
                    let dataSignUp={
                        username: this.user.username,
                        token_access: result.data.access,
                        token_refresh: result.data.refresh
                    }
                    this.$emit('completedSignUp',dataSignUp)
                }).catch((error)=>{
                    console.log(error)
                    alert("Error: fallo el registro");

                })
            }
        }
    }
    
    </script>

    <style>
    .signUp_user{
        margin: 0;
        padding: 0%;
        height: 100%;
        width: 100%;
        display: flex;
        justify-content: center;
        align-items: center;
    }
    .container_signUp_user {

        border: 3px solid #283747;
        border-radius: 10px;
        width: 25%;
        height: 85%;
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
    }
    .signUp_user h2{
        color: #283747;
    }
    .signUp_user form{
        width: 70%;
    }
    .signUp_user input {
        height: 40px;
        width: 100%;
        box-sizing: border-box;
        padding: 10px 20px;
        margin: 5px0;
        border: 1px solid #283747;
    }
    .signUp_user button {
        width: 100%;
        height: 40px;
        color: #E5E7E9;
        background: #77a8d9;
        border: 1px solid #E5E7E9;
        border-radius: 5px;
        padding: 10px 25px;
        margin: 5px0 25px0;

    }
    .signUp_user button:hover{
        color: #E5E7E9;
        background: crimson;
        border: 1px solid #283747;
    }
    </style>