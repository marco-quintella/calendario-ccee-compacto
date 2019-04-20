<template>
  <q-page class="flex flex-center">
    <div v-html="calendario"></div>
  </q-page>
</template>

<style>
</style>

<script>
import Axios from 'axios'

export default {
  name: 'PageIndex',
  data () {
    return {
      data: {
        startDate: '',
        endDate: '',
        tipoEvento: 'Todos'
      },
      calendario: ''
    }
  },
  async created () {
    for (let i = 1; i <= 30; i++) {
      let today = ''
      i <= 9 ? (today = '0' + i) : (today = i)
      this.data = {
        startDate: '04/' + today + '/2019',
        endDate: '04/30/2019',
        tipoEvento: 'Todos'
      }
      await Axios.post(
        'https://www.ccee.org.br/portal/faces/oracle/webcenter/portalapp/pages/publico/noticiaopiniao/eventos_calendario.jspx',
        {
          data: this.data }
      )
        .then(response => {
          this.calendario = this.calendario + '<br><br>' + response.data
        })
        .catch(error => console.error(error))
    }
  }
}
</script>
