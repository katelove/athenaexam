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
          <button class="bluePlus" @click="addData()">
            <h4>+</h4>
          </button>
        </th>
        <th>
          <input
            type="text"
            v-model.trim="name"
            placeholder="請輸入名字"
            :class="{
              'is-invalid': $v.name.$error
            }"
          />
          <div class="invalid-feedback">
            <span v-if="submitted && !$v.name.required" class="valiateWord"
              >名字不能為空</span
            >
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
            placeholder="請輸入信箱"
            class="mailInput"
            multiple
            :class="{
              'is-invalid': $v.email.$error
            }"
          />
          <div class="invalid-feedback">
            <span v-if="submitted && !$v.email.required" class="valiateWord"
              >信箱不能為空</span
            >
            <span v-if="!$v.email.isEmail" class="valiateWord"
              >請輸入正確多筆信箱(需包含@、正確mail address)
            </span>
          </div>
        </th>
        <th>
          <input
            type="text"
            v-model.number="english"
            placeholder="請輸入分數"
          />
        </th>
        <th>
          <input type="text" v-model.number="math" placeholder="請輸入分數" />
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

// 驗證多筆信箱
const isEmail = function (value) {
  if (value === undefined) {
    return true
  }
  const regexp = /^(([a-zA-Z\-0-9\\.]+@)([a-zA-Z\-0-9\\.]+)[,]*)+/g

  var mailNum = true
  // eslint-disable-next-line no-array-constructor
  let arr = []

  if (String(value).indexOf(',') !== -1) {
    arr = String(value).split(',')
  } else {
    arr.push(value)
  }

  for (var i = 0; i < arr.length; i++) {
    const reg = new RegExp(regexp)
    if (reg.test(arr[i]) === false) {
      mailNum = false
      console.log('this.mailNum:' + mailNum)
      break
    }
    // 每個函數都會有一個回傳值。如果你幫某個函數回傳了值，
    // 那就是告訴他你已經獲得到你要的資料了，可以結束執行了。
    // 那麼如果 arr 中第一個通過測試，就會直接結束 function。
  }

  return mailNum
}

// eslint-disable-next-line
const isEmail_v2 = function(value) {
  if (value === undefined) {
    return true
  }
  const regexp = /^(([a-zA-Z\-0-9\\.]+@)([a-zA-Z\-0-9\\.]+)[,]*)+/g

  var mailNum = value.match(regexp) === value

  return mailNum
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
      dataList: [],
      submitted: false,
      spaceRequired: false
    }
  },
  validations: {
    name: {
      required,
      minLength: minLength(3),
      maxLength: maxLength(10),
      isName
    },
    email: {
      required,
      isEmail
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
      this.handleSubmit()
      if (this.spaceRequired === true) {
        this.dataList.push({
          id: this.hashGenerator(16),
          name: this.name,
          email: this.email,
          english: this.english,
          math: this.math
        })
        // 新增物件到localstorage
        localStorage.setItem('dataList', JSON.stringify(this.dataList))
        this.name = ''
        this.email = ''
        this.english = ''
        this.math = ''
      }
    },
    handleSubmit (e) {
      this.submitted = true

      this.$v.$touch()
      if (this.$v.$invalid) {
        // eslint-disable-next-line no-useless-return
        if (this.$v.name.required === true && this.$v.email.required === true) {
          this.spaceRequired = true
        }
        return this.spaceRequired
      }
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
</style>
