<script setup>
    import axios from "axios";
    import {ref,reactive} from 'vue'
    import Alerta from './Alerta.vue'
    const userValidate = reactive({
        email:'',
        password:''
    })
    const alerta = reactive({
        tipo: '',
        mensaje: ''
    })

</script>
<template>
    <div class="mx-auto my-10 max-w-2xl bg-red-300 rounded-3xl ">
        <div class="p-10">
            <img class="w-32  mx-auto" src="../assets/img/Cherry_icon.png" alt="" srcset="">
            <h1 class="text-3xl text-center font-bold"><span class=" text-red-600">Cherry Stock</span> - Login</h1>
            <form @submit.prevent="loguearUsuario"
            class="flex flex-col px-5 mt-5 " method="post">
                <label class="uppercase text-2xl font-semibold " for="">Correo</label>
                <input class="border-2 rounded-md h-4 p-5 "  placeholder="Ingrese su Email" type="email" v-model="userValidate.email">

                <label class="uppercase font-semibold text- text-2xl mt-5 " for="">Contraseña</label>
                <input class="border-2 rounded-md h-4 p-5 "  placeholder="Ingrese su Contraseña" type="password " v-model="userValidate.password">

                <input 
                class="w-full p-3 mt-6 rounded-md bg-green-800 hover:bg-green-700 cursor-pointer text-white" type="submit" value="Iniciar Sesión">
            </form>
            <Alerta
            v-if="alerta.mensaje"
            :alerta="alerta"
            />
        </div>
    </div>
</template>


