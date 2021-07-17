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
          <button class="bluePlus"><h4>+</h4></button>
        </th>
        <th v-for="(item, index) in inputList" :key="index">
          <input type="text" />
        </th>
        <th></th>
        <th></th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <th class="tableIcon">
          <div><font-awesome-icon icon="edit" /></div>
          <div><font-awesome-icon icon="trash-alt" /></div>
        </th>
      </tr>
    </tbody>
  </table>
</template>

<script>
export default {
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
      inputList: [] // 資料
    }
  },
  mounted () {
    // input欄位有4個
    for (var i = 0; i < 4; i++) {
      this.inputList.push({
        name: '',
        email: '',
        english: '',
        math: ''
      })
    }
  }
}
</script>
<style lang="scss">
@import '../scss/tableGrades.scss';
</style>
