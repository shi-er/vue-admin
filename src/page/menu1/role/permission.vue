<template>
  <div style="padding: 20px;">
    <el-table
      :data="tableData"
      style="width: 100%">
      <el-table-column
        label="权限id">
        <template slot-scope="scope">
          <span>{{scope.row.id}}</span>
        </template>
      </el-table-column>
      <el-table-column
        label="PID">
        <template slot-scope="scope">
          <span>{{scope.row.pid}}</span>
        </template>
      </el-table-column>
      <el-table-column
        label="标题">
        <template slot-scope="scope">
          <span>{{ scope.row.title }}</span>
        </template>
      </el-table-column>
      <el-table-column
        label="类型">
        <template slot-scope="scope">
          <span>{{scope.row.type}}</span>
        </template>
      </el-table-column>
      <el-table-column
        label="状态">
        <template slot-scope="scope">
          <span>{{scope.row.state}}</span>
        </template>
      </el-table-column>
      <el-table-column
        label="地址">
        <template slot-scope="scope">
          <span>{{scope.row.url}}</span>
        </template>
      </el-table-column>
      <el-table-column
        label="权限code">
        <template slot-scope="scope">
          <span>{{scope.row.permcode}}</span>
        </template>
      </el-table-column>
      <el-table-column
        label="排序">
        <template slot-scope="scope">
          <span>{{scope.row.sort}}</span>
        </template>
      </el-table-column>
      <el-table-column
        label="描述">
        <template slot-scope="scope">
          <span>{{scope.row.description}}</span>
        </template>
      </el-table-column>
    </el-table>
    <el-col :span="24" class="toolbar">
      <el-pagination
        @size-change="handleSizeChange"
        @current-change="handleCurrentChange"
        :page-sizes="[5, 10, 20, 50]"
        :page-size="10"
        layout="total, sizes, prev, pager, next, jumper"
        :total="total">
      </el-pagination>
    </el-col>
  </div>
</template>

<script>
  import axios from 'axios';
  import qs from 'qs';

  export default {
    name: "permission",
    data() {
      return {
        total: 0,
        currentPage: 1,
        pageSize: 10,
        tableData: []
      }
    }
    ,
    methods: {
      handleCurrentChange(val) {
        this.currentPage = val;
        this.getData();
      },
      handleSizeChange(val) {
        this.pageSize = val;
        this.getData();
      },
      getData() {
        const url = '/basic/permission/list?_index=' + ((this.currentPage - 1) * this.pageSize) + '&_size=' + this.pageSize;
        axios.get(url,
          qs.stringify({})).then((response) => {
          this.tableData = response.data.rows;
          this.total = response.data.total;
        }).catch((error) => {
          console.log(error);
        });
      }
      ,
      getCurrentDateTime(date) {
        return moment(date).format('YYYY-MM-DD HH:mm:ss')
      }
    }
    ,
    mounted() {
      this.getData();
      console.info(this.tableData);
    }
    ,
  }
</script>

<style scoped>

</style>
