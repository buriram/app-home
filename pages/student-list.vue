<template>
  <div>
    <h1>Student List</h1>
    <v-container>
      <v-layout>
        <v-flex>
          <v-data-table
            :headers="headers"
            :items="students"
            class="elevation-1"
          >
            <template slot="items" slot-scope="props">
              <td>{{ props.item.sCode }}</td>
              <td>{{ props.item.sName }}</td>
              <td>{{ props.item.sClass }}</td>
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
      students: [],
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
      let res = await this.$http.get('/student/list')
      this.students = res.data.student
    },
  },
}
</script>
