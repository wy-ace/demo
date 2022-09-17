<template>
  <div class="HW">
    <el-radio-group v-model="isCollapse" style="margin: 20px 0">
      <el-radio-button :label="true">卡片</el-radio-button>
      <el-radio-button :label="false">列表</el-radio-button>
    </el-radio-group>
    <div class="card" v-show="isCollapse">
      <ul>
        <li v-for="(item, index) in datas" :key="index">
          <div class="left">
            <img :src="require('../assets/imgs/' + item.logo)" alt="" />
          </div>
          <div class="center">
            <h2>{{ item.prjName }}</h2>
            <p>项目经理：{{ item.prjManager }}</p>
            <p>立项日期：{{ item.prjStartDate.substr(0, 10) }}</p>
            <template v-if="item.taskCount !== null">
              <p>
                任务：{{ item.taskCount }} 完成：{{
                  item.taskDoneCount
                }}
                进行：{{ item.taskDoingCount }}
              </p>
            </template>
          </div>
          <div class="right">
            <p v-if="item.projectStatus === '进行中'">
              <svg t="1663397833007"
                class="icon"
                viewBox="0 0 1024 1024"
                version="1.1"
                xmlns="http://www.w3.org/2000/svg"
                p-id="11296"
                width="10"
                height="10"
              >
                <path
                  d="M514.048 128q79.872 0 149.504 30.208t121.856 82.432 82.432 122.368 30.208 150.016q0 78.848-30.208 148.48t-82.432 121.856-121.856 82.432-149.504 30.208-149.504-30.208-121.856-82.432-82.432-121.856-30.208-148.48q0-79.872 30.208-150.016t82.432-122.368 121.856-82.432 149.504-30.208z"
                  p-id="11297"
                  data-spm-anchor-id="a313x.7781069.0.i14"
                  class="selected"
                  fill="#1296db"
                ></path></svg
              >进行中
            </p>
            <p v-else>
              <svg
                t="1663397833007"
                class="icon"
                viewBox="0 0 1024 1024"
                version="1.1"
                xmlns="http://www.w3.org/2000/svg"
                p-id="11296"
                width="10"
                height="10"
              >
                <path
                  d="M514.048 128q79.872 0 149.504 30.208t121.856 82.432 82.432 122.368 30.208 150.016q0 78.848-30.208 148.48t-82.432 121.856-121.856 82.432-149.504 30.208-149.504-30.208-121.856-82.432-82.432-121.856-30.208-148.48q0-79.872 30.208-150.016t82.432-122.368 121.856-82.432 149.504-30.208z"
                  p-id="11297"
                  data-spm-anchor-id="a313x.7781069.0.i14"
                  class="selected"
                  fill="#ff4e33"
                ></path></svg
              >审核中
            </p>
            <p>⭐</p>
          </div>
        </li>
      </ul>
    </div>
    <div style="border: 1px solid #eee; border-bottom: 0" v-show="!isCollapse">
      <el-table :data="datas" stripe style="width: 100%" empty-text="暂无数据">
        <el-table-column prop="icon" label="" width="50"></el-table-column>
        <el-table-column prop="productCategory" label="所属品类">
        </el-table-column>
        <el-table-column
          prop="prjCategory"
          :show-overflow-tooltip="true"
          label="项目类别"
        >
        </el-table-column>
        <el-table-column prop="address" label="项目编号" width="100">
        </el-table-column>
        <el-table-column prop="prjName" label="项目名称"> </el-table-column>
        <el-table-column prop="projectStatus" label="项目状态">
          <template slot-scope="scope">
            <div v-if="scope.row.projectStatus === '进行中'" v-html='`<svg t="1663397833007"
                class="icon"
                viewBox="0 0 1024 1024"
                version="1.1"
                xmlns="http://www.w3.org/2000/svg"
                p-id="11296"
                width="10"
                height="10"
              >
                <path
                  d="M514.048 128q79.872 0 149.504 30.208t121.856 82.432 82.432 122.368 30.208 150.016q0 78.848-30.208 148.48t-82.432 121.856-121.856 82.432-149.504 30.208-149.504-30.208-121.856-82.432-82.432-121.856-30.208-148.48q0-79.872 30.208-150.016t82.432-122.368 121.856-82.432 149.504-30.208z"
                  p-id="11297"
                  data-spm-anchor-id="a313x.7781069.0.i14"
                  class="selected"
                  fill="#1296db"
                ></path></svg
              >进行中`'></div>
            <div v-if="scope.row.projectStatus === '审核中'" v-html='`
            <svg
                t="1663397833007"
                class="icon"
                viewBox="0 0 1024 1024"
                version="1.1"
                xmlns="http://www.w3.org/2000/svg"
                p-id="11296"
                width="10"
                height="10"
              >
                <path
                  d="M514.048 128q79.872 0 149.504 30.208t121.856 82.432 82.432 122.368 30.208 150.016q0 78.848-30.208 148.48t-82.432 121.856-121.856 82.432-149.504 30.208-149.504-30.208-121.856-82.432-82.432-121.856-30.208-148.48q0-79.872 30.208-150.016t82.432-122.368 121.856-82.432 149.504-30.208z"
                  p-id="11297"
                  data-spm-anchor-id="a313x.7781069.0.i14"
                  class="selected"
                  fill="#ff4e33"
                ></path></svg
              >审核中
            `'></div>
          </template>
        </el-table-column>
        <el-table-column prop="prjManager" label="项目经理"> </el-table-column>
        <el-table-column prop="department" label="所属部门"> </el-table-column>
        <el-table-column prop="plainTime" label="项目计划时间" min-width="100">
        </el-table-column>
      </el-table>
    </div>
  </div>
</template>

<script>
import sendData from "../assets/data.json";
// 数据比较简单，不用vuex管理
export default {
  data() {
    return {
      isCollapse: true,
      datas: [],
    };
  },
  mounted() {
    this.datas = sendData;
    this.datas.forEach((item) => {
      let startTime = item.prjStartDate.substr(0, 10);
      let endTime = item.prjEndDate.substr(0, 10);
      this.$set(item, "icon", "⭐");
      this.$set(item, "plainTime", startTime + " ~ " + endTime);
      item.projectStatus =
        item.projectStatus === "processing" ? `进行中` : `审核中`;
      // item.logo = require(`../assets/imgs/${item.logo}`)
    });
  },
};
</script>

<style>
* {
  margin: 0;
  padding: 0;
  list-style: none;
}
img {
  width: 60px;
  height: 60px;
}
.HW .el-table tr th {
  color: black;
}
.HW {
  margin: 0 5%;
}
.HW .el-radio-button__orig-radio:checked + .el-radio-button__inner {
  background-color: #fff;
  color: #70b7ff;
}
.HW .el-radio-group {
  display: block;
  text-align: right;
}
.HW .card ul {
  overflow: hidden;
  min-width: 600px;
}
.HW .card ul li {
  height: 100px;
  float: left;
  display: flex;
  justify-content: flex-start;
  width: 22%;
  min-width: 265px;
  margin: 20px 2%;
  border: 1px solid #d7d7d7;
  border-radius: 5px;
  overflow: hidden;
  box-sizing: border-box;
  padding: 14px 10px 14px 0px;
}
.HW .card ul li .left {
  width: 60px;
  margin: 0 10px;
  display: flex;
  justify-content: center;
  align-items: center;
}
.HW .card ul li .center{
  transform: scale(0.9,0.9);
  zoom: 0.9;
}
.HW .card ul li .center h2 {
  display: inline-block;
  font-size: 14px;
  line-height: 1;
  margin: 0;
  font-weight: 600;
}
.HW .card ul li .center p {
  font-size: 11px;
  line-height: 1;
  margin: 8px 0;
  color: #6b7f92;
}
.HW .card ul li .right {
  flex: 1;
  text-align: right;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  align-items: right;
}
.HW .card ul li .right p {
  font-size: 12px;
  transform: scale(0.9,0.9);
  zoom: 0.9;
  font-weight: 500;
  line-height: 1;
  margin-bottom: 0;
}
.HW .card ul li:nth-child(4n-3) {
  margin-left: 0;
}
.HW .card ul li:nth-child(4n) {
  margin-right: 0;
}

@media screen and (max-width: 1355px) {
  .HW .card ul li {
    width: 30%;
    min-width: 265px;
    margin: 20px 2.5%;
  }
  .HW .card ul li:nth-child(3n-2) {
    margin-left: 0;
  }
  .HW .card ul li:nth-child(3n) {
    margin-right: 0;
  }
  .HW .card ul li:not(:first-child):nth-child(4n-3) {
    margin-left: 2.5%;
  }
  .HW .card ul li:nth-child(4n) {
    margin-right: 2.5%;
  }
}
@media screen and (max-width: 1000px) {
  .HW .card ul li {
    width: 46%;
    margin: 20px 4%;
  }
  .HW .card ul li:nth-child(2n-1) {
    margin-left: 0;
  }
  .HW .card ul li:nth-child(2n) {
    margin-right: 0;
  }
  .HW .card ul li:not(:first-child, :nth-child(2n-1)):nth-child(3n-2) {
    margin-left: 4%;
  }
  .HW .card ul li:not(:nth-child(2n)):nth-child(3n) {
    margin-right: 4%;
  }
  .HW .card ul li:not(:first-child):nth-child(4n-3) {
    margin-left: 0;
  }
  .HW .card ul li:nth-child(4n) {
    margin-right: 0;
  }
}
</style>
