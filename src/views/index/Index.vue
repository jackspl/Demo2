<template>
  <el-container class="box">

    <!-- 主体部分 -->
    <el-container class="main">
      <!-- 左侧导航栏 -->
      <!-- 默认高亮 -->
      <el-aside class="left" width="200px">
        <div class="logo">
          <img src="@/assets/logo2.png" alt />
        </div>
        <el-menu router
        @open="handleOpen"
        @close="handleClose"
        default-active="/users/overview"
        background-color="#2f3b52"
        text-color="#a5aab7"
        active-text-color="#ffd04b">
          <!-- 主题一 -->
          <div class="left-title">客户端监控</div>
          <el-submenu index="2">
            <!-- 配置导航标题 -->
            <template v-slot:title class="sdsd">
              <i class="el-icon-caret-bottom" :class="{ cgcolor: actives2 }"></i>
              <span class="title1">行为分析</span>
            </template>
            <!-- 配置展开内容 -->
            <!-- 总览 -->
            <el-menu-item index="/users/overview" style="padding-left: 60px">
              <span slot="title">总览</span>
            </el-menu-item>
            <!-- 用户KPI分析 -->
            <el-menu-item index="/users/kplAnalysis" style="padding-left: 60px; disabled" >
              <span slot="title">KPI分析</span>
            </el-menu-item>

            <!-- 产品数据分析 -->
            <el-menu-item index="/productDataAnalysis" style="padding-left: 60px; disabled" @click="dashboard5">
              <span slot="title">产品数据分析</span>
            </el-menu-item>

            <!-- 系统优化 -->
            <el-menu-item style="padding-left: 60px">
              <span slot="title">系统优化</span>
            </el-menu-item>

            <!-- 不规范操作 -->
            <el-menu-item style="padding-left: 60px">
              <span slot="title">不规范操作</span>
            </el-menu-item>

            <!-- 信息安全 -->
            <el-menu-item index="/users/informationSecurity" style="padding-left: 60px">
              <span slot="title">信息安全</span>
              <i class="informationSecurityNum"><P>100</P></i>
            </el-menu-item>

            <!-- 显示数据 -->
            <el-menu-item index="showDB" style="padding-left: 60px; display:none">
              <span slot="title">显示数据</span>
            </el-menu-item>
          </el-submenu>
          <el-submenu index="1">
            <!-- 配置导航标题 -->
            <template v-slot:title>
              <i class="el-icon-caret-bottom" :class="{ cgcolor: actives1 }"></i>
              <span class="title1">场景监控</span>
            </template>
            <!-- 配置展开内容 -->
            <!-- 场景频次监控 -->
            <el-menu-item
              index="/users/usersFrequency"
              style="padding-left: 60px"
            >
              <span slot="title">场景频次监控</span>
            </el-menu-item>

            <!-- 场景性能监控 -->
            <el-menu-item
              index="/users/scenarioFrequency"
              style="padding-left: 60px"
            >
              <span slot="title">场景性能监控</span>
            </el-menu-item>

            <!-- 性能趋势监控 -->
            <!-- <el-menu-item index="clientFrequency">
              <span slot="title">性能趋势监控</span>
            </el-menu-item>-->

            <!-- retrieval 操作详情检索 -->
            <el-menu-item index="/users/infoRetr" style="padding-left: 60px">
              <span slot="title">操作详情检索</span>
            </el-menu-item>
          </el-submenu>
          <!-- 主题二 -->
          <div class="left-title-top10">服务器监控</div>
          <el-submenu index="4">
            <!-- 总览 -->
            <template v-slot:title>
              <i
                class="el-icon-caret-bottom"
                :class="{ cgcolor: actives4 }"
              ></i>
              <span class="title1">总览</span>
            </template>
          </el-submenu>
          <el-submenu index="5">
            <!-- 服务 -->
            <template v-slot:title>
              <i
                class="el-icon-caret-bottom"
                :class="{ cgcolor: actives5 }"
              ></i>
              <span class="title1">服务</span>
            </template>
            <!-- 配置展开内容 -->
            <!-- 概况 -->
            <el-menu-item index="/users/survey" style="padding-left: 60px">
              <span slot="title">概况</span>
            </el-menu-item>

            <!-- 趋势分析 -->
            <el-menu-item index="/users/trendAnalysisUnit" style="padding-left: 60px">
              <span slot="title">趋势分析</span>
            </el-menu-item>
            <!-- 详情 -->
            <el-menu-item index="/users/detAnalysisUnit" style="padding-left: 60px">
              <span slot="title">详情</span>
            </el-menu-item>
          </el-submenu>
          <el-submenu index="6">
            <!-- 主机 -->
            <template v-slot:title>
              <i
                class="el-icon-caret-bottom"
                :class="{ cgcolor: actives6 }"
              ></i>
              <span class="title1">主机</span>
            </template>
            <!-- 概况 -->
            <el-menu-item index="/users/hostIndex" style="padding-left: 60px">
              <span slot="title">概况</span>
            </el-menu-item>

            <!-- 趋势分析 -->
            <el-menu-item  index="/users/hostTrend" style="padding-left: 60px">
              <span slot="title">趋势分析</span>
            </el-menu-item>
            <!-- 详情 -->
            <el-menu-item index="/users/hostDet" style="padding-left: 60px">
              <span slot="title">详情</span>
            </el-menu-item>
          </el-submenu>
          <el-submenu index="7">
            <!-- 地图 -->
            <template v-slot:title>
              <i
                class="el-icon-caret-bottom"
                :class="{ cgcolor: actives7 }"
              ></i>
              <span class="title1">管理</span>
            </template>
            <!-- 配置展开内容 -->
            <!-- 用户 -->
            <el-menu-item index="/users/manage" style="padding-left: 60px">
              <span slot="title">用户</span>
            </el-menu-item>
            <!-- 通知 -->
            <el-menu-item style="padding-left: 60px">
              <span slot="title">通知</span>
            </el-menu-item>
             <!-- 系统 -->
            <el-menu-item style="padding-left: 60px">
              <span slot="title">系统</span>
            </el-menu-item>
          </el-submenu>
          <!-- <el-submenu index="8">
            <template v-slot:title>
              <i
                class="el-icon-caret-bottom"
                :class="{ cgcolor: actives8 }"
              ></i>
              <span class="title1">管理</span>
              <i class="eventManagNum"><P>23</P></i>
            </template>
          </el-submenu> -->
          <el-submenu index="9">
            <!-- 事件 -->
            <template v-slot:title>
              <i
                class="el-icon-caret-bottom"
                :class="{ cgcolor: actives9 }"
              ></i>
              <span class="title1">事件</span>
              <i class="monitorNum"><P>2</P></i>
            </template>
            <!-- 配置展开内容 -->
            <!-- 概况 -->
            <el-menu-item index="/users/eventOver" style="padding-left: 60px">
              <span slot="title">概况</span>
            </el-menu-item>
             <!-- 监控事件 -->
            <el-menu-item index="/users/11" style="padding-left: 60px">
              <span slot="title">监控事件</span>
            </el-menu-item>
             <!-- 用户操作事件 -->
            <el-menu-item index="/users/22" style="padding-left: 60px">
              <span slot="title">用户操作事件</span>
            </el-menu-item>
             <!-- 问题处理 -->
            <el-menu-item index="/users/33" style="padding-left: 60px">
              <span slot="title">问题处理</span>
            </el-menu-item>
          </el-submenu>
          <div class="left-title-top10">管理控制台</div>
          <!-- TC连接信息 -->
          <el-menu-item index="/users/connectDB" style="padding-left: 50px" @click="LoginDB">
            <span slot="title">TC连接信息</span>
          </el-menu-item>
          <el-menu-item style="padding-left: 50px">
            <span slot="title">客户端监控设置</span>
          </el-menu-item>
          <el-menu-item style="padding-left: 50px">
            <span slot="title">服务器监控设置</span>
          </el-menu-item>
          <el-menu-item style="padding-left: 50px">
            <span slot="title">运行状态</span>
          </el-menu-item>
          <el-menu-item index="/users/about" style="padding-left: 50px">
            <span slot="title">关于</span>
          </el-menu-item>
          <el-menu-item style="padding-left: 50px" @click="loginOut">
            <span slot="title">退出</span>
          </el-menu-item>
        </el-menu>
      </el-aside>
      <!-- 右侧图表数据 -->
      <el-main class="right">
        <router-view :key="key"></router-view>
      </el-main>
    </el-container>
  </el-container>
