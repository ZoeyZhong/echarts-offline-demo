<template>
  <div class="map-china-container">
    <div id="map-china" style="width: 800px; height: 700px"></div>
  </div>
</template>

<script>
import * as echarts from "echarts";
import "./china.js";
export default {
  name: "HelloWorld",
  created() {
    this.setEchartOption();
  },
  mounted() {
    this.$nextTick(() => {
      this.initEchartMap();
    });
  },
  beforeDestroy() {
    this.chartMap.clear(); // 清空 chart 数据
  },
  data() {
    return {
      // echart 配制 option
      options: {
        tooltip: {
          triggerOn: "mousemove", // mousemove、click
          padding: 8,
          borderWidth: 1,
          borderColor: "#FFCC00",
          backgroundColor: "rgba(255,255,255,0.9)",
          textStyle: {
            color: "#000000",
            fontSize: 13,
          },
          formatter: function (e, t, n) {
            let data = e.data;
            // console.log('当前省份数据：', data)
            return `
                                   <div class="tooltip-info">
                                       <h3>${data.name}</h3>
                                       <p class="tooltip-info-item"><span class="lebel">项目数量</span><span class="value">${data.value}</span></p>
                                       <p class="tooltip-info-item"><span class="lebel">设备数量</span><span class="value">${data.countDevice}</span></p>
                                       <p class="tooltip-info-item"><span class="lebel">报警数量</span><span class="value">${data.countAlarm}</span></p>
                                   </div>
                                `;
          },
        },
        // 图例样式
        visualMap: {
          show: true,
          left: 26,
          bottom: 40,
          showLabel: true,
          textStyle: {
            color: "white",
          },
          pieces: [
            // rgba(64,158,255,1)
            // rgba(0,222,255,1)
            // rgba(255,255,255,1)
            // rgba(76,217,100,1)
            {
              gte: 100,
              label: ">= 1000",
              color: "rgba(64,158,255,0.9)",
            },
            {
              gte: 500,
              lt: 999,
              label: "500 - 999",
              color: "rgba(64,158,255,0.8)",
            },
            {
              gte: 100,
              lt: 499,
              label: "100 - 499",
              color: "rgba(64,158,255,0.7)",
            },
            {
              gte: 10,
              lt: 99,
              label: "10 - 99",
              color: "rgba(64,158,255,0.6)",
            },
            {
              lt: 10,
              label: "<10",
              color: "rgba(64,158,255,0.5)",
            },
          ],
        },
        geo: {
          map: "china",
          scaleLimit: {
            min: 1,
            max: 10,
          },
          zoom: 1.1,
          top: 150, // 距离顶部距离
          label: {
            normal: {
              show: true,
              fontSize: "13px", // 地图省份文字大小
              color: "white", // 地图省份文字颜色
            },
            emphasis: {
              show: true,
              fontWeight: "bold",
              fontSize: "16px", // 地图省份文字 hover 大小
              color: "#000000",
            },
          },
          itemStyle: {
            normal: {
              areaColor: "rgba(255,255,255,0.7)",
              shadowBlur: 10,
              shadowColor: "rgba(0, 0, 0, 0.2)",
              borderColor: "rgba(0, 0, 0, 0.2)",
            },
            emphasis: {
              areaColor: "#f2d5ad",
              shadowOffsetX: 0,
              shadowOffsetY: 0,
              borderWidth: 1,
              borderColor: "#FF9500",
            },
          },
          // 某块被选中时的样式
          select: {
            label: {
              fontWeight: "bold",
              fontSize: "16px", // 地图省份文字 hover 大小
              color: "#000000", // 地图省份文字 hover 颜色
            },
            itemStyle: {
              areaColor: "#FFCC00", // 背景色
            },
          },
        },
        series: [
          {
            name: "项目数量",
            type: "map",
            geoIndex: 0,
            label: function () {},
            data: [],
          },
        ],
      },
      // echart data
      dataList: [
        { name: "南海诸岛", value: 100, countDevice: 4, countAlarm: 3 },
        { name: "北京", value: 540, countDevice: 4, countAlarm: 3 },
        { name: "天津", value: 130, countDevice: 4, countAlarm: 3 },
        { name: "上海", value: 400, countDevice: 4, countAlarm: 3 },
        { name: "重庆", value: 750, countDevice: 4, countAlarm: 3 },
        { name: "河北", value: 130, countDevice: 4, countAlarm: 3 },
        { name: "河南", value: 830, countDevice: 4, countAlarm: 3 },
        { name: "云南", value: 110, countDevice: 4, countAlarm: 3 },
        { name: "辽宁", value: 19, countDevice: 4, countAlarm: 3 },
        { name: "黑龙江", value: 150, countDevice: 4, countAlarm: 3 },
        { name: "湖南", value: 690, countDevice: 4, countAlarm: 3 },
        { name: "安徽", value: 60, countDevice: 4, countAlarm: 3 },
        { name: "山东", value: 5, countDevice: 4, countAlarm: 3 },
        { name: "新疆", value: 4, countDevice: 4, countAlarm: 3 },
        { name: "江苏", value: 31, countDevice: 4, countAlarm: 3 },
        { name: "浙江", value: 104, countDevice: 4, countAlarm: 3 },
        { name: "江西", value: 36, countDevice: 4, countAlarm: 3 },
        { name: "湖北", value: 52, countDevice: 4, countAlarm: 3 },
        { name: "广西", value: 33, countDevice: 4, countAlarm: 3 },
        { name: "甘肃", value: 7, countDevice: 4, countAlarm: 3 },
        { name: "山西", value: 5, countDevice: 4, countAlarm: 3 },
        { name: "内蒙古", value: 778, countDevice: 4, countAlarm: 3 },
        { name: "陕西", value: 22, countDevice: 4, countAlarm: 3 },
        { name: "吉林", value: 4, countDevice: 4, countAlarm: 3 },
        { name: "福建", value: 18, countDevice: 4, countAlarm: 3 },
        { name: "贵州", value: 5, countDevice: 4, countAlarm: 3 },
        { name: "广东", value: 98, countDevice: 4, countAlarm: 3 },
        { name: "青海", value: 1, countDevice: 4, countAlarm: 3 },
        { name: "西藏", value: 0, countDevice: 4, countAlarm: 3 },
        { name: "四川", value: 44, countDevice: 4, countAlarm: 3 },
        { name: "宁夏", value: 4, countDevice: 4, countAlarm: 3 },
        { name: "海南", value: 22, countDevice: 4, countAlarm: 3 },
        { name: "台湾", value: 3, countDevice: 4, countAlarm: 3 },
        { name: "香港", value: 5, countDevice: 4, countAlarm: 3 },
        { name: "澳门", value: 555, countDevice: 4, countAlarm: 3 },
      ],

      chartMap: null,
    };
  },
  methods: {
    // 初始化中国地图
    initEchartMap() {
      let mapElement = document.getElementById("map-china");
      this.chartMap = echarts.init(mapElement);
      this.chartMap.setOption(this.options);
      // 响应省份点击事件
      this.chartMap.on("click", (params) => {
        // params.data 是点击省份的数据，根据需要做自己的业务就可以了
        console.log(params);
      });
    },
    // 修改 echart 数据
    setEchartOption() {
      this.options.series[0]["data"] = this.dataList;
      this.chartMap.setOption(this.options);
      console.log(this.options.series);
    },
  },
};
</script>

<style scoped>
.map-china-container {
  height: 100%;
  position: relative;
}
.map-china-container #map-china {
  height: 100%;
}
</style>

<style>
#map-china .tooltip-info h3 {
  margin-bottom: 10px;
}
#map-china .tooltip-info-item {
  display: flex;
  justify-content: space-between;
  line-height: 1.7;
  overflow: hidden;
}
#map-china .tooltip-info-item .label {
}
#map-china .tooltip-info-item .value {
  text-align: right;
  width: 50px;
}
</style>
