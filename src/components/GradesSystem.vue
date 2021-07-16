<template>
  <div class="container">
    <div class="row">
      <div class="col-sm-12 col-md-12 col-lg-12 col-xl-12">
        <!-- 標題 -->
        <div>
          <h1>成績輸入系統</h1>
        </div>
        <!-- 查詢條件 -->
        <div>
          <h2>查詢條件</h2>
          <!-- 姓名 -->
          <div class="row detail-search-line">
            <div class="col-sm-6 col-md-6 col-lg-4 col-xl-4">姓名</div>
            <div class="col-sm-6 col-md-6 col-lg-8 col-xl-8">
              <input type="text" />
            </div>
          </div>
          <!-- Email -->
          <div class="row detail-search-line">
            <div class="col-sm-6 col-md-6 col-lg-4 col-xl-4">Email</div>
            <div class="col-sm-6 col-md-6 col-lg-8 col-xl-8">
              <input type="text" />
            </div>
          </div>
          <!-- 成績查詢 -->
          <div class="row detail-search-line">
            <div class="col-sm-6 col-md-6 col-lg-4 col-xl-4">成績查詢</div>
            <div class="col-sm-6 col-md-6 col-lg-8 col-xl-8">
                <b-form-checkbox-group
               id="radio-group-1"
               v-model="selected"
               class="mb-3"
               :options="gradesOptions"
               name="flavour-1">
                <!-- <p style="color:red">{{errors[0]}}</p> -->
                </b-form-checkbox-group>
            </div>
          </div>
        </div>
      </div>
    </div>
    <div class="row">
      <div class="col-sm-12 col-md-12 col-lg-12 col-xl-12">
        <TableGrades></TableGrades>
      </div>
    </div>
  </div>
</template>

<script>
import TableGrades from './TableGrades.vue'
export default {
  data () {
    return {
      selected: [],
      gradesOptions: [
        { text: '不及格', value: '及格' },
        { text: '等於及格', value: '等於及格' },
        { text: '大於及格', value: '大於及格' }
      ]
    }
  },
  components: {
    TableGrades
  }
}
</script>

<style lang="scss">
.detail-search-line {
  display: flex;
  justify-content: center;
}
</style>