</template>

<script>
// queryTable
import { tcDB } from '@/api/table.js'
// import { debounce } from '../js/commit.js'
export default {
  data () {
    return {
      actives1: false,
      actives2: false,
      actives3: false,
      actives4: false,
      actives5: false,
      actives6: false,
      actives7: false,
      actives8: false,
      actives9: false,
      activeIndex: 0,
      rot: 0,
      date: '',
      timer: null,
      zheXianFlag: 1,
      zheXianDate: '',
      // 数据的数据个数
      query: '',
      active: ''
    }
  },
  computed: {
    key () {
      return this.$route.path + Math.random()
    }
  },
  created () {
    // 现在时间，随时刷新
    this.nowTTimes()
    // 初始化带上时间
    this.Data()
  },
  methods: {
    handleOpen (key, keyPath) {
      this.rot = key
      if (this.rot === '1') {
        this.actives1 = !this.actives1
      } else if (this.rot === '2') {
        this.actives2 = !this.actives2
      } else if (this.rot === '3') {
        this.actives3 = !this.actives3
      } else if (this.rot === '4') {
        this.actives4 = !this.actives4
      } else if (this.rot === '5') {
        this.actives5 = !this.actives5
      } else if (this.rot === '6') {
        this.actives6 = !this.actives6
      } else if (this.rot === '7') {
        this.actives7 = !this.actives7
      } else if (this.rot === '8') {
        this.actives8 = !this.actives8
      } else if (this.rot === '9') {
        this.actives9 = !this.actives9
      }
    },
    handleClose (key, keyPath) {
      this.rot = key
      if (this.rot === '1') {
        this.actives1 = !this.actives1
      } else if (this.rot === '2') {
        this.actives2 = !this.actives2
      } else if (this.rot === '3') {
        this.actives3 = !this.actives3
      } else if (this.rot === '4') {
        this.actives4 = !this.actives4
      } else if (this.rot === '5') {
        this.actives5 = !this.actives5
      } else if (this.rot === '6') {
        this.actives6 = !this.actives6
      } else if (this.rot === '7') {
        this.actives7 = !this.actives7
      } else if (this.rot === '8') {
        this.actives8 = !this.actives8
      } else if (this.rot === '9') {
        this.actives9 = !this.actives9
      }
    },
    // 用户提示时间
    Data () {
      this.nowData = new Date()
      const d = this.nowData
      let month =
        d.getMonth() + 1 < 10 ? '0' + (d.getMonth() + 1) : d.getMonth() + 1
      let day = d.getDate() < 10 ? '0' + d.getDate() : d.getDate()
      let times = d.getFullYear() + '-' + month + '-' + day
      this.zheXianDate = times
    },
    // 连接数据库按钮
    async LoginDB () {
      const value = {}
      try {
        const { data } = await tcDB(value)
        const { resultInfo, onlinePeopleCount } = data
        this.resultInfo = resultInfo
        this.query = onlinePeopleCount
        // 传值
        localStorage.setItem('query', JSON.stringify(this.query))
      } catch (e) {
        console.log(e)
      }
    },
    // 退出按钮
    loginOut () {
      this.$confirm('你确定要退出系统吗？', '温馨提示', {
        type: 'warning'
      })
        .then(() => {
          this.$message.success('退出成功')
          localStorage.removeItem('token')
          this.$router.push('/')
        })
        .catch(err => {
          console.log(err)
        })
    },
    dashboard5 () {
    },
    // 当前时间格式化
    timeFormate (timeStamp) {
      let year = new Date(timeStamp).getFullYear()
      let month =
        new Date(timeStamp).getMonth() + 1 < 10
          ? '0' + (new Date(timeStamp).getMonth() + 1)
          : new Date(timeStamp).getMonth() + 1
      let date =
        new Date(timeStamp).getDate() < 10
          ? '0' + new Date(timeStamp).getDate()
          : new Date(timeStamp).getDate()
      let hh =
        new Date(timeStamp).getHours() < 10
          ? '0' + new Date(timeStamp).getHours()
          : new Date(timeStamp).getHours()
      let mm =
        new Date(timeStamp).getMinutes() < 10
          ? '0' + new Date(timeStamp).getMinutes()
          : new Date(timeStamp).getMinutes()
      let ss =
        new Date(timeStamp).getSeconds() < 10
          ? '0' + new Date(timeStamp).getSeconds()
          : new Date(timeStamp).getSeconds()
      // return year + "年" + month + "月" + date +"日"+" "+hh+":"+mm ;
      this.date =
        year +
        '年' +
        month +
        '月' +
        date +
        '日' +
        ' ' +
        hh +
        ':' +
        mm +
        ':' +
        ss
    },
    // 定时器函数
    nowTTimes () {
      this.timeFormate(new Date())
      this.timer = setTimeout(this.nowTTimes, 1 * 1000)
    },
    // 销毁定时器
    beforeDestroy: function () {
      if (this.timer) {
        clearTimeout(this.timer) // 在Vue实例销毁前，清除我们的定时器
      }
    }
  }
}
</script>

<style lang="scss" scoped>
@import "../../css/index/index.css";
</style>
