<template>
  <v-parallax src="/pic/background.png" height="643">
    <v-layout column align-center justify-center>
      <h1>Room Booking : {{ user.tFirstname || '' }}</h1>
      <v-flex xs12 lg6>
        <v-menu
          :close-on-content-click="false"
          v-model="menud"
          :nudge-right="40"
          lazy
          transition="scale-transition"
          offset-y
          full-width
          max-width="290px"
          min-width="290px"
        >
          <v-text-field
            slot="activator"
            v-model="computedDateFormatted"
            label="กรุณาเลือกวันที่"
            hint="MM/DD/YYYY format"
            persistent-hint
            prepend-icon="event"
            readonly
          />
          <v-date-picker v-model="date" no-title @input="menud = false"/>
        </v-menu>
        <p>Date in ISO format: <strong>{{ date }}</strong></p>
      </v-flex>
      <v-data-table
        :headers="headers"
        :items="bks"
        class="elevation-1"
      >
        <template slot="items" slot-scope="props">
          <td class="text-xs-left">{{ props.item.bDate }}</td>
          <td class="text-xs-left">{{ props.item.bTimein }}</td>
          <td class="text-xs-left">{{ props.item.user }}</td>
        </template>
      </v-data-table>

      <v-flex xs12 sm6/>
      <v-flex xs12 sm6>
        <v-select
          :items="states"
          v-model="e6"
          label="Select"
          multiple
          max-height="400"
          hint="กรุณาเลือกเวลา"
          persistent-hint
        />
        <v-btn color="warning" @click="Dosave">จองห้อง</v-btn>
      </v-flex>
    </v-layout>
    <div>
      <a>test</a>
    </div>
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
      bks: [],
      headers: [
        { text: 'วันที่', align: 'left', sortable: false },
        { text: 'เวลา', align: 'left', sortable: false },
        { text: 'ผู้จอง', align: 'left', sortable: false },

      ],
      e6: [],
      states: [
        '8.00-9.00', '9.00-10.00', '10.00-11.00', '11.00-12.00',
        '13.00-14.00', '14.00-15.00', '15.00-16.00', '16.00-17.00',
      ],
    }
  },
  computed: {
    filteredBooking() {
      return this.bks.filter(x => x.b_date + '' === this.date)
    },
    computedDateFormatted() {
      return this.formatDate(this.date)
    },
  },
  watch: {
    date (val) {
      this.dateFormatted = this.formatDate(this.date)
      this.getBooking()
    },
  },
  async created() {
    let ok = await JSON.parse(window.sessionStorage.getItem('user'))
    if (!ok) {
      return this.$router.replace('/login')
    }
    this.getBooking()
  },
  methods: {
    async getBooking() {
      let res = await this.$http.get('/student/booking?b_date=' + this.date)
      this.bks = res.data.bk
    },
    async Dosave() {
      let res = await this.$http.post('/student/save', {
        b_date: this.date,
        b_time: this.e6,
        user: this.user.tFirstname,
        keyRoom: ('' + Math.floor(Math.random() * 1000000)).padStart(6, '0'),
      })
      if (!res.data.ok) {
        // TODO: แสดงข้อความ ว่าบันทึกไม่สำเร็จ
      } else {
        // TODO: แสดงข้อความ ว่าบันทึกสำเร็จ
        this.$router.push('/booking')
      }
    },
    formatDate (date) {
      if (!date) return null

      const [year, month, day] = date.split('-')
      return `${month}/${day}/${year}`
    },
    parseDate (date) {
      if (!date) return null

      const [month, day, year] = date.split('/')
      return `${year}-${month.padStart(2, '0')}-${day.padStart(2, '0')}`
    },
  }, // methods
}
</script>
