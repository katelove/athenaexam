<template>
  <table id="gradesSty">
    <thead>
      <tr>
        <th class="gradesTitle" v-for="(item, index) in titleList" :key="index">
          {{ item }}
        </th>
      </tr>
      <tr>
        <th>
          <button class="bluePlus" @click="addData()"><h4>+</h4></button>
        </th>
        <th><input type="text" v-model="name" /></th>
        <th><input type="text" v-model="email" /></th>
        <th><input type="text" v-model="english" /></th>
        <th><input type="text" v-model="math" /></th>
        <th></th>
        <th></th>
      </tr>
    </thead>
    <tbody>
      <DataInfo
        v-for="(item, index) in dataList"
        :key="index"
        v-bind="item"
        @updated="dataUpdate($event)"
      />
    </tbody>
  </table>
</template>

<script>
import DataInfo from './DataInfo.vue'

export default {
  components: { DataInfo },
  name: 'TableGrades',
  props: ['name', 'email', 'english', 'math'],
  data () {
    return {
      titleList: [
        '動作',
        '姓名',
        '電子信箱',
        '英文',
        '數學',
        '新增時間',
        '修改時間'
      ],
      dataList: []
    }
  },
  methods: {
    // 產生id
    hashGenerator (digit) {
      const pattern =
        'ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789'
      let output = ''
      for (let i = 0; i < digit; i++) {
        output += pattern.charAt(Math.random() * pattern.length)
      }
      return output
    },
    // 新增
    addData () {
      this.dataList.push({
        id: this.hashGenerator(16),
        name: this.name,
        email: this.email,
        english: this.english,
        math: this.math
      })
      this.name = ''
      this.email = ''
      this.english = ''
      this.math = ''
    },
    dataUpdate (newData) {
      const origin = this.dataList
      if (newData.event === 'update') {
        origin.forEach((item, index) => {
          if (item.id === newData.id) {
            // eslint-disable-next-line no-unused-expressions
            item.name = newData.name
            // eslint-disable-next-line no-unused-expressions
            item.email = newData.email
            // eslint-disable-next-line no-unused-expressions
            item.english = newData.english
            // eslint-disable-next-line no-unused-expressions
            item.math = newData.math
          }
        })
      }
    }
  },
  component: {
    DataInfo
  }
}
</script>
<style lang="scss">
@import '../scss/tableGrades.scss';
</style>
