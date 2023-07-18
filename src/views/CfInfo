<template>
  <div class="container">
    <div style="margin-top: 2%;margin-bottom: 1%">
      <el-input v-model="searchId" placeholder="请输入学生cf-id"></el-input>
      <el-button type="primary" @click="search">查询</el-button>
    </div>
    <el-table :data="tableData.slice((currentPage - 1) * pageSize, currentPage * pageSize)" stripe border style="width: 100%" v-loading="loading">
      <el-table-column prop="cfId" label="cfId" width="160px"></el-table-column>
      <el-table-column prop="cfContest" label="cfContest" width="220"></el-table-column>
      <el-table-column prop="cfContestId" label="cfContestId" width="210"></el-table-column>
      <el-table-column prop="cfRank" label="cfRank" width="100px"></el-table-column>
      <el-table-column prop="cfOldRating" label="cfOldRating" width="100px"></el-table-column>
      <el-table-column prop="cfNewRating" label="cfNewRating" width="100px"></el-table-column>
      <el-table-column prop="cfSumContest" label="cfSumConteset" width="130px"></el-table-column>
      <el-table-column prop="cfDate" label="cfDate" width="180px"></el-table-column>
      <!--      <el-table-column  label="操作" width="100px">
            <template slot-scope="scope">
              <el-button @click="handleEdit(scope.row)" type="text" size="small">编辑</el-button>
              <el-button @click="handleDel(scope.row)" type="text" size="small">删除</el-button>
            </template>
            </el-table-column>-->
    </el-table>
    <div class="block">
      <el-pagination
        layout="prev, pager, next"
        :total="totalNum"
        :page-size="pageSize"
        :current-page="currentPage"
        @current-change="handleCurrentChange"
      ></el-pagination>
    </div>
  </div>
</template>

<script>
import axios from 'axios'
export default {
  data () {
    return {
      pageSize: 7, // 表示一页多少条数据
      totalNum: 0,
      currentPage: 1,
      tableData: [],
      loading: true,
      searchId: '',
      errorMsg: '' // 添加errorMsg变量用于显示查询失败的提示信息
    }
  },
  created () {
    this.getInfo()
  },
  methods: {
    getInfo () {
      axios.get('/stu/info/acmer/codeforces/all/1/100').then(res => {
        if (res.data.code === 200) {
          this.loading = false
          const msgInfo = res.data.data.records
          for (const item in msgInfo) {
            this.tableData.push({
              cfId: msgInfo[item].cfId,
              cfContest: msgInfo[item].cfContest,
              cfContestId: msgInfo[item].cfContestId,
              cfRank: msgInfo[item].cfRank,
              cfOldRating: msgInfo[item].cfOldRating,
              cfNewRating: msgInfo[item].cfNewRating,
              cfSumContest: msgInfo[item].cfSumContest,
              cfDate: msgInfo[item].cfDate
            })
          }
          this.totalNum = this.tableData.length
        }
      })
    },
    handleCurrentChange (val) {
      this.currentPage = val
    },
    search () {
      // 发送查询请求，根据学生id查询信息
      axios.get(`/stu/info/acmer/codeforces/search/${this.searchId}`)
        .then(res => {
          if (res.data.code === 200) {
            // 清空表格数据
            this.tableData = []
            const result = res.data.data
            if (result) {
              this.tableData.push({
                cfId: result.cfId,
                cfContest: result.cfContest,
                cfcontestId: result.cfcontestId,
                cfRank: result.cfRank,
                cfOldRating: result.cfOldRating,
                cfNewRating: result.cfNewRating,
                cfSumContest: result.cfSumContest,
                cfDate: result.cfDate
              })
            }
            this.totalNum = this.tableData.length
            this.errorMsg = ''
          } else {
            this.tableData = []
            this.totalNum = 0
            this.errorMsg = '用户不存在'
          }
        })
    }

  }
}
</script>

<style scoped>
.container {
  width: 100%;
  background-color: white;
  box-sizing: border-box;
  border-bottom: #eceef0 solid 2px;
  padding: 0px 18px;
}
.headBox {
  width: 100%;
  height: 75px;
  display: flex;
  align-items: center;
  box-sizing: border-box;
}
.headBox p {
  display: flex;
  justify-content: center;
  align-items: center;
}
.headBox p span {
  display: inline-block;
  width: 70px;
  margin-right: 5px;
  color: #7a7d7f;
  font-weight: bold;
}
.headBox p:nth-child(1) span,
.headBox p:nth-child(2) span {
  margin-right: -10px;
}
.headBox p:nth-child(2) span,
.headBox p:nth-child(3) span,
.headBox button {
  margin-left: 7px;
}
.headBox button span {
  margin-left: 5px;
}
.container .block {
  display: flex;
  justify-content: center;
  margin-top: 5px;
}
</style>
