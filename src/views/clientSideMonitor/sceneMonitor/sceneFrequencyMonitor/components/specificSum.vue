<template>
  <div class="specificSum">
    <div class="seachSum clearfix">
      <el-form ref="form" :model="form">
        <!-- 搜索条件 -->
        <div class="seachCond">
          <el-form-item label="搜素条件" class="the1">
            <el-select v-model="form.region" placeholder="top20 频次场景">
              <el-option label="top50 频次场景" value="shanghai"></el-option>
              <el-option label="top100 频次场景" value="beijing"></el-option>
            </el-select>
          </el-form-item>
        </div>
        <!-- 图片 -->
        <div class="seachImg">
          <img class="img" src="../../../../../assets/seve.png" />
        </div>
        <!-- 场景名称 -->
        <div class="sceneName">
          <el-form-item label="场景名称" prop="sceneName">
            <el-autocomplete
              v-model="form.sceneName"
              placeholder="所有场景"
              clearable
              type="text"
              :debounce="0"
              :fetch-suggestions="querySearchScen"
              @select="handleSelectScen"
            >
              <!-- <el-tree :data="data" :props="defaultProps" @node-click="handleNodeClick"></el-tree> -->
            </el-autocomplete>
          </el-form-item>
        </div>
        <!-- 搜索按钮 -->
        <div class="seachButton">
          <el-button type="primary" @click="seachBtn">查询</el-button>
          <el-button @click="reset">重置</el-button>
        </div>
        <!-- 结束时间 -->
        <div class="endTime">
          <el-form-item label="结束时间" prop="actionEndTime">
            <el-date-picker
              v-model="form.actionEndTime"
              type="datetime"
              format="yyyy-MM-dd HH:mm:ss"
              value-format="yyyy-MM-dd HH:mm:ss"
              placeholder="选择日期时间"
              clearable
            ></el-date-picker>
          </el-form-item>
        </div>
        <!-- 开始时间 -->
        <div class="startTime">
          <el-form-item label="开始时间" prop="actionBeginTime">
            <el-date-picker
              v-model="form.actionBeginTime"
              type="datetime"
              format="yyyy-MM-dd HH:mm:ss"
              value-format="yyyy-MM-dd HH:mm:ss"
              placeholder="选择日期时间"
              clearable
            ></el-date-picker>
          </el-form-item>
        </div>
      </el-form>
    </div>
    <el-row>
      <el-col :span="4">
        <div id="main111" style="width: 100%; height: 430px"></div>
      </el-col>
      <el-col :span="20">
        <div class="histogramBox">
          <!-- 右侧柱状图渲染展示 -->
          <el-col :lg="24" :xl="24">
            <specificSum
              :categories="categories"
              :MaxTime="MaxTime"
              :userName="userName"
              :htName="htName"
              :scenName="scenName"
              :actTime="actTime"
              :endTime="endTime"
            ></specificSum>
          </el-col>
        </div>
      </el-col>
    </el-row>

    <!-- ------------------------------------------------------------ -->
    <!-- 下载Excel按钮 -->
    <!-- <el-button
      type="primary"
      icon="el-icon-document"
      round
      @click="handleDownload"
      class="excel"
    >Export Excel</el-button>-->

    <!-- 底部表格  -->

    <div class="content">
      <el-row>
        <el-col :span="24">
          <div class="grid-content bg-purple-dark">
            <el-table
              :data="userList"
              @sort-change="sort_change"
              border
              :row-class-name="tableRowClassName"
              :header-cell-style="{
                background: '#365a88',
                color: 'white',
                fontSize: '16px',
                borderRight: '1px solid #344e77'
              }"
              :cell-style="{ background: '#2f5580', color: 'white' }"
            >
              <el-table-column
                type="index"
                label="序号"
                align="center"
                width="100"
                :index="table_index"
              ></el-table-column>
              <el-table-column prop="sceneNameDesc" width="130" align="center" label="场景名"></el-table-column>
              <!-- 带表格排序功能 -->
              <el-table-column
                prop="operationCount"
                align="center"
                sortable="custom"
                label="场景操作次数"
                width="150"
              ></el-table-column>
              <el-table-column align="center" label="次数时间分布">
                <!-- 折现图模板 -->
                <template slot-scope="{ row }">
                  <CellTable :tableDate="row.cellForm"></CellTable>
                </template>
              </el-table-column>
            </el-table>
          </div>
        </el-col>
      </el-row>
    </div>

    <!-- 分页 -->
    <el-pagination
      align="center"
      @size-change="handleSizeChange"
      @current-change="handleCurrentChange"
      :current-page.sync="currentPage"
      :page-sizes="[25, 50, 100]"
      :page-size="pagesSize"
      layout="total, sizes, prev, pager, next"
      :total="total"
    ></el-pagination>
  </div>
