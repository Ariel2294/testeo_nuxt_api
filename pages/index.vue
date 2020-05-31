<template>
  <div class="container">
    <div>
      <logo />
      <h1 class="title">testeo_nuxt</h1>
      <h2 class="subtitle">My phenomenal Nuxt.js project</h2>
      <div class="links">
        <table>
          <thead>
            <th>Nombre</th>
            <th>edad</th>
          </thead>

          <tbody>
            <tr v-for="(usuario, index) in usuarios" :key="index">
              <td>{{ usuario.nombre }} {{ usuario.apellido }}</td>
              <td>{{ usuario.edad }}</td>
            </tr>
          </tbody>
        </table>

        <table>
          <thead>
            <th>tipo</th>
          </thead>

          <tbody>
            <tr v-for="(bebida, index) in bebidas" :key="index">
              <td>{{ bebida.tipo }}</td>
            </tr>
          </tbody>
        </table>
      </div>
    </div>
  </div>
</template>

<script>
import Logo from '~/components/Logo.vue'
export default {
  components: {
    Logo
  },

  async asyncData({ $axios, params }) {
    const data_user = await $axios.get(
      `https://api.server.saynets.com/usuarios`
    )
    const data_bebidas = await $axios.get(
      `https://api.server.saynets.com/bebidas`
    )

    return { bebidas: data_bebidas.data.ok, usuarios: data_user.data.ok }
  },
  beforeMount() {
    // this.$axios
    //   .get('https://api-bebidas-ugb.herokuapp.com/usuarios')
    //   .then(result => {
    //     this.usuarios = result.data.ok.map(element => {
    //       return {
    //         usuario: `${element.nombre} ${element.apellido}`,
    //         edad: element.edad
    //       }
    //     })
    //   })
    console.log(this.bebidas)
    console.log(this.usuarios)
  }
}
</script>

<style>
.container {
  margin: 0 auto;
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
}

.title {
  font-family: 'Quicksand', 'Source Sans Pro', -apple-system, BlinkMacSystemFont,
    'Segoe UI', Roboto, 'Helvetica Neue', Arial, sans-serif;
  display: block;
  font-weight: 300;
  font-size: 100px;
  color: #35495e;
  letter-spacing: 1px;
}

.subtitle {
  font-weight: 300;
  font-size: 42px;
  color: #526488;
  word-spacing: 5px;
  padding-bottom: 15px;
}

.links {
  padding-top: 15px;
}
</style>
