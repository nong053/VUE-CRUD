<template>
   <div class="q-qutter-md" style="max-width: 400px">
        <q-form
            @submit="onSubmit"
            class="q-gutter-md"
        >
            <q-input v-model="id" label="ID"></q-input>
            <q-input v-model="fname" label="First Name"></q-input>
            <q-input v-model="lname" label="Last Name"></q-input>
            <q-input v-model="username" label="Username"></q-input>
            <q-input v-model="password" label="Password"></q-input>
            <q-input v-model="email" label="Email"></q-input>
            <q-input v-model="avatar" label="Avatar"></q-input>
            <q-btn label="Update" type="Submit" color="primary"></q-btn>
        </q-form>

        </div>
</template>
<script setup>

import {ref} from 'vue';

import {useRoute} from 'vue-router';
const router= useRoute()

const id = ref(router.params.id)
const fname=ref('')
const lname=ref('')
const username=ref('')
const password=ref('')
const email=ref('')
const avatar=ref('')


const fetchData=()=>{
    fetch("https://www.melivecode.com/api/users/"+id.value)
    .then(res=>res.json())
    .then((result)=>{
        fname.value=result.user.fname
        lname.value=result.user.fname
        username.value=result.user.username
        password.value=result.user.password
        email.value=result.user.email
        avatar.value=result.user.avatar
        
    })
}
fetchData()
const onSubmit=()=>{
    const myHeaders = new Headers();
    myHeaders.append("Content-Type", "application/json");

    const raw = JSON.stringify({
    "id": id.value,
    "fname": fname.value,
    "lname": lname.value,
    "username": username.value,
    "password": password.value,
    "email": email.value,
    "avatar": avatar.value

    });

    const requestOptions = {
    method: "PUT",
    headers: myHeaders,
    body: raw,
    redirect: "follow"
    };

    fetch("https://www.melivecode.com/api/users/update", requestOptions)
    .then((response) => response.json())
    .then((result) => {
        alert(result.message);
    })
    .catch((error) => console.error(error));
}

</script>