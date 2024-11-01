<template>
  <div>
    <div>
      <div class="inline">
        <el-icon color="green" size="20"> <CircleCheck /></el-icon>
        <span>学生信息查询</span>
        <div class="flex-grow"></div>
        <span>选择学生信息查询方式：</span>
        <el-radio-group v-model="radio">
          <el-radio label="name">学生姓名</el-radio>
          <el-radio label="subject">专业班级</el-radio>
          <el-radio label="hometown">家庭地址</el-radio>
        </el-radio-group>
        <el-input
          v-model="search"
          size="default"
          placeholder="根据方式输入检索信息"
          :prefix-icon="Search"
          clearable
        />
      </div>
      <el-table
        :data="filterTableData"
        style="width: 100%"
        border
        max-height="250"
      >
        <el-table-column label="入学日期" prop="date" />
        <el-table-column label="学生姓名" prop="name" width="300" />
        <el-table-column label="专业班级" prop="subject" />
        <el-table-column label="家庭地址" prop="hometown" />
        <el-table-column label="联系电话" prop="php" />
        <!-- 自定义列模板 -->
        <el-table-column align="right" label="操作">
          <template #default="scope">
            <el-button
              size="small"
              type="primary"
              @click="handleQuery(scope.$index, scope.row)"
              >查看</el-button
            >
          </template>
        </el-table-column>
      </el-table>
    </div>
  </div>
</template>
<script setup>
import { Search, CircleCheck } from "@element-plus/icons-vue";
import { computed, ref } from "vue";
import { ElMessage } from "element-plus";
import { useStore } from "vuex";
const store = useStore();
const radio = ref("name");
const search = ref("");
const filterTableData = computed(() =>
  store.state.students.filter(
    (data) =>
      !search.value ||
      data[radio.value].toLowerCase().includes(search.value.toLowerCase())
  )
);
const handleQuery = (index, row) => {
  ElMessage(
    "序号：" +
      row.no +
      "-" +
      row.name +
      "-" +
      row.subject +
      "-" +
      row.hometown
  );
};
</script>
<style scoped>
.el-input {
  width: 200px;
}
.inline {
  display: flex;
}
.flex-grow {
  flex-grow: 1;
}
</style>
