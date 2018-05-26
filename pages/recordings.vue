<template>
  <div>
    <h1>Student List</h1>
    <v-container>
      <v-layout>
        <v-flex>
          <v-text-field v-model="user" label="กรอกรหัสเพื่อค้นหา" />
          <v-btn color="success" @click="getStd">ตกลง</v-btn>
        </v-flex>
      </v-layout>
      <v-layout>
        <v-flex>
          <v-data-table
            :headers="headers"
            :items="memos"
            class="elevation-1"
          >
            <template slot="items" slot-scope="props">
              <td>{{ props.item.sCode }}</td>
              <td>{{ props.item.mDate }}</td>
              <td>{{ props.item.mDetail }}</td>
            </template>
          </v-data-table>
        </v-flex>
      </v-layout>
    </v-container>
  </div>
</template>
<script>
export default {
  data() {
    return {
      memos: [],
      user: '',
      headers: [
        { text: 'รหัส', align: 'left', sortable: false },
        { text: 'ชื่อสกุล', align: 'left', sortable: false },
        { text: 'ห้อง', align: 'left', sortable: false },
      ],
    }
  }, // data
  async created() {
    this.getStd()
  },
  methods: {
    async getStd() {
      let res = await this.$http.get('/student/rds?user=' + this.user)
      this.memos = res.data.memo
    },
  },
}
</script>
