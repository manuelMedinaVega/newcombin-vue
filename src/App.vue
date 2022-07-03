<template>
  <RegistroUsuarios @nuevo="send" />
  <ListaUsuarios :usuario="usuario" />
</template>

<script>
import RegistroUsuarios from './components/RegistroUsuarios.vue'
import ListaUsuarios from './components/ListaUsuarios.vue'
export default {
  name: 'App',
  mounted() {
    console.log('app mounted')
  },
  components: {
    RegistroUsuarios,
    ListaUsuarios
  },
  data() {
    return {
      token: '',
      usuario: {}
    }
  },
  methods: {
    send(data) {
      this.usuario = data
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
