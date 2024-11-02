<template>
  <div>
    <div class="inline">
      <el-icon color="blue" size="20">
        <DocumentAdd />
      </el-icon>
      <span>学生信息添加</span>
      <div class="flex-grow"></div>
      <el-badge :value="studentSum" class="item">在库学生数</el-badge>
    </div>
    <fieldset>
      <legend align="left"><h4>采集学生信息</h4></legend>
      <el-form :model="form" label-width="80px" :inline="true">
        <el-form-item label="入学日期">
          <el-date-picker
            v-model="form.date"
            type="date"
            placeholder="选择入学日期"
            :size="size"
          />
        </el-form-item>
        <el-form-item label=" 学生姓名">
          <el-input
            v-model="form.name"
            placeholder="请输入学生姓名"
            required
            clearable
          />
        </el-form-item>
        <el-form-item label=" 专业班级">
          <el-input
            type="text"
            placeholder="请输入专业班级"
            v-model="form.subject"
            required
            clearable
          />
        </el-form-item>
        <el-form-item label="家庭地址">
          <el-input
            type="text"
            placeholder="请输入家庭地址"
            v-model="form.hometown"
            required
            clearable
          />
        </el-form-item>
        <el-form-item label="联系电话">
          <el-input
            type="text"
            placeholder="请输入联系电话"
            v-model="form.php"
            required
            clearable
          />
        </el-form-item>
        <el-button size="small" type="success" @click="addstudent">添加</el-button
        ><br />
      </el-form>
    </fieldset>
    <div>
      <el-table :data="tableData" style="width: 100%" border max-height="250">
        <el-table-column label="入学日期" prop="date" />
        <el-table-column label="学生姓名" prop="name" width="300" />
        <el-table-column label="专业班级" prop="subject" />
        <el-table-column label="家庭地址" prop="hometown" />
        <el-table-column label="联系电话" prop="php" />
      </el-table>
    </div>
  </div>
</template>

<script setup>
import { ref, reactive, computed } from "vue";
import { ElMessage } from "element-plus";
import { DocumentAdd } from "@element-plus/icons-vue";
import { useStore } from "vuex"; // 导入Vuex中useStore
const store = useStore(); //创建仓库
const tableData = computed(() => store.state.students); //获取仓库中state
const studentSum = computed(() => store.state.students.length);
const form = reactive({
  no: "",
  date: "",
  subject: "",
  name: "",
  hometown: "",
  php: "",
});
const bn = ref("");
bn.value = "b-" + (1000000 + store.state.index).toString().substring(1);
//console.log(bn.value);
const size = ref("default");
const addstudent = () => {
  // 当所有输入框均不为空时执行添加
  if (
    form.date != "" &&
    form.name != "" &&
    form.subject != "" &&
    form.hometown != "" &&
    form.php != ""
  ) {
    const onestudent = {
      no: bn.value,
      date: form.date.toLocaleDateString().split("/").join("-"),
      name: form.name,
      subject: form.subject,
      hometown: form.hometown,
      php: form.php,
    };
    store.commit("addOnestudent", onestudent); // 执行添加图书
    store.commit("addIndex"); // 同时index累进1
    ElMessage("学生信息添加成功！");
  } else {
    alert("请先输入学生信息！");
  }
};
</script>
<style scoped>
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