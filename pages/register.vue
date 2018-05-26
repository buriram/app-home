<template>
  <div>
    <h1>Register Member.</h1>
    <v-text-field v-model="user" label="อีเมลล์" />
    <v-text-field v-model="pass" label="รหัสผ่าน" />
    <v-text-field v-model="first_name" label="ชื่อผู้ใช้" />
    <v-text-field v-model="last_name" label="นามสกุล" />
    <v-btn color="success" @click="save">บันทึก</v-btn>
  </div>
</template>
<script>
// http://localhost:3000/#/student/edit?id=1
export default {
  data() {
    return {
      user: '',
      pass: '',
      first_name: '',
      last_name: '',
    }
  },
  methods: {
    async save() {
      let res = await this.$http.post('/student/regis', {
        user: this.user,
        pass: this.pass,
        first_name: this.first_name,
        last_name: this.last_name,

      })
      if (!res.data.ok) {
        // TODO: แสดงข้อความ ว่าบันทึกไม่สำเร็จ
      } else {
        // TODO: แสดงข้อความ ว่าบันทึกสำเร็จ
        this.$router.push('/login')
      }
    },
  },
}
</script>
