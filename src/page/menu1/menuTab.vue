<template>
  <div class="tab-content">
    <el-tabs v-model="activeName" @tab-click="handleClick">
      <el-tab-pane label="权限管理" name="first">
        <permission/>
      </el-tab-pane>
      <el-tab-pane label="角色管理" name="second">
        <role/>
      </el-tab-pane>
      <el-tab-pane label="用户角色" name="third">
        <roleUser/>
      </el-tab-pane>
      <!--<el-tab-pane label="定时任务补偿" name="fourth">定时任务补偿</el-tab-pane>-->
    </el-tabs>
  </div>
</template>
<script>
  import axios from 'axios';
  import qs from 'qs';
  import permission from './role/permission';
  import role from './role/role';
  import roleUser from './role/roleUser';

  export default {
    data() {
      return {
        activeName: 'first',
        permCode: '',
        type: ''
      };
    },
    methods: {
      handleClick(tab, event) {
        console.log(tab, event);
      }
    },
    mounted() {

    },
    components: {
      permission,
      role,
      roleUser
    }
  };
</script>

<style lang="css">
</style>
