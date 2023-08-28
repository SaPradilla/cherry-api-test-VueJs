<script setup>
    import Alerta from './Alerta.vue'
    import axios from "axios";
    import {ref,reactive} from 'vue'
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
    // const userValidate = reactive({})
    const registarUsuario =()=>{        
        axios.post('https://cherry-api-test.onrender.com/api/users/register',{
            // email: userValidate.email,
            // password:  userValidate.password
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
        setTimeout(() => {
            Object.assign(alerta, {
                tipo: '',
                mensaje: ''
            })
        }, 4000)  
    }
    
</script>
<template>
    <div class="mx-auto my-10 max-w-2xl bg-red-300 rounded-3xl ">
        <div class="p-10">
            <img class="w-32  mx-auto" src="../assets/img/Cherry_icon.png" alt="" srcset="">
            <h1 class="text-3xl text-center font-bold"><span class=" text-red-600">Cherry Stock</span> - Registro</h1>
            <form @submit.prevent="registarUsuario"
            class="flex flex-col px-5 mt-5 " method="post">

                <label class="uppercase text-2xl font-semibold mt-5 " for="">Nombre</label>
                <input class="border-2 rounded-md h-4 p-5 "  placeholder="Ingrese el nombre" type="name" v-model="userValidate.name">

                <label class="uppercase text-2xl font-semibold mt-5" for="">Correo</label>
                <input class="border-2 rounded-md h-4 p-5 "  placeholder="Ingrese su Email" type="email" v-model="userValidate.email">


                <label class="uppercase text-2xl font-semibold mt-5" for="">Estado</label>
                
                <select class=" border-2 rounded-md h-11" name="estado" disabled="disabled " >
                    <option class="" value="Activo" selected>Activo - por defecto</option>
                    <option value="Inactivo" >Desativado</option>
                </select>

                <label class="uppercase font-semibold text- text-2xl mt-5 " for="">Celular</label>
                    <input class="border-2 rounded-md h-4 p-5 "  placeholder="Ingrese el número de celular" type="text" v-model="userValidate.phone">


                <label class="uppercase font-semibold text- text-2xl mt-5 " for="">Contraseña</label>
                <input class="border-2 rounded-md h-4 p-5 "  placeholder="Ingrese su Contraseña" type="password " v-model="userValidate.password">
                
                <label class="uppercase text-2xl font-semibold mt-5" for="">Rol</label>
                
                <select 
                class=" border-2 rounded-md h-11"
                v-model="userValidate.rol">
                >
                    <option value="">--Seleccione--</option>
                    <option value="Contratista">Contratista</option>
                    <option value="Planta" >Planta</option>
                </select>
                <input 
                class="w-full p-3 mt-6 rounded-md bg-green-800 hover:bg-green-700 cursor-pointer text-white" type="submit" value="Registrar">
            </form>
            <Alerta
            v-if="alerta.mensaje"
            :alerta="alerta"
            />
        </div>
    </div>
</template>


