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
      <DataInfo v-for="(item, index) in dataList" :key="index" v-bind="item" />
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
  mounted () {
    console.log('name:' + this.name)
  },
  methods: {
    addData () {
      this.dataList.push({
        name: this.name,
        email: this.email,
        english: this.english,
        math: this.math
      })
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
