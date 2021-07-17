<template>
  <tr class="tdInputSty">
    <th class="tableIcon">
      <div><font-awesome-icon icon="edit" @click="editBtn()" /></div>
      <div><font-awesome-icon icon="trash-alt" @click="del()" /></div>
    </th>
    <td>
      <span v-if="!edit">{{ name }}</span>
      <input type="text" v-if="edit" v-model="name" />
    </td>
    <td>
      <span v-if="!edit">{{ email }}</span>
      <input type="text" v-if="edit" v-model="email" />
    </td>
    <td>
      <span v-if="!edit">{{ english }}</span>
      <input type="text" v-if="edit" v-model="english" />
    </td>
    <td>
      <span v-if="!edit">{{ math }}</span>
      <input type="text" v-if="edit" v-model="math" />
    </td>
    <td></td>
    <td></td>
  </tr>
</template>

<script>
export default {
  name: 'DataInfo',
  props: ['name', 'email', 'english', 'math'],
  data () {
    return {
      edit: false
    }
  },
  watch: {
    data: 'onchange'
  },
  methods: {
    onchange () {
      this.$emit('updated', {
        name: this.name,
        email: this.email,
        english: this.english,
        math: this.math,
        event: 'update'
      })
    },
    editBtn () {
      // edit按鈕流程: 1)一開始 edit false
      // 2)按一次 狀態false 變true 編輯
      // 3)再按一次 狀態true變false 呼叫update
      // == 為判斷式,===包含判斷型態
      // eslint-disable-next-line no-unused-expressions
      this.edit = !this.edit
      if (this.edit === true) {
        // eslint-disable-next-line no-unused-expressions
        this.edit = true
      } else {
        onchange()
      }
    }
  }
}
</script>

<style lang="scss">
.tdInputSty {
  input {
    width: 80px;
    height: 28px;
    border-radius: 5px;
    border: 1px solid gray;
  }
}
</style>
