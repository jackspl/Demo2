<template>
  <!-- 系统 -->
  <div class="manageSystem"></div>
</template>
<script>
export default {
  data() {
    return {};
  },
  created() {},
  methods: {},
  mounted() {}
};
</script>
<style lang="scss" >
@import "../../../../css/manageFile/manageSystem.css";
.manageSystem {
  /* 清除浮动的公共类 */
  .clearfix:before,
  .clearfix:after {
    content: "";
    display: table;
  }
  .clearfix:after {
    clear: both;
  }
  /* 为了兼容IE6,7 */
  .clearfix {
    *zoom: 1;
  }
}
</style>
