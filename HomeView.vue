<template>
  <div>
    <el-carousel
      :interval="5000"
      arrow="always"
      height="350px"
      :type="type"
      :indicator-position="position"
    >
      <el-carousel-item v-for="num in 4" :key="num">
        <div justify="center">
          <img :src="`${publicPath}banner-${num}.jpg`" />
        </div>
      </el-carousel-item>
    </el-carousel>
  </div>
</template>
<script setup>
import { useStore } from "vuex";
import { ref, computed } from "vue";
const store = useStore();
// 设置公共路径，供静态资源使用
const publicPath = ref(process.env.BASE_URL);
// 从仓库中读取走马灯显示型、指示器的位置
const type = computed(() => store.state.carouselType);
const position = computed(() => store.state.indicatorPosition);
</script>
<style scoped>
.el-carousel__item div {
  color: #6e6f71;
  opacity: 0.75;
  height: 350px;
  margin: 0;
  text-align: center;
}
.el-carousel__item:nth-child(2n) {
  background-color: #99a9bf;
}

.el-carousel__item:nth-child(2n + 1) {
  background-color: #d3dce6;
}
div img {
  width: 100%;
  height: 350px;
}
</style>
