<template>
  <div class="container">
    <!-- 標題 -->
    <div class="row">
      <div class="col-sm-12 col-md-12 col-lg-12 col-xl-12">
        <div>
          <h1>成績輸入系統</h1>
        </div>
      </div>
    </div>
    <!-- 查詢條件 -->
    <div class="row">
      <div class="col-sm-12 col-md-12 col-lg-12 col-xl-12 centerSty">
        <div class="searchInfo">
          <div class="searchTitle">
            <h2>查詢條件</h2>
          </div>
          <!-- 姓名 -->
          <div class="row detailSearch">
            <div class="col-sm-6 col-md-6 col-lg-4 col-xl-4 detailName">
              姓名 :
            </div>
            <div class="col-sm-6 col-md-6 col-lg-8 col-xl-8">
              <input
                type="text"
                v-model.trim="searchData.searchName"
                @keyup.enter="inputHandler"
              />
            </div>
          </div>
          <!-- Email -->
          <div class="row detailSearch">
            <div class="col-sm-6 col-md-6 col-lg-4 col-xl-4 detailName">
              Email :
            </div>
            <div class="col-sm-6 col-md-6 col-lg-8 col-xl-8">
              <input
                type="text"
                v-model.trim="searchData.searchEmail"
                @keyup.enter="inputHandler"
              />
            </div>
          </div>
          <!-- 成績查詢 -->
          <div class="row detailSearch">
            <div class="col-sm-6 col-md-6 col-lg-4 col-xl-4 detailName">
              成績查詢 :
            </div>
            <div class="col-sm-6 col-md-6 col-lg-8 col-xl-8">
              <b-form-group label="英文">
                <b-form-checkbox-group
                  id="radio-group-1"
                  v-model="searchData.searchEnglish"
                  class="gradesChoice"
                  :options="gradesOptions"
                  name="flavour-1"
                >
                </b-form-checkbox-group>
              </b-form-group>
              <b-form-group label="數學">
                <b-form-checkbox-group
                  id="radio-group-2"
                  v-model="searchData.searchMath"
                  class="gradesChoice"
                  :options="gradesOptions"
                  name="flavour-1"
                >
                </b-form-checkbox-group>
              </b-form-group>
            </div>
          </div>
        </div>
      </div>
    </div>
    <div class="row">
      <div class="col-sm-12 col-md-12 col-lg-12 col-xl-12 centerSty">
        <TableGrades v-bind="searchData"></TableGrades>
      </div>
    </div>
  </div>
</template>

<script>
import TableGrades from './TableGrades.vue'
export default {
  name: 'GradesSystem',
  data () {
    return {
      searchData: {
        searchName: '',
        searchEmail: '',
        searchEnglish: '',
        searchMath: ''
      },
      selected: [],
      // gradesOptions: ['不及格', '等於及格', '大於及格'],
      gradesOptions: [
        {
          text: '不及格',
          value: '及格'
        },
        {
          text: '等於及格',
          value: '等於及格'
        },
        {
          text: '大於及格',
          value: '大於及格'
        }
      ],
      sender: {}
    }
  },
  methods: {
    inputHandler () {}
  },
  components: {
    TableGrades
  }
}
</script>

<style lang="scss">
.centerSty {
  display: flex;
  justify-content: center;
}
@import '../scss/searchDetail.scss';
</style>
