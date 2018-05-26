<template>
  <v-parallax src="/pic/background.png" height="643">
    <v-layout column align-center justify-center>
      <h1>Room Booking : {{ user.tFirstname || '' }}</h1>
      <v-data-table
        :headers="headers"
        :items="kroom"
        class="elevation-1"
      >
        <template slot="items" slot-scope="props">
          <td class="text-xs-left">{{ props.item.bDate }}</td>
          <td class="text-xs-left">{{ props.item.bTimein }}</td>
          <td class="text-xs-left">{{ props.item.keyroom }}</td>
        </template>
      </v-data-table>

      <v-flex xs12 sm6/>
    </v-layout>
  </v-parallax>
</template>
<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1, h2 {
  font-weight: normal;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
<script>

export default {
  data() {
    return {
      user: JSON.parse(window.sessionStorage.getItem('user')),
      date: this.$moment().format('YYYY-MM-DD'),
      dateFormatted: null,
      menud: false,
      kroom: [],
      bks: [],
      headers: [
        { text: 'วันที่', align: 'left', sortable: false },
        { text: 'เวลา', align: 'left', sortable: false },
        { text: 'รหัสเข้า', align: 'left', sortable: false },

      ],
    }
  },
  async created() {
    let ok = await JSON.parse(window.sessionStorage.getItem('user'))
    if (!ok) {
      return this.$router.replace('/login')
    }
    this.getKeyroom()
  },
  methods: {
    async getKeyroom() {
      let res = await this.$http.get('/student/getRoom?user=' + this.user.tFirstname)
      this.kroom = res.data.krr
    },
  }, // methods
}
</script>
