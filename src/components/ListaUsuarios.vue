<template>
    <div>
        <h1>Lista de usuarios</h1>
        <table>
            <tr>
                <th>First Name</th>
                <th>Last Name</th>
                <th>Address</th>
                <th>SSN</th>
            </tr>
            <tr v-for="(usuario, i) in usuarios" :key="i">
                <td>{{usuario.firstName}}</td>
                <td>{{usuario.lastName}}</td>
                <td>{{usuario.address}}</td>
                <td>{{usuario.ssn}}</td>
            </tr>
        </table>
    </div>
</template>

<script>
import axios from 'axios'
export default {
    name: 'ListaUsuarios',
    props: {
        usuario: Object
    },
    mounted() {
        axios.post("http://localhost:8081/auth", {
            username: 'sarah',
            password: 'connor'
        }).then((resp) => {
            this.token = resp.data.token
            this.getUsuarios()
        }).catch(() => {
            console.log('error auth');
        })
    },
    data() {
        return {
            usuarios: [],
            token: ''
        }
    },
    methods: {
        getUsuarios() {
            axios.get('http://localhost:8081/api/members', {
                headers: { "Authorization": 'Bearer '+this.token }
            }).then((resp) => {
                this.usuarios = resp.data
            }).catch(() => {
                console.log('error listar')
            })
        }
    },
    watch: {
        usuario(newUsuario) {
            if(newUsuario != {}) {
                this.usuarios.push(newUsuario)
            }
        }
    }
}
</script>

<style>
    table {
    font-family: arial, sans-serif;
    border-collapse: collapse;
    width: 100%;
    }

    td, th {
    border: 1px solid #dddddd;
    text-align: left;
    padding: 8px;
    }

    tr:nth-child(even) {
    background-color: #dddddd;
    }
</style>