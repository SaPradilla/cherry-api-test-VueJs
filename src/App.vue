<script setup>
  import Login from './components/Login.vue';
  import Register from './components/Register.vue';
  import {ref,reactive} from 'vue'
  import axios from 'axios'


  const userValidate = reactive({
        name:'',
        email:'',
        state:'Activo',
        phone:'',
        password:'',
        rol:''
  })
  const alerta = reactive({
        tipo: '',
        mensaje: ''
  })



  // Loguear
  const loguearUsuario =()=>{        
        axios.post('https://cherry-api-test.onrender.com/api/users/login',{
            // email: userValidate.email,
            // password:  userValidate.password
        
            email:userValidate.email,
            password:userValidate.password
            
        }).then(respuesta =>{
            alerta.mensaje = respuesta.data.msg
            alerta.tipo = 'exito'
            console.log(respuesta.data.msg)
            console.log(respuesta)
        }).catch(error =>{
            alerta.mensaje = error.response.data.msg
            alerta.tipo = 'error'
            console.log( error.response.data.msg)
            console.log(error)
        })
        setTimeout(() => {
            Object.assign(alerta, {
                tipo: '',
                mensaje: ''
            })
        }, 4000)  

    }

  // Registrar
  const registarUsuario = ()=>{        
      axios.post('https://cherry-api-test.onrender.com/api/users/register',{
          name:userValidate.name,
          email:userValidate.email,
          state:'Activo',
          phone:userValidate.phone,
          password:userValidate.password,
          rol:userValidate.rol
      }).then(respuesta =>{
          alerta.mensaje = respuesta.data.msg
          alerta.tipo = 'exito'
          console.log(respuesta.data.msg)
          console.log(respuesta)
      }).catch(error =>{
          alerta.mensaje = error.response.data.msg
          alerta.tipo = 'error'
          console.log(error.response.data.msg)
          console.log(error)
      })
      // setTimeout(() => {
      //     Object.assign(alerta, {
      //         tipo: '',
      //         mensaje: ''
      //     })
      // }, 4000)  
  }
</script>

<template>
  <div class="md:flex mt-10">
    <h2
    @click=""
    >Login</h2>
    <h2>Registro</h2>
    <div class="md:w-1/2 md:h-screen">
      <h1 class="text-center text-4xl">Sing In</h1>
      <Login
      :userValidate="userValidate"
      />
    </div>
    <div class="md:w-1/2 md:h-screen">
      
      <h1 class="text-center text-4xl">Sign Up</h1>
      <Register
      @registarUsuario="registarUsuario"
      :userValidate="userValidate"
      :alerta="alerta"
      />
    </div>
  </div>
   
</template>

<style scoped>
</style>
