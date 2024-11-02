<template>
  <div>
    <div class="inline">
      <el-icon color="red" size="20"><Delete /></el-icon>
      <span>学生信息删除</span>
      <div class="flex-grow"></div>
      <el-badge :value="studentSum" class="item">在库学生数</el-badge>
    </div>
    <el-table :data="tableData" style="width: 100%" border max-height="250">
      <el-table-column label="入学日期" prop="date" />
      <el-table-column label="学生姓名" prop="name" width="300" />
      <el-table-column label="专业班级" prop="subject" />
      <el-table-column label="家庭地址" prop="hometown" />
      <el-table-column label="联系电话" prop="php" />
      <!-- 自定义列模板 -->
      <el-table-column align="left" label="操作">
        <template #default="scope">
          <el-button
            size="small"
            type="danger"
            @click="handleDelete(scope.$index)"
            >删除</el-button
          >
        </template>
      </el-table-column>
    </el-table>
  </div>
</template>

<script setup>
import { Delete } from "@element-plus/icons-vue";
import { computed } from "vue";
import { useStore } from "vuex";
import { ElMessage, ElMessageBox } from "element-plus";
const store = useStore();
const tableData = computed(() => store.state.students);
const studentSum = computed(() => store.state.students.length);
const handleDelete = (index) => {
  //删除指定的学生信息(index);
  ElMessageBox.confirm("您确定需要删除学生信息。继续吗？", "警告", {
    confirmButtonText: "OK",
    cancelButtonText: "Cancel",
    type: "warning",
  })
    .then(() => {
      //删除仓库中一条学生信息
      store.commit("deleteOnestudent", index);
      //tableData.splice(index, 1);
      ElMessage({
        type: "success",
        message: "删除完成",
      });
    })
    .catch(() => {
      ElMessage({
        type: "info",
        message: "删除取消",
      });
    });
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
.item {
  margin-top: 10px;
  margin-right: 40px;
}
</style>
