<template>
  <div class="container">
    <div style="margin-top: 2%;margin-bottom: 1%">
      <el-input v-model="searchId" placeholder="请输入学生id"></el-input>
      <el-button type="primary" @click="search">查询</el-button>
    </div>
    <el-table :data="tableData.slice((currentPage - 1) * pageSize, currentPage * pageSize)" stripe border style="width: 100%" v-loading="loading">
      <el-table-column prop="id" label="id" width="130px"></el-table-column>
      <el-table-column prop="date" label="date" width="210"></el-table-column>
      <el-table-column prop="contest" label="contest" width="180px"></el-table-column>
      <el-table-column prop="rank" label="rank"></el-table-column>
      <el-table-column prop="performance" label="performance" width="120px"></el-table-column>
      <el-table-column prop="newRating" label="newRating" width="120px"></el-table-column>
      <el-table-column prop="diff" label="diff" width="80px"></el-table-column>
      <el-table-column prop="count" label="count"></el-table-column>
      <el-table-column prop="maxrating" label="maxrating"></el-table-column>
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
      axios.get('/stu/info/acmer/atcoder/all/1/100').then(res => {
        if (res.data.code === 200) {
          this.loading = false
          const msgInfo = res.data.data.records
          for (const item in msgInfo) {
            this.tableData.push({
              id: msgInfo[item].acId,
              date: msgInfo[item].acDate,
              contest: msgInfo[item].acContest,
              rank: msgInfo[item].acRank,
              performance: msgInfo[item].acPerformance,
              newRating: msgInfo[item].acNewrating,
              diff: msgInfo[item].acDiff,
              count: msgInfo[item].acCount,
              maxrating: msgInfo[item].acMaxrating
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
      axios.get(`/stu/info/acmer/atcoder/search/${this.searchId}`)
        .then(res => {
          if (res.data.code === 200) {
            // 清空表格数据
            this.tableData = []
            const result = res.data.data
            if (result) {
              this.tableData.push({
                id: result.acId,
                date: result.acDate,
                contest: result.acContest,
                rank: result.acRank,
                performance: result.acPerformance,
                newRating: result.acNewrating,
                diff: result.acDiff,
                count: result.acCount,
                maxrating: result.acMaxrating
              })
            }
            this.totalNum = this.tableData.length
            this.errorMsg = ''
          } else {
            this.totalNum = 0
            this.errorMsg = '用户不存在'
          }
        })
        .catch(error => {
          console.error(error)
          this.errorMsg = '查询失败'
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
