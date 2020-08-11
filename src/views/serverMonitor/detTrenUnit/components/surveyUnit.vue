<template>
  <!-- 概况 -->
  <div class="surveyUnit">
    <div class="topBox clearfix">
    <!-- 左侧服务概况 -->
    <div class="boxLeft">
      <div class="leftPei">
        <div id="topPei">
          <div id="allServer"></div>
        </div>
        <div id="bottomPei">
          <div id="allHost"></div>
        </div>
      </div>
      <div class="rightTab">
        <div class="topTab">
          <div class="m10">服务概况</div>
          <el-table :data="tableData" border>
            <el-table-column prop="1" label="全部"></el-table-column>
            <el-table-column prop="2" label="正常"></el-table-column>
            <el-table-column prop="3" label="警告"></el-table-column>
            <el-table-column prop="4" label="未知"></el-table-column>
            <el-table-column prop="5" label="紧急"></el-table-column>
            <el-table-column prop="6" label="问题"></el-table-column>
            <el-table-column prop="7" label="待定"></el-table-column>
            <el-table-column prop="8" label="未处理"></el-table-column>
          </el-table>
        </div>
        <div class="bottomTab">
          <div class="m10">问题来源主机排名</div>
          <el-table :data="hostTable" border height="200px">
            <el-table-column prop="1" label="主机" width="135px"></el-table-column>
            <el-table-column prop="2" label="全部" width="64px"></el-table-column>
            <el-table-column prop="3" label="正常" width="64px"></el-table-column>
            <el-table-column prop="4" label="警告" width="64px"></el-table-column>
            <el-table-column prop="5" label="未知" width="64px"></el-table-column>
            <el-table-column prop="6" label="紧急" width="64px"></el-table-column>
            <el-table-column prop="7" label="待定" width="64px"></el-table-column>
            <el-table-column prop="8" label="问题" width="64px"></el-table-column>
            <el-table-column prop="9" label="未处理" width="80px"></el-table-column>
          </el-table>
        </div>
      </div>
    </div>
    <!-- 右侧指标概况 -->
    <div class="boxRight">
      <div class="leftPei">
        <div id="topPei">
          <div id="allIndex"></div>
        </div>
        <div id="bottomPei">
          <div id="allHostIndex"></div>
        </div>
      </div>
      <div class="rightTab">
        <div class="topTab">
          <div class="m10">服务概况</div>
          <el-table :data="tableData" border>
            <el-table-column prop="1" label="全部"></el-table-column>
            <el-table-column prop="2" label="正常"></el-table-column>
            <el-table-column prop="3" label="警告"></el-table-column>
            <el-table-column prop="4" label="未知"></el-table-column>
            <el-table-column prop="5" label="紧急"></el-table-column>
            <el-table-column prop="6" label="问题"></el-table-column>
            <el-table-column prop="7" label="待定"></el-table-column>
            <el-table-column prop="8" label="未处理"></el-table-column>
          </el-table>
        </div>
        <div class="bottomTab">
          <div class="m10">问题来源主机排名</div>
          <el-table :data="hostTable" border height="200px">
            <el-table-column prop="1" label="主机" width="135px"></el-table-column>
            <el-table-column prop="2" label="全部" width="64px"></el-table-column>
            <el-table-column prop="3" label="正常" width="64px"></el-table-column>
            <el-table-column prop="4" label="警告" width="64px"></el-table-column>
            <el-table-column prop="5" label="未知" width="64px"></el-table-column>
            <el-table-column prop="6" label="紧急" width="64px"></el-table-column>
            <el-table-column prop="7" label="待定" width="64px"></el-table-column>
            <el-table-column prop="8" label="问题" width="64px"></el-table-column>
            <el-table-column prop="9" label="未处理" width="80px"></el-table-column>
          </el-table>
        </div>
      </div>
    </div>
    </div>
    <!-- 动态表格 -->
    <div class="botBox">
      <el-table
        v-if="this.spanMethod.length"
        ref="table"
        :data="testTableArr"
        :span-method="arraySpanMethod"
        class="ele-table table-info-area"
        border
        stripe
        height="530px"
        style="background-color: #02356f;"
      >
        <el-table-column
          :prop="item"
          :label="tableTitle[item].name+info[tableTitle[item].type]"
          align="center"
          v-for="(item,index) in tableTitleKey"
          :key="index"
          style=""
          :render-header="labelHead"
        >

        </el-table-column>
      </el-table>
    </div>
  </div>
