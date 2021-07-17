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
      <div class="col-sm-12 col-md-12 col-lg-12 col-xl-12">
        <SearchDetail></SearchDetail>
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
import SearchDetail from './SearchDetail.vue'
import TableGrades from './TableGrades.vue'
export default {
  name: 'GradesSystem',
  components: {
    SearchDetail,
    TableGrades
  }
}
</script>
