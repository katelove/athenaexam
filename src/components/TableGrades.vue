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
        <th>
          <input
            type="text"
            class="form-control"
            v-model="name"
            placeholder="請輸入名字"
            :class="{
              'is-invalid': $v.name.$error
            }"
          />
          <div class="invalid-feedback">
            <!-- <span v-if="!$v.name.required" class="valiateWord"
              >名字不能為空</span
            > -->
            <span v-if="!$v.name.minLength" class="valiateWord"
              >名字至少為3位字元</span
            >
            <span v-if="!$v.name.maxLength" class="valiateWord"
              >名字不能超過10位字元</span
            >
            <span v-if="!$v.name.isName" class="valiateWord"
              >請輸入真實姓名，中英文不能同時有，不包含任何符號和數字</span
            >
          </div>
        </th>
        <th>
          <input
            type="email"
            v-model="email"
            placeholder="kate1234@gmail.com"
          />
        </th>
        <th>
          <input type="text" v-model.number="english" placeholder="70" />
        </th>
        <th>
          <input type="text" v-model.number="math" placeholder="80" />
        </th>
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
import { required, minLength, maxLength } from 'vuelidate/lib/validators'

// 驗證姓名
const isName = function (value) {
  const reg = /^([\u4E00-\u9FA5]+|[a-zA-Z]+)$/
  return reg.test(value)
}

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
  validations: {
    name: {
      required,
      minLength: minLength(3),
      maxLength: maxLength(10),
      isName
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
      localStorage.setItem('dataList', JSON.stringify(this.dataList))
      this.name = ''
      this.email = ''
      this.english = ''
      this.math = ''
    },
    dataUpdate (newData) {
      const origin = this.dataList

      // 把資料寫回原始陣列
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
        // 把更新後原始陣列儲存起來
        // using localStorage here to save data
        let arrayJason = JSON.parse(localStorage.getItem('dataList'))
        if (arrayJason.length !== 0) {
          arrayJason.forEach(function (item) {
            if (item.id === newData.id) {
              item.name = newData.name
              item.email = newData.email
              item.english = newData.english
              item.math = newData.math
            }
          })
          localStorage.setItem('dataList', JSON.stringify(arrayJason))
        }
      } else if (newData.event === 'del') {
        const d = origin.filter(item => {
          return (item.id = newData.id)
        })
        const index = origin.indexOf(d[0])
        origin.splice(index, 1)
        localStorage.setItem('dataList', JSON.stringify(origin))
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

.valiateWord {
  color: red;
  font-size: 10px;
  display: block;
}
input:focus {
  outline: 0;
  border: 1px solid #0066cc;
  box-shadow: 0px 0px 5px 0px #0066cc;
}
</style>
