<template>
  <div>
    <v-parallax src="/pic/background.png" height="643">
      <v-layout column align-center justify-center>
        <h1>Chat room</h1>
        <div>
          <v-text-field v-model="name" label="ชื่อ"/>
          <v-text-field v-model="text" label="ข้อความ"/>
          <v-btn @click="send">ส่ง</v-btn>
        </div>
        <ul>
          <li v-for="(m, idx) in msg" :key="idx">
            <b>{{ m.name }}</b> พูดว่า {{ m.text }}
          </li>
        </ul>
  </v-layout></v-parallax></div>
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
      name: '',
      text: '',
      msg: [],
    }
  }, // data
  created() {
    this.$socket.subscribe('room39', this.onMsg)
  },
  beforeDestroy() {
    this.$socket.unsubscribe('room39')
  },
  methods: {
    send() {
      this.$socket.publish('room39', {
        name: this.name,
        text: this.text,
      })
    },
    onMsg(data) {
      this.msg.unshift(data)
    },
  }, // methods
}
</script>
