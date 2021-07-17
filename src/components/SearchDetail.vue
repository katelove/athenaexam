<template>
  <!-- 查詢條件 -->
  <div class="searchInfo">
    <div class="searchTitle">
      <h2>查詢條件</h2>
    </div>
    <!-- 姓名 -->
    <div class="row detailSearch">
      <div class="col-sm-6 col-md-6 col-lg-4 col-xl-4 detailName">姓名 :</div>
      <div class="col-sm-6 col-md-6 col-lg-8 col-xl-8">
        <input type="text" />
      </div>
    </div>
    <!-- Email -->
    <div class="row detailSearch">
      <div class="col-sm-6 col-md-6 col-lg-4 col-xl-4 detailName">Email :</div>
      <div class="col-sm-6 col-md-6 col-lg-8 col-xl-8">
        <input type="text" />
      </div>
    </div>
    <!-- 成績查詢 -->
    <div class="row detailSearch">
      <div class="col-sm-6 col-md-6 col-lg-4 col-xl-4 detailName">
        成績查詢 :
      </div>
      <div class="col-sm-6 col-md-6 col-lg-8 col-xl-8">
        <b-form-checkbox-group
          id="radio-group-1"
          v-model="selected"
          class="gradesChoice"
          :options="gradesOptions"
          name="flavour-1"
        >
        </b-form-checkbox-group>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'SearchDetail',
  data () {
    return {
      types: ['text', 'email'],
      selected: [],
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
      ]
    }
  }
}
</script>

<style lang="scss">
@import '../scss/searchDetail.scss';
</style>
