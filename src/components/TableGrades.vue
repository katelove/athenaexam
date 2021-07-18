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
            @input="isName()"
          />
          <div class="invalid-feedback">
            <span
              v-if="dataVarify.name.error && dataVarify.name.msg == 'empty'"
              class="valiateWord"
              >名字不能為空</span
            >
            <span
              v-if="dataVarify.name.error && dataVarify.name.msg == 'max'"
              class="valiateWord"
              >名字不能超過10位字元</span
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
            @input="isEmail()"
          />
          <div class="invalid-feedback">
            <span
              v-if="dataVarify.email.error && dataVarify.email.msg == 'empty'"
              class="valiateWord"
              >信箱不能為空</span
            >
            <span
              v-if="dataVarify.email.error && dataVarify.email.msg == 'invalid'"
              class="valiateWord"
              >請輸入正確信箱(需包含@、正確mail address)
            </span>
          </div>
        </th>
        <th>
          <input
            type="text"
            v-model="english"
            placeholder="請輸入分數"
            @input="isGrades('english')"
          />
          <div class="invalid-feedback">
            <span
              v-if="
                dataVarify.english.error && dataVarify.english.msg == 'empty'
              "
              class="valiateWord"
              >分數不能為空</span
            >
            <span
              v-if="
                dataVarify.english.error && dataVarify.english.msg == 'number'
              "
              class="valiateWord"
              >請輸入正確成績(分數範圍 0~100)
            </span>
          </div>
        </th>
        <th>
          <input
            type="text"
            v-model.number="math"
            placeholder="請輸入分數"
            @input="isGrades('math')"
          />
          <div class="invalid-feedback">
            <span
              v-if="dataVarify.math.error && dataVarify.math.msg == 'empty'"
              class="valiateWord"
              >分數不能為空</span
            >
            <span
              v-if="dataVarify.math.error && dataVarify.math.msg == 'number'"
              class="valiateWord"
              >請輸入正確成績(分數範圍 0~100)
            </span>
          </div>
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
      dataVarify: {
        name: {
          error: false,
          msg: 'empty'
        },
        email: {
          error: false,
          msg: 'invalid'
        },
        english: {
          error: false,
          msg: 'number'
        },
        math: {
          error: false,
          msg: 'number'
        }
      }
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
      // chk欄位是否為空值
      this.chkValue()
      // this.handleSubmit()
      if (this.submitted === true) {
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
    chkValue () {
      console.log('this.name:' + this.name)
      if (
        this.name === undefined ||
        this.email === undefined ||
        this.english === undefined ||
        this.math === undefined
      ) {
        if (this.name === undefined) {
          this.dataVarify.name.error = true
          this.dataVarify.name.msg = 'empty'
          this.submitted = false

          if (this.email === undefined) {
            this.dataVarify.email.error = true
            this.dataVarify.email.msg = 'empty'
            this.submitted = false
            if (this.english === undefined) {
              this.dataVarify.english.error = true
              this.dataVarify.english.msg = 'empty'
              this.submitted = false
              if (this.math === undefined) {
                this.dataVarify.math.error = true
                this.dataVarify.math.msg = 'empty'
                this.submitted = false
                return this.submitted
              }
              return this.submitted
            }
            return this.submitted
          }
          return this.submitted
        }
      } else {
        this.submitted = true
        return this.submitted
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
    },
    // 驗證姓名
    isName () {
      if (this.name === '') {
        this.dataVarify.name.error = true
        this.dataVarify.name.msg = 'empty'
        return false
      } else if (this.name.length > 10) {
        this.dataVarify.name.error = true
        this.dataVarify.name.msg = 'max'
        return false
      } else {
        this.dataVarify.name.error = false
        this.dataVarify.name.msg = ''
        return true
      }
    },
    // 驗證信箱
    isEmail () {
      if (this.email === '') {
        this.dataVarify.email.error = true
        this.dataVarify.email.msg = 'empty'
        return false
      } else {
        const regexp = /^(([a-zA-Z\-0-9\\.]+@)([a-zA-Z\-0-9\\.]+)[,]*)+/g
        let arr = []
        var mailNum = true
        if (String(this.email).indexOf(',') !== -1) {
          arr = String(this.email).split(',')
        } else {
          arr.push(this.email)
        }

        for (var i = 0; i < arr.length; i++) {
          const reg = new RegExp(regexp)
          if (reg.test(arr[i]) === false) {
            mailNum = false
            this.dataVarify.name.error = true
            this.dataVarify.name.msg = 'invalid'
            console.log('this.mailNum:' + mailNum)
            break
          }
        }
        return true
      }
    },
    // 驗證分數
    isGrades (type) {
      var dataVarify = null
      var data = null

      if (type === 'english') {
        dataVarify = this.dataVarify.english
        console.log('this.english:' + this.english)
        data = this.english
      } else {
        dataVarify = this.dataVarify.math
        data = this.math
      }

      if (data === '') {
        dataVarify.error = true
        dataVarify.msg = 'empty'
        return false
      } else {
        const reg = /^(\d|[1-9]\d|^100)$/
        if (reg.test(data) === false) {
          dataVarify.error = true
          dataVarify.msg = 'number'
          return false
        } else {
          dataVarify.error = false
          dataVarify.msg = ''
          return true
        }
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