</template>

<script>
import { getCountList, getPulldownListScene, getPieData } from "@/api/table.js";
import CellTable from "@/components/CellTable";
import moment from "moment";
export default {
  components: {
    CellTable: CellTable
  },
  data() {
    return {
      data: [
        {
          label: "一级 1",
          children: [
            {
              label: "二级 1-1",
              children: [
                {
                  label: "三级 1-1-1"
                }
              ]
            }
          ]
        }
      ],
      defaultProps: {
        children: "children",
        label: "label"
      },
      isShowCellTable: true,

      // 现在开始时间
      times: "",
      // 获取当前的时间往前推一个月
      Dtimes: "",
      flag: false,
      form: {
        region: "",

        sceneName: "", // 英文的场景名
        sceneNameDesc: "", // 选中的场景名
        actionBeginTime: "", // 开始时间
        actionEndTime: "" // 结束时间
      },
      // 模拟登录用户数量
      zheXianFlag: 2,
      zheXianDates: "2019-12-23",
      // Echarts图表数据
      categories: [],
      MaxTime: [],
      userName: "",
      htName: "",
      scenName: "",
      actTime: "",
      endTime: "",

      // 场景名模糊下拉菜单
      sceneName: "",

      // 表格数据
      userList: [],
      value: "",
      // 分页默认第一页高亮
      currentPage: 1,
      pagesNum: 1, // 当前页
      pagesSize: 25, // 每页条数
      total: 5, // 总页数

      // 下载表格表名+当前日期
      filename: "操作频次监控" + moment().format("YYYY年MM月DD日")
    };
  },
  created() {
    // 初始化带上时间
    this.Data();
    this.getSumTimes();
    this.getUserList();
  },
  methods: {
    async getUserList(valuee) {
      // 传默认时间到后台
      const value = {
        pagesNum: this.pagesNum,
        pagesSize: this.pagesSize,
        actionBeginTime: this.form.actionBeginTime,
        actionEndTime: this.form.actionEndTime,
        sceneName: this.form.sceneName,
        sceneNameDesc: this.form.sceneNameDesc,
        ...valuee
      };
      try {
        const { data } = await getCountList(value);
        const { tableList,normalCounts,seriousCounts } = data;
        if (tableList === null) {
          this.userList = "";
          this.total = "0";
        } else {
          this.userList = tableList;
          console.log('数据',tableList)
          this.total = data.tableTotalList[0];
          this.initItem(normalCounts,seriousCounts)
          this.userList.forEach((item, index) => {
            console.log(item.pZheXianY)
            item.cellForm = {
              class: `min${index}`,
              CrosXTimes: item.pZheXianX,
              series: [
                {
                  name: "总计查看",
                  type: "line",
                  symbol: "none", // 取消折点圆圈
                  data: item.pZheXianY,
                  areaStyle: {
                    normal: {
                      // 颜色渐变函数 前四个参数分别表示四个位置依次为左、下、右、上
                      color: new this.$echarts.graphic.LinearGradient(
                        0,
                        0,
                        0,
                        1,
                        [
                          {
                            offset: 0,
                            color: "rgba(248,225,131,0.39)"
                          },
                          {
                            offset: 0.34,
                            color: "rgba(227,212,150,0.25)"
                          },
                          {
                            offset: 1,
                            color: "rgba(201,193,163,0.00)"
                          }
                        ]
                      )
                    }
                  },
                  itemStyle: {
                    normal: {
                      color: "#ddaf84", // 改变折线点的颜色
                      lineStyle: {
                        color: "#ddaf84" // 改变折线颜色
                      }
                    }
                  }
                }
              ]
            };
          });
        }
        this.sceneNameDesc = tableList.sceneNameDesc;
        this.sceneList = data.sceneList;
        // 传向图表标题的数据
        this.userName = this.form.userId;
        this.htName = this.form.hostName;
        this.scenName = this.form.sceneName;
        this.actTime = moment(this.form.actionBeginTime).format(
          "YYYY-MM-DD HH:mm:ss"
        );
        this.endTime = moment(this.form.actionEndTime).format(
          "YYYY-MM-DD HH:mm:ss"
        );

        // X轴的场景名称
        this.categories = tableList.map(item => {
          return item.sceneNameDesc;
        });
        this.MaxTime = tableList.map(item => {
          return item.operationCount;
        });
        // 获取默认form开始、结束时间和图表开始结束时间
        this.endTime = this.times;
        this.actTime = this.Dtimes;
        // 右侧柱状图渲染展示
      } catch (e) {
        console.log(e);
      }
    },

    handleNodeClick(data) {
      console.log(data);
    },
    // 饼图函数（模拟接口）
    initItem(normalCounts,seriousCounts) {
      let myChart111 = this.$echarts.init(document.getElementById("main111"));
      const option111 = {
        // color: ["#98c831", "#f4a014", "#eb1460"],
        color: ["#98c831", "#eb1460"],
        animation: false,
        tooltip: {
          trigger: "item",
          formatter: "{a} {b} :{d}%",
          textStyle: {
            fontSize: 14
          }
        },
        legend: {
          // data: ["正常", "警告", "严重"],
          data: ["正常", "严重"],
          itemWidth: 16, // 设置宽度
          itemHeight: 10, // 设置高度
          itemGap: 20, // 设置间距
          bottom: "30%",
          left: "12%",
          orient: "horizontal",
          textStyle: {
            // 图例文字的样式
            color: "#73d6db",
            fontSize: 16
          }
        },
        toolbox: {
          show: true,
          orient: "vertical",
          left: "right",
          top: "center"
        },
        yAxis: [{ gridIndex: 0, name: "年级", show: false }],
        series: [
          {
            name: "",
            type: "pie",
            hoverAnimation: false,

            radius: "82%",
            center: ["50%", "31%"],
            data: [
              { value: normalCounts, name: "正常" },
              { value: seriousCounts, name: "严重" }
              // { value: 45, name: "警告" },
            ],
            label: {
              normal: {
                position: "inner",
                formatter: "{c}" + '({d}%)',
                offset: [100],
                textStyle: {
                  color: "#ffffff",
                  fontSize: 14
                }
              }
            }
          }
        ]
      };
      myChart111.setOption(option111);
    },
    // 表格排序功能
    sortFun: function(attr, rev) {
      // 第一个参数传入info里的prop表示排的是哪一列，第二个参数是升还是降排序
      if (rev === undefined) {
        rev = 1;
      } else {
        rev = rev ? 1 : -1;
      }

      return function(a, b) {
        a = a[attr];
        b = b[attr];
        if (a < b) {
          return rev * -1;
        }
        if (a > b) {
          return rev * 1;
        }
        return 0;
      };
    },
    // 前端排序
    sort_change(column) {
      // column是个形参，就是前面说的info，你叫什么都可以
      this.pagesNum = 1; // return to the first page after sorting
      this.currentPage = 1;
      if (column.prop === "operationCount") {
        this.userList = this.userList.sort(
          this.sortFun(column.prop, column.order === "ascending")
        );
      } else if (column.prop === "status") {
        this.userList = this.userList.sort(
          this.sortFun(column.prop, column.order === "ascending")
        );
      } else if (column.prop === "priority") {
        this.userList = this.userList.sort(
          this.sortFun(column.prop, column.order === "ascending")
        );
      }
    },
    // 用户提示时间
    Data() {
      this.nowData = new Date();
      const d = this.nowData;
      let month =
        d.getMonth() + 1 < 10 ? "0" + (d.getMonth() + 1) : d.getMonth() + 1;
      let day = d.getDate() < 10 ? "0" + d.getDate() : d.getDate();
      let times = d.getFullYear() + "-" + month + "-" + day;
      this.zheXianDate = times;
      this.zheXianDates = times;
      this.zheXianDateDown = times;
    },
    // 表格分页序号
    table_index(index) {
      return (this.pagesNum - 1) * this.pagesSize + index + 1;
    },
    getSumTimes() {
      // 获取当前的时间， 变量名为tiems
      this.nowData = new Date();
      const d = this.nowData;
      let month =
        d.getMonth() + 1 < 10 ? "0" + (d.getMonth() + 1) : d.getMonth() + 1;
      let day = d.getDate() < 10 ? "0" + d.getDate() : d.getDate();
      let hours = d.getHours() < 10 ? "0" + d.getHours() : d.getHours();
      let min = d.getMinutes() < 10 ? "0" + d.getMinutes() : d.getMinutes();
      let sec = d.getSeconds() < 10 ? "0" + d.getSeconds() : d.getSeconds();
      let times =
        d.getFullYear() +
        "-" +
        month +
        "-" +
        day +
        " " +
        hours +
        ":" +
        min +
        ":" +
        sec;
      this.times = times;

      // 获取当前的时间往前推一个月， 变量名为Dtimes
      let dTimes = new Date(new Date(this.nowData).getTime() - 86400000 * 30);
      let Dmonth =
        dTimes.getMonth() + 1 < 10
          ? "0" + (dTimes.getMonth() + 1)
          : dTimes.getMonth() + 1;
      let Dday =
        dTimes.getDate() < 10 ? "0" + dTimes.getDate() : dTimes.getDate();
      let Dhours =
        dTimes.getHours() < 10 ? "0" + dTimes.getHours() : dTimes.getHours();
      let Dmin =
        dTimes.getMinutes() < 10
          ? "0" + dTimes.getMinutes()
          : dTimes.getMinutes();
      let Dsec =
        dTimes.getSeconds() < 10
          ? "0" + dTimes.getSeconds()
          : dTimes.getSeconds();
      let Dtimes =
        dTimes.getFullYear() +
        "-" +
        Dmonth +
        "-" +
        Dday +
        " " +
        Dhours +
        ":" +
        Dmin +
        ":" +
        Dsec;
      this.Dtimes = Dtimes;
      this.form.actionEndTime = this.times;
      this.form.actionBeginTime = this.Dtimes;
    },
    // Excel表格数据
    handleDownload() {
      this.downloadLoading = true;
      // 引包
      import("@/utils/Export2Excel")
        .then(excel => {
          // 第一行标题
          const tHeader = ["场景名", "场景操作次数"];
          // 第一行标题对应的字段
          const filterVal = ["sceneNameDesc", "operationCount"];
          // 表格对应的接口表格集合
          const list = this.userList;

          // 数据过滤
          const data = this.formatJson(filterVal, list);
          excel.export_json_to_excel({
            header: tHeader, // 表头 必填
            data, // 具体数据 必填
            filename: this.filename, // 非必填
            autoWidth: this.autoWidth, // 非必填
            bookType: this.bookType // 非必填 'xlsx'
          });
          this.downloadLoading = false;
        })
        .catch(() => {
          this.downloadLoading = false;
        });
    },
    formatJson(filterVal, jsonData) {
      // 处理对应列名下的数据格式的，例如时间Date
      return jsonData.map(v =>
        filterVal.map(j => {
          if (j === "Data") {
            var date = new Date(v[j]);
            return date, "yyyy-MM-dd HH:mm:ss";
          } else {
            return v[j];
          }
        })
      );
    },
    // 隔行变色
    tableRowClassName({ row, rowIndex }) {
      if (rowIndex % 2 === 0) {
        return "warning-row";
      } else {
        return "";
      }
    },

    // 分页功能
    // 更改每页个数
    handleSizeChange(val) {
      this.pagesSize = val;
      this.pagesNum = 1;
      this.currentPage = 1;
      this.getUserList();
    },
    // 切换页
    handleCurrentChange(val) {
      this.pagesNum = val;
      this.getUserList();
    },
    // 立即查询
    async seachBtn() {
      const ttime1 = this.form.actionBeginTime;
      const ttime2 = this.form.actionEndTime;
      const timeStr1 = new Date(ttime1).getTime();
      const timeStr2 = new Date(ttime2).getTime();
      if (timeStr1 > timeStr2) {
        this.$message.error("请合理选择时间");
        return;
      }
      this.pagesNum = 1;
      await this.$refs.form.validate(isValid => {
        if (isValid) {
          this.getUserList(this.form);
        } else {
        }
      });
      if (this.form.sceneNameDesc === "") {
        this.categories = "";
        this.MaxTime = 0;
        this.MinTime = 0;
        this.AvgTime = 0;
      }
    },
    // 点击重置按钮
    reset() {
      this.form.sceneName = "";
      this.form.actionBeginTime = "";
      this.form.actionEndTime = "";
      this.getSumTimes();
    },
    // 第一个参数， 用户输入的值  第二个值回调函数
    querySearchScen(queryString, callback) {
      // 从后台获取到对象数组
      getPulldownListScene({
        sceneName: queryString
      }).then(res => {
        let list = [];
        if (res.data.fuzzySceneList === null) {
          list = [];
        } else {
          res.data.fuzzySceneList.forEach(item => {
            list.push({
              value: item
            });
          });
        }
        callback(list);
      });
    },
    handleSelectScen(item) {}
  },
  mounted() {
    const that = this;
    document.onkeydown = function(e) {
      if (window.event.keyCode === 13) {
        that.seachBtn();
      }
    };
  },
  updated() {}
};
</script>

<style lang="scss" scoped>
@import "../../../../../css/base/base.css";
@import "../../../../../css/clientSideMonitor/sceneMonitor/sceneFrequencyMonitor/specificSum.css";

.price-bar {
  color: red !important;
}
.tiger-trend-charts {
  height: 60px;
  min-width: 100px;
}
</style>
