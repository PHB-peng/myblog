<template>
  <div class="app-container">
    <!-- 数据表格 -->
    <el-table :data="data" style="width: 100%" border>
      <el-table-column prop="date" label="序号" width="60">
        <template slot-scope="">{{ scope.$index + 1 }}</template>
      </el-table-column>
      <el-table-column prop="title" label="标题" width="150">
        <template slot-scope="">{{ scope.row.title }}</template>
      </el-table-column>
      <el-table-column label="中图预览">
        <template slot-scope="scope">
          <el-image
            style="width: 100px; height: 100px"
            :src="scope.row.midImg2"
            :fit="fill"
          ></el-image>
        </template>
      </el-table-column>
      <el-table-column label="大图预览">
        <template slot-scope="scope">
          <el-image
            style="width: 100px; height: 100px"
            :src="scope.row.bigImg2"
            :fit="fill"
          ></el-image>
        </template>
      </el-table-column>
      <el-table-column label="操作" align="center">
        <template slot-scope="scope">
          <el-button type="primary" icon="el-icon-edit" circle size="mini">
            <el-tooltip
              class="item"
              effect="dark"
              content="编辑"
              placement="top"
              :hide-after="2000"
            >
              <el-button
                type="primary"
                icon="el-icon-edit"
                circle
                size="mini"
                @click="editBannerHandel(scope.row)"
                >编辑</el-button
              >
            </el-tooltip>
          </el-button>
        </template>
      </el-table-column>
    </el-table>
    <!-- 编辑 -->
    <el-dialog title="请编辑信息" :visible.sync="dialogFormVisible">
  <el-form :model="form">
    <el-form-item label="标题" :label-width="formLabelWidth">
      <el-input v-model="form.title" ></el-input>
    </el-form-item>
  <el-form-item label="描述" :label-width="formLabelWidth">
      <el-input v-model="form.description" ></el-input>
    </el-form-item>
  </el-form>
  <div slot="footer" class="dialog-footer">
    <el-button @click="dialogFormVisible = false">取 消</el-button>
    <el-button type="primary" @click="dialogFormVisible = false">确 定</el-button>
  </div>
</el-dialog>
  </div>
</template>

<script>
import { getBanner } from "@/api/banner.js";
import { server_URL } from "@/urlConfig.js";
export default {
  data() {
    return {
      data: [],
      dialogFormVisible: false,//编辑对话框是否显示
      form:{
        id: '',
        midImg: "",
        big: '',
        title: '',
        description:'',
      },
      formLabelWidth: '120px'
    };
  },
  created() {
    this.fetchData();
  },
  methods: {
    fetchData() {
      getBanner().then((res) => {
        console.log(res, "aa");
        this.data = res.data;
        for (let i of this.data) {
          item.midImg2 = server_URL + item.midImg;
          item.bigImg2 = server_URL + item.bigImg;
        }
      });
    },
    editBannerHandel(bannerInfo) {
      // console.log(bannerInfo, "e");
      this.form = {...bannerInfo};
      dialogFormVisible : true;
    },
  },
};
</script>

<style lang="scss" scoped>
</style>