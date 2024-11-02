// 设置首页走马灯样式
<template>
  <div>
    <h3>设置首页走马灯样式</h3>
    <el-divider />
    <div>
      <span>走马灯类型Type:</span>
      <el-radio-group v-model="carouselType" @change="changeType">
        <el-radio label="">一般模式</el-radio>
        <el-radio label="card">卡片模式</el-radio>
      </el-radio-group>
    </div>
    <div>
      <span>指示器的位置：</span>
      <el-radio-group v-model="carouselIndicator" @change="changePosition">
        <el-radio label="">内部</el-radio>
        <el-radio label="outside">外部</el-radio>
        <el-radio label="none">不显示</el-radio>
      </el-radio-group>
    </div>
  </div>
</template>
<script setup>
import { useStore } from "vuex";
import { ref } from "vue";
const store = useStore();
const carouselType = ref("");
const carouselIndicator = ref("");
const changeType = () => {
  store.commit("changeCarouselType", carouselType.value);
};
const changePosition = () => {
  store.commit("changeIndicatorPosition", carouselIndicator.value);
};
</script>
