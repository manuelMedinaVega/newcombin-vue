<template>
    <div class="form-register">
        <input type="text" v-model="firstName" placeholder="First Name">
        <input type="text" v-model="lastName" placeholder="Last Name">
        <input type="text" v-model="address" placeholder="Address">
        <input type="text" v-model="ssn" placeholder="SSN">
        <button v-on:click="reset">Reset</button>
        <button v-on:click="save" :disabled="disable">Save</button>
    </div>
</template>

<script>
import axios from 'axios'
export default {
    name: 'RegistroUsuarios',
    mounted() {
        axios.post("http://localhost:8081/auth", {
            username: 'sarah',
            password: 'connor'
        }).then((resp) => {
            this.token = resp.data.token
        }).catch(() => {
            console.log('error auth');
        })
    },
    data() {
        return {
            firstName: '',
            lastName: '',
            address: '',
            ssn: '',
            token: ''
        }
    },
    methods: {
        reset() {
            this.firstName = ''
            this.lastName = ''
            this.address = ''
            this.ssn = ''
        },
        save() {
            axios.post('http://localhost:8081/api/members', {
                firstName: this.firstName,
                lastName: this.lastName,
                address: this.address,
                ssn: this.ssn
            }, {
                headers: { "Authorization": 'Bearer '+this.token }
            }).then(() => {
                this.$emit('nuevo', {
                    firstName: this.firstName,
                    lastName: this.lastName,
                    address: this.address,
                    ssn: this.ssn
                });
                this.reset()
            }).catch(() => {
                console.log('error al registrar')
            })
        }
    }, 
    computed: {
        disable() {
            return !this.firstName || !this.lastName || !this.address || !this.ssn
        }
    }
}
</script>

<style>
    .form-register input{
        display: block
    }
</style>