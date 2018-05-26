<template>
  <div>
    <h1>บันทึกข้อมูลการตรวจเยี่ยม.</h1>
    <v-text-field v-model="user" label="รหัสนักศึกษา" />
    <v-text-field v-model="detail" label="รายละเอียด" textarea />
    <v-text-field v-model="date" label="วันที่" />
    <v-btn color="success" @click="save">บันทึก</v-btn>
  </div>
</template>
<script>
// http://localhost:3000/#/student/edit?id=1
export default {
  data() {
    return {
      user: '',
      detail: '',
      date: this.$moment().format('YYYY-MM-DD'),
    }
  },
  methods: {
    async save() {
      let res = await this.$http.post('/student/save', {
        user: this.user,
        m_detail: this.detail,
        m_date: this.date,

      })
      if (!res.data.ok) {
        // TODO: แสดงข้อความ ว่าบันทึกไม่สำเร็จ
      } else {
        // TODO: แสดงข้อความ ว่าบันทึกสำเร็จ
        this.$router.push('/recordings')
      }
    },
  },
}
</script>