</template>
<script>
import {
  // 12、公司KPI贡献接口
  comloyeKpiPie
} from "@/api/table.js";
import { tableData, tableTitle } from "./mock";
export default {
  data() {
    return {
      tableData: [
        {
          1: "5976",
          2: "4283",
          3: "1186",
          4: "63",
          5: "95",
          6: "36",
          7: "35",
          8: "78"
        },
        {
          1: "100%",
          2: "24.9%",
          3: "1.4%",
          4: "2.5%",
          5: "0.7%",
          6: "0.9%",
          7: "2.9%",
          8: "78%"
        }
      ],
      hostTable: [
        {
          1: "TC_server1",
          2: "760",
          3: "760",
          4: "760",
          5: "760",
          6: "760",
          7: "760",
          8: "760",
          9: "760"
        },
        {
          1: "TC_server1",
          2: "760",
          3: "760",
          4: "760",
          5: "760",
          6: "760",
          7: "760",
          8: "760",
          9: "760"
        },
        {
          1: "TC_server1",
          2: "760",
          3: "760",
          4: "760",
          5: "760",
          6: "760",
          7: "760",
          8: "760",
          9: "760"
        },
        {
          1: "TC_server1",
          2: "760",
          3: "760",
          4: "760",
          5: "760",
          6: "760",
          7: "760",
          8: "760",
          9: "760"
        },
        {
          1: "TC_server1",
          2: "760",
          3: "760",
          4: "760",
          5: "760",
          6: "760",
          7: "760",
          8: "760",
          9: "760"
        },
        {
          1: "TC_server1",
          2: "760",
          3: "760",
          4: "760",
          5: "760",
          6: "760",
          7: "760",
          8: "760",
          9: "760"
        },
        {
          1: "TC_server1",
          2: "760",
          3: "760",
          4: "760",
          5: "760",
          6: "760",
          7: "760",
          8: "760",
          9: "760"
        },
        {
          1: "TC_server1",
          2: "760",
          3: "760",
          4: "760",
          5: "760",
          6: "760",
          7: "760",
          8: "760",
          9: "760"
        },
        {
          1: "TC_server1",
          2: "760",
          3: "760",
          4: "760",
          5: "760",
          6: "760",
          7: "760",
          8: "760",
          9: "760"
        }
      ],
      // -----------------------------
      // 动态表格数据
      info: {
        string: "",
        avg: "(平均值)",
        sum: "(总数)"
      },
      testTableArr: [], // table数据
      spanKey: [], // 需要合并的列,每个元素为表格的prop值（键值）
      tableTitle: {}, // table表头显示
      tableTitleKey: [], // 所有的列的prop值（键值）
      spanMethod: [], // 表格向下合并的方式
      divArr: [], // 分片数据，用于将数据分片，保证不会
      divIndex: [0] // 用于记录分片的位置
    };
  },
  created() {
    // 全部服务饼图
    this.getAllServer();

    // 全部服务饼图
    this.getAllHost();

    // 全部指标饼图
    this.getAllIndex();
    // 全部服务指标饼图
    this.getAllHostIndex();
  },
  methods: {
    labelHead: function(h, { column, $index }) {
      let l = column.label.length;
      let f = 16;
      column.minWidth = f * (l + 2); //加上一个文字长度
      return h("div", { class: "table-head", style: { width: "100%" } }, [
        column.label
      ]);
    },
    // 提取全部服务公共饼图函数
    async getAllServer(index = 1) {
      const value = {
        actionBeginTime: "2020-06-21 10:10:34",
        actionEndTime: "2020-07-21 10:10:34",
        kpiContributionFlag: 1
      };
      const { data } = await comloyeKpiPie(value);
      const { contributionList, allKPI } = data;
      const newArr = contributionList.map((item, index) => {
        const comRandColor = this.randColor(item, index);
        return {
          value: item.KPI,
          name:
            item.company +
            "(" +
            ((item.KPI / allKPI) * 100).toFixed(1) +
            "%" +
            ")",
          radius: [0, "50%"],
          hoverAnimation: false,
          itemStyle: {
            normal: {
              color: comRandColor
            }
          }
        };
      });
      this.serverPei(newArr, allKPI);
    },
    // 全部服务饼图函数
    serverPei(arr, allKPI) {
      let myChart1 = this.$echarts.init(document.getElementById("allServer"));
      this.initHeight1 = document.getElementById("topPei").offsetHeight;
      this.initWidth1 = document.getElementById("topPei").offsetWidth;
      const option1 = {
        animation: false,
        title: {
          text: "全部服务",
          subtext: allKPI,
          x: "center",
          y: "40%",
          textStyle: {
            fontWeight: "normal",
            fontSize: 14,
            color: "white"
          },
          subtextStyle: {
            fontSize: 14,
            color: "white"
          }
        },
        // 鼠标放上去有提示
        tooltip: {
          show: true,
          trigger: "item",
          formatter: "{b}：{c}"
          // formatter: '{b}：{c}个<br/>占比：({d}%)'
        },
        series: [
          {
            type: "pie",
            stillShowZeroSum: true,
            //     外圈大小  内圈大小
            radius: ["80%", "50%"],
            //     左右居中  上下居中
            center: ["50%", "50%"],
            // 饼图轮廓阴影
            itemStyle: {
              normal: {
                shadowBlur: 30,
                shadowColor: "rgba(255,227,42,0.3)",
                shadowOffsetX: -5,
                shadowOffsetY: 5
              }
            },
            label: {
              normal: {
                position: "inner",
                show: false,
                textStyle: {
                  color: "#fff",
                  fontSize: 12
                }
              }
            },
            labelLine: {
              normal: {
                show: false
              }
            },
            data: arr
          }
        ]
      };
      myChart1.setOption(option1);
      let resize1 = {
        height: this.initHeight1,
        width: this.initWidth1
      };
      myChart1.resize(resize1);
    },
    // ----------------------------------
    // 提取全部主机公共饼图函数
    async getAllHost(index = 1) {
      const value = {
        actionBeginTime: "2020-06-21 10:10:34",
        actionEndTime: "2020-07-21 10:10:34",
        kpiContributionFlag: 1
      };
      const { data } = await comloyeKpiPie(value);
      const { contributionList, allKPI } = data;
      const newArr = contributionList.map((item, index) => {
        const comRandColor = this.randColor(item, index);
        return {
          value: item.KPI,
          name:
            item.company +
            "(" +
            ((item.KPI / allKPI) * 100).toFixed(1) +
            "%" +
            ")",
          radius: [0, "50%"],
          hoverAnimation: false,
          itemStyle: {
            normal: {
              color: comRandColor
            }
          }
        };
      });
      this.hostPei(newArr, allKPI);
    },
    // 全部主机饼图函数
    hostPei(arr, allKPI) {
      let myChart2 = this.$echarts.init(document.getElementById("allHost"));
      this.initHeight2 = document.getElementById("bottomPei").offsetHeight;
      this.initWidth2 = document.getElementById("bottomPei").offsetWidth;
      const option2 = {
        animation: false,
        title: {
          text: "全部主机",
          subtext: allKPI,
          x: "center",
          y: "50%",
          textStyle: {
            fontWeight: "normal",
            fontSize: 14,
            color: "white"
          },
          subtextStyle: {
            fontSize: 14,
            color: "white"
          }
        },
        // 鼠标放上去有提示
        tooltip: {
          show: true,
          trigger: "item",
          formatter: "{b}：{c}"
          // formatter: '{b}：{c}个<br/>占比：({d}%)'
        },
        series: [
          {
            type: "pie",
            stillShowZeroSum: true,
            //     外圈大小  内圈大小
            radius: ["90%", "50%"],
            //     左右居中  上下居中
            center: ["50%", "60%"],
            // 饼图轮廓阴影
            itemStyle: {
              normal: {
                shadowBlur: 30,
                shadowColor: "rgba(255,227,42,0.3)",
                shadowOffsetX: -5,
                shadowOffsetY: 5
              }
            },
            label: {
              normal: {
                position: "inner",
                show: false,
                textStyle: {
                  color: "#fff",
                  fontSize: 12
                }
              }
            },
            labelLine: {
              normal: {
                show: false
              }
            },
            data: arr
          }
        ]
      };
      myChart2.setOption(option2);
      let resize2 = {
        height: this.initHeight2,
        width: this.initWidth2
      };
      myChart2.resize(resize2);
    },
    // --------------------------------------
    // 提取全部指标公共饼图函数
    async getAllIndex(index = 1) {
      const value = {
        actionBeginTime: "2020-06-21 10:10:34",
        actionEndTime: "2020-07-21 10:10:34",
        kpiContributionFlag: 1
      };
      const { data } = await comloyeKpiPie(value);
      const { contributionList, allKPI } = data;
      const newArr = contributionList.map((item, index) => {
        const comRandColor = this.randColor(item, index);
        return {
          value: item.KPI,
          name:
            item.company +
            "(" +
            ((item.KPI / allKPI) * 100).toFixed(1) +
            "%" +
            ")",
          radius: [0, "50%"],
          hoverAnimation: false,
          itemStyle: {
            normal: {
              color: comRandColor
            }
          }
        };
      });
      this.indexPei(newArr, allKPI);
    },
    // 全部指标饼图函数
    indexPei(arr, allKPI) {
      let myChart3 = this.$echarts.init(document.getElementById("allIndex"));
      this.initHeight3 = document.getElementById("topPei").offsetHeight;
      this.initWidth3 = document.getElementById("topPei").offsetWidth;
      const option3 = {
        animation: false,
        title: {
          text: "全部指标",
          subtext: allKPI,
          x: "center",
          y: "40%",
          textStyle: {
            fontWeight: "normal",
            fontSize: 14,
            color: "white"
          },
          subtextStyle: {
            fontSize: 14,
            color: "white"
          }
        },
        // 鼠标放上去有提示
        tooltip: {
          show: true,
          trigger: "item",
          formatter: "{b}：{c}"
          // formatter: '{b}：{c}个<br/>占比：({d}%)'
        },
        series: [
          {
            type: "pie",
            stillShowZeroSum: true,
            //     外圈大小  内圈大小
            radius: ["80%", "50%"],
            //     左右居中  上下居中
            center: ["50%", "50%"],
            // 饼图轮廓阴影
            itemStyle: {
              normal: {
                shadowBlur: 30,
                shadowColor: "rgba(255,227,42,0.3)",
                shadowOffsetX: -5,
                shadowOffsetY: 5
              }
            },
            label: {
              normal: {
                position: "inner",
                show: false,
                textStyle: {
                  color: "#fff",
                  fontSize: 12
                }
              }
            },
            labelLine: {
              normal: {
                show: false
              }
            },
            data: arr
          }
        ]
      };
      myChart3.setOption(option3);
      let resize3 = {
        height: this.initHeight3,
        width: this.initWidth3
      };
      myChart3.resize(resize3);
    },
    // --------------------------------------
    // 提取全部主机指标公共饼图函数
    async getAllHostIndex(index = 1) {
      const value = {
        actionBeginTime: "2020-06-21 10:10:34",
        actionEndTime: "2020-07-21 10:10:34",
        kpiContributionFlag: 1
      };
      const { data } = await comloyeKpiPie(value);
      const { contributionList, allKPI } = data;
      const newArr = contributionList.map((item, index) => {
        const comRandColor = this.randColor(item, index);
        return {
          value: item.KPI,
          name:
            item.company +
            "(" +
            ((item.KPI / allKPI) * 100).toFixed(1) +
            "%" +
            ")",
          radius: [0, "50%"],
          hoverAnimation: false,
          itemStyle: {
            normal: {
              color: comRandColor
            }
          }
        };
      });
      this.hostIndexPei(newArr, allKPI);
    },
    // 全部主机指标饼图函数
    hostIndexPei(arr, allKPI) {
      let myChart4 = this.$echarts.init(
        document.getElementById("allHostIndex")
      );
      this.initHeight4 = document.getElementById("bottomPei").offsetHeight;
      this.initWidth4 = document.getElementById("bottomPei").offsetWidth;
      const option4 = {
        animation: false,
        title: {
          text: "全部主机",
          subtext: allKPI,
          x: "center",
          y: "50%",
          textStyle: {
            fontWeight: "normal",
            fontSize: 14,
            color: "white"
          },
          subtextStyle: {
            fontSize: 14,
            color: "white"
          }
        },
        // 鼠标放上去有提示
        tooltip: {
          show: true,
          trigger: "item",
          formatter: "{b}：{c}"
          // formatter: '{b}：{c}个<br/>占比：({d}%)'
        },
        series: [
          {
            type: "pie",
            stillShowZeroSum: true,
            //     外圈大小  内圈大小
            radius: ["90%", "50%"],
            //     左右居中  上下居中
            center: ["50%", "60%"],
            // 饼图轮廓阴影
            itemStyle: {
              normal: {
                shadowBlur: 30,
                shadowColor: "rgba(255,227,42,0.3)",
                shadowOffsetX: -5,
                shadowOffsetY: 5
              }
            },
            label: {
              normal: {
                position: "inner",
                show: false,
                textStyle: {
                  color: "#fff",
                  fontSize: 12
                }
              }
            },
            labelLine: {
              normal: {
                show: false
              }
            },
            data: arr
          }
        ]
      };
      myChart4.setOption(option4);
      let resize4 = {
        height: this.initHeight4,
        width: this.initWidth4
      };
      myChart4.resize(resize4);
    },
    // 随机颜色
    randColor(item, index) {
      // const Arr = ['red', 'black', 'yellow', 'blue', '#FD70B8',
      // '#CBEAED', '#8EEBAC', '#6139E5', '#F38946', '#7BA5F4', '#3CFA89'
      // , '#4FEE1F', '#CB59F6', '#FDB10F', '#EBD50C', '#F0D54E']
      const Arr = [
        "#CBEAED",
        "#8EEBAC",
        "#6139E5",
        "#F38946",
        "#7BA5F4",
        "#3CFA89",
        "#4FEE1F",
        "#CB59F6",
        "#6139E5",
        "#F38946",
        "yellow",
        "blue",
        "red",
        "black",
        "yellow",
        "blue",
        "red",
        "black",
        "yellow",
        "blue",
        "red",
        "black",
        "yellow",
        "blue",
        "red",
        "black",
        "yellow",
        "blue"
      ];
      // const color = Math.floor(Math.random() * Arr.length + 1)-1;
      const color = Arr[index];
      return color;
    },
    // -----------------------------
    // 动态表格数据
    getInit() {
      setTimeout(() => {
        // mock异步
        let response = tableData;
        // const ccText = response.value
        // console.log(ccText)
        // for (var i = 0; i < ccText.length; i++) {
        //   for (var j = 0; j < i + 1; j++) {
        //     console.log(i[j]);
        //   }
        // }
        // for(var i = 0; i < response.value.length; i++) {

        // }
        // const ccText = response.value[0]
        // for(var i = 0; i < ccText.length; i++) {
        //   console.log( ccText[i])
        //   if(ccText[i] === '紧急') {
        //     console.log('紧急情况')
        //   }
        // }
        this.testTableArr = this.initTableData({
          key: response.key,
          value: response.value
        });
        this.normalizeData(this.testTableArr, this.spanKey);
      }, 200);
    },
    /**
     * 将response{key:[],value:[]}  转换成可用于表格的数据
     * @param response
     * @returns {Promise}
     */
    initTableData(response) {
      let initArr = [];
      for (const indexValue in response.value) {
        let initObj = {};
        for (const indexKey in response.key) {
          initObj[response.key[indexKey]] =
            response.value[indexValue][indexKey];
        }
        initArr.push(initObj);
      }
      return initArr;
    },
    /**
     * 合并表格
     */
    arraySpanMethod({ rowIndex, columnIndex }) {
      if (this.spanKey.length) {
        for (let keyIndex = 0; keyIndex < this.spanKey.length; keyIndex++) {

          // 找到指定需要合并的列，应用合并规则
          if (this.spanKey[keyIndex] === this.tableTitleKey[columnIndex]) {
            const _row = this.spanMethod[keyIndex][rowIndex];
            const _col = _row > 0 ? 1 : 0;

            return {
              rowspan: _row,
              colspan: _col
            };
          }
        }
      } else {
        return {
          rowspan: 1,
          colspan: 1
        };
      }
    },
    /**
     * data为传入的表格数据，结构为[{},{}]
     * spanKey为需要合并操作的列  结构为[]
     */
    normalizeData(data, spanKey) {
      this.spanMethod = [];
      this.divIndex = [0];
      // 有需要合并的字段才做处理
      if (spanKey.length) {
        for (let keyIndex = 0; keyIndex < spanKey.length; keyIndex++) {
          const key = spanKey[keyIndex];

          this.sliceData();
          this.spanMethod.push(this.spanKeyMenthod(key));
        }
      }
    },

    /**
     * key 为指定列的键值
     * contactArr 指定的列下 行的合并方式   []
     * contactDot 单元格合并展示位
     */
    spanKeyMenthod(key) {
      let divContactArr = []; // 记录当前列的向下合并方式
      // 计算每一片单独的行扩展方式
      let divIndexTemp = [...this.divIndex];
      // 重点： 记录每次循环的上一次分片位置，目的是让当前位置index插入在分片中   eg：[0,6,20]
      for (const itemIndex in this.divArr) {
        let divArrItem = this.divArr[itemIndex];
        let contactArr = [];
        let contactDot = 0;
        divArrItem.map((item, index) => {
          if (index == 0) {
            contactArr.push(1);
            contactDot = 0;
          } else {
            // 不是第一行的情况下比较和上一行的值
            if (item[key] === divArrItem[index - 1][key]) {
              // 值相同则放入0，第一个相同的合并方式数组加一
              contactArr[contactDot] += 1;
              contactArr.push(0);
            } else {
              contactArr.push(1);
              contactDot = index;
              // 记录分片的位置
              this.divIndex.push(index + divIndexTemp[itemIndex]);
              // 重点：插入分片中    eg：第一块分片位置index在0,6中插入   [0,2,3,5,6,20]  第二块分片位置index在6,20中插入[0,2,3,5,6,8,11,15,20]
              this.divIndex.sort((a, b) => {
                return a - b;
              }); // 因为是push进去  所以需要排序
              this.divIndex = [...new Set(this.divIndex)]; // 去重
            }
          }
        });
        divContactArr = divContactArr.concat(contactArr);
      }
      return divContactArr;
    },
    /**
     * 将数据分片，防止数据向下合并的时候跨级
     */
    sliceData() {
      this.divArr = [];
      for (let index = 0; index < this.divIndex.length; index++) {
        if (index == this.divIndex.length - 1) {
          // 如果最后一个则截取到数据最末尾
          this.divArr.push(this.testTableArr.slice(this.divIndex[index]));
        } else {
          // 截取两个分片位置之间的数据
          this.divArr.push(
            this.testTableArr.slice(
              this.divIndex[index],
              this.divIndex[index + 1]
            )
          );
        }
      }
    }
  },
  mounted() {
    // -----------------------------
    // 动态表格数据
    this.spanKey = ["serviceArr"];
    this.tableTitle = tableTitle;
    this.tableTitleKey = [
      "serviceArr",
      "indexArr",
      "stateArr",
      "attemptArr",
      "functionArr",
      "testingArr",
      "stateInfoArr",
      "referenceLogArr",
      "1",
      "2",
      "3",
      "4",
      "11",
      "12",
      "13",
      "14"
    ];
    this.getInit();
  }
};
</script>
<style lang="scss" >
@import "../../../../css/serviceFile/surveyUnit.css";
.surveyUnit {
/* 清除浮动的公共类 */
.clearfix:before,
.clearfix:after {
	content:"";
	display:table;
}
.clearfix:after {
	clear:both;
}
/* 为了兼容IE6,7 */
.clearfix {
	*zoom:1;
}
.topBox {


  // 左侧服务概况
  .boxLeft {
    width: 50%;
    height: 430px;
    border: 1px solid #3e74a3;
    background-color: #193153;
    box-sizing: border-box;
    margin-top: 10px;
    float: left;
    border-radius: 5px;
    .leftPei {
      width: 20%;
      height: 100%;
      box-sizing: border-box;
      float: left;
      #topPei {
        height: 200px;
        z-index: 999;
      }
      #bottomPei {
        height: 200px;
        z-index: 999;
      }
    }
    .rightTab {
      width: 80%;
      height: 100%;
      box-sizing: border-box;
      float: left;
      .topTab {
        text-align: center;
        .m10 {
          margin: 10px 0;
          color: white;
          font-size: 20px;
        }
        .el-table th,
        .el-table tr {
          background-color: #02356f;
          color: white;
          border-bottom: 1px solid #3e74a3;
          border-right: 1px solid #3e74a3;
          text-align: center;
        }
      }
      .bottomTab {
        .m10 {
          margin: 10px 0;
          color: white;
          font-size: 20px;
        }
        .el-table th,
        .el-table tr {
          background-color: #02356f;
          color: white;
          border-bottom: 1px solid #3e74a3;
          border-right: 1px solid #3e74a3;
          text-align: center;
        }
        text-align: center;
        margin-top: 10px;
        .el-table__header tr,
        .el-table__header th {
          padding: 0;
          height: 40px;
        }
        .el-table__body tr,
        .el-table__body td {
          padding: 0;
          height: 24px;
        }
        /* 最为关键得两个样式代码，可以设置全局滚动条样式，也可以按需设置 */
        ::-webkit-scrollbar {
          /* 设置竖向滚动条的宽度 */
          width: 4px;
          /* 设置横向滚动条的高度 */
          height: 5px;
        }
        ::-webkit-scrollbar-thumb {
          /*滚动条的背景色*/
          background-color: rgba(144, 147, 153, 0.3);
          border-radius: 5px;
          /* 设置竖向滚动条的宽度 */
          width: 4px;
          /* 设置横向滚动条的高度 */
          height: 5px;
        }
      }
    }
  }
  // 右侧指标概况
  .boxRight {
    width: 50%;
    height: 430px;
    background-color: #193153;
    box-sizing: border-box;
    margin-top: 10px;
    float: left;
    border-radius: 5px;
    .leftPei {
      width: 20%;
      height: 100%;
      background-color: #02356f;
      box-sizing: border-box;
      float: left;
      #topPei {
        height: 200px;
        z-index: 999;
      }
      #bottomPei {
        height: 200px;
        z-index: 999;
      }
    }
    .rightTab {
      width: 80%;
      height: 100%;
      box-sizing: border-box;
      float: left;
      .topTab {
        text-align: center;
        .m10 {
          margin: 10px 0;
          color: white;
          font-size: 20px;
        }
        .el-table th,
        .el-table tr {
          background-color: #02356f;
          color: white;
          border-bottom: 1px solid #3e74a3;
          border-right: 1px solid #3e74a3;
          text-align: center;
        }
      }
      .bottomTab {
        .m10 {
          margin: 10px 0;
          color: white;
          font-size: 20px;
        }
        .el-table th,
        .el-table tr {
          background-color: #02356f;
          color: white;
          border-bottom: 1px solid #3e74a3;
          border-right: 1px solid #3e74a3;
          text-align: center;
        }
        text-align: center;
        margin-top: 10px;
        .el-table__header tr,
        .el-table__header th {
          padding: 0;
          height: 40px;
        }
        .el-table__body tr,
        .el-table__body td {
          padding: 0;
          height: 24px;
        }
        /* 最为关键得两个样式代码，可以设置全局滚动条样式，也可以按需设置 */
        ::-webkit-scrollbar {
          /* 设置竖向滚动条的宽度 */
          width: 4px;
          /* 设置横向滚动条的高度 */
          height: 5px;
        }
        ::-webkit-scrollbar-thumb {
          /*滚动条的背景色*/
          background-color: rgba(144, 147, 153, 0.3);
          border-radius: 5px;
          /* 设置竖向滚动条的宽度 */
          width: 4px;
          /* 设置横向滚动条的高度 */
          height: 5px;
        }
      }
    }
  }
  }
  // 动态表格
  .botBox {
    width: 100%;
    height: 530px;
    border: 1px solid #3e74a3;
    margin-top: 20px;
    .el-table thead {
      color: red;
    }
    .titleColor1 {
      writing-mode: tb-rl;
    }
    .titleColor2 {
      writing-mode: tb-rl;
    }
    .el-table th,
    .el-table tr {
      background-color: #02356f;
      color: white;
      border-bottom: 1px solid #3e74a3;
      border-right: 1px solid #3e74a3;
      text-align: center;
    }
    .el-table--striped .el-table__body tr.el-table__row--striped td {
      background-color: #02356f;
    }
    /* 最为关键得两个样式代码，可以设置全局滚动条样式，也可以按需设置 */
    ::-webkit-scrollbar {
      /* 设置竖向滚动条的宽度 */
      width: 4px;
      /* 设置横向滚动条的高度 */
      height: 5px;
    }
    ::-webkit-scrollbar-thumb {
      /*滚动条的背景色*/
      background-color: rgba(144, 147, 153, 0.3);
      border-radius: 5px;
      /* 设置竖向滚动条的宽度 */
      width: 4px;
      /* 设置横向滚动条的高度 */
      height: 5px;
    }
  }

}
</style>
