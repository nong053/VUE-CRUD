<template>
  
        <div class="q-qutter-md" style="max-width: 400px">
        <q-form
            @submit="onSubmit"
            class="q-gutter-md"
        >

            <q-input v-model="fname" label="First Name"></q-input>
            <q-input v-model="lname" label="Last Name"></q-input>
            <q-input v-model="username" label="Username"></q-input>
            <q-input v-model="password" label="Password"></q-input>
            <q-input v-model="email" label="Email"></q-input>
            <q-input v-model="avatar" label="Avatar"></q-input>
            <q-btn label="Submit" type="Submit" color="primary"></q-btn>
        </q-form>

        </div>
   
</template>

<script setup>
import {ref} from 'vue'
import router from '@/router';
const fname=ref('Karn')
const lname=ref('Yong')
const username=ref('karn.yong@melivecode.com')
const password=ref('1234')
const email=ref('agc@agc.com')
const avatar=ref('https://www.melivecode.com/users/1.png')

    const onSubmit=()=>{
        const myHeaders = new Headers();
        myHeaders.append("Content-Type", "application/json");

        const raw = JSON.stringify({
        "fname": fname.value,
        "lname": lname.value,
        "username": username.value,
        "password": password.value,
        "email": email.value,
        "avatar": avatar.value
        });

        const requestOptions = {
        method: "POST",
        headers: myHeaders,
        body: raw,
        redirect: "follow"
        };

        fetch("https://www.melivecode.com/api/users/create", requestOptions)
        .then((response) => response.json())
        .then((result) => {
            alert(result.message)
            console.log(result);
           
                router.push('/')
            
        })
        .catch((error) => console.error(error));
    }
</script>