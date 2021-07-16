<template>
<div>
  <table>
    <thead>
      <tr>
        <th v-for='(item,index) in titleList' :key="index">{{item}}</th>
      </tr>
    </thead>
  </table>
</div>
</template>

<script>
export default {
  data () {
    return {
      titleList: ['動作', '姓名', 'email', '英文', '數學', '時間']
    }
  }
}
</script>
