<template>
  <div class="containerBox">
    <div class="container">
        <div class="leftBox">
          <div class="searchBox" >
            <el-input type="text" v-model="value1" placeholder="max"></el-input> <span>-</span>
            <el-input type ="text" v-model="value2" placeholder="min"></el-input>
            <el-button type="primary">Search</el-button>
        </div>
           <el-table
      :data="tableData"
      border
      :default-sort = "{prop: 'Tuple_id', prop: 'Time', prop: 'SensorID', prop: 'Voltage',prop: 'Humidity ',prop: 'Temp ',order: 'descending'}"
      style="width: 100%">
      <el-table-column
        sortable
        prop="Tuple_id"
        label="Tuple_id"
        width="180">
      </el-table-column>
      <el-table-column
        sortable
        prop="Time"
        label="Time"
        width="180">
      </el-table-column>
      <el-table-column
        sortable
        prop="SensorID"
        label="SensorID">
      </el-table-column>
      <el-table-column
        sortable
        prop="Voltage"
        label="Voltage">
      </el-table-column>
      <el-table-column
        sortable
        prop="Humidity"
        label="Humidity">
      </el-table-column>
      <el-table-column
        sortable
        prop="Temp"
        label="Temp">
      </el-table-column>
        </el-table>
        </div>
     <div id="myChart"></div>
    </div>
     <div class="echart" id="mychart2" :style="myChartStyle"></div>
      <router-link to="/averageData"><el-button type="primary" >Search</el-button></router-link>
  </div>
</template>

<script>
// import echarts from 'echarts'	// 引入echarts
import * as echarts from 'echarts';
console.log(echarts,'echarts');
    export default {
      data() {
        return {
          tableData: [{
            Tuple_id: 'T1',
            Time: '11AM',
            SensorID: 1,
            Voltage:2.64,
            Humidity:0.4,
            Temp:34
          },{
            Tuple_id: 'T2',
            Time: '11AM',
            SensorID: 2,
            Voltage:2.65,
            Humidity:0.5,
            Temp:35
          },{
            Tuple_id: 'T3',
            Time: '11AM',
            SensorID: 3,
            Voltage:2.63,
            Humidity:0.4,
            Temp:35
          },{
            Tuple_id: 'T4`',
            Time: '12PM',
            SensorID: 1,
            Voltage:2.7,
            Humidity:0.3,
            Temp:35
          },{
            Tuple_id: 'T5',
            Time: '12PM',
            SensorID: 2,
            Voltage:2.7,
            Humidity:0.5,
            Temp:35
          },{
            Tuple_id: 'T6',
            Time: '12PM',
            SensorID: 3,
            Voltage:2.3,
            Humidity:0.4,
            Temp:100
          },{
            Tuple_id: 'T7',
            Time: '1PM',
            SensorID: 1,
            Voltage:2.7,
            Humidity:0.3,
            Temp:35
          },{
            Tuple_id: 'T8`',
            Time: '1PM',
            SensorID: 2,
            Voltage:2.7,
            Humidity:0.5,
            Temp:35
          },{
            Tuple_id: 'T9',
            Time: '1PM',
            SensorID: 3,
            Voltage:2.3,
            Humidity:0.5,
            Temp:80
          }],
           echartsOption: {	// echarts for graph data and format
                legend: {	
                    data: ['11AM', '12PM', '1PM']
                },
                tooltip: {   //cursor
                    trigger: 'axis'
                },
                series: [{
                  name: 'pie chart',
                  type: 'pie',
                  barWidth: '60%',
                  data: [	// pie chart： {value, name}
                    {value: 0.6, name: '11AM'},		// value not nessarily be scale
                    {value: 0.2, name: '12PM'},
                    {value: 0.2, name: '1PM'},
                  ],
                }],
            },
            myChart: {},
            xData: [], 
            yData: [23, 24, 18, 25, 27, 28, 25], 
            myChartStyle: { float: "left", width: "100%", height: "400px" } 
              }
      },
      mounted(){
        let myChart = echarts.init(document.getElementById('myChart'), 'light')	// initilize echarts, theme == light
        myChart.setOption(this.echartsOption)	// echarts option
        this.initEcharts();
      },
      methods:{
        initEcharts() {
          const option = {
            xAxis: {
              data: this.xData
            },
            yAxis: {},
            series: [
              {
                data: this.yData,
                type: "line" // line graph
              }
            ]
          };
          this.myChart = echarts.init(document.getElementById("mychart2"));
          this.myChart.setOption(option);
          //resize according to scale
          window.addEventListener("resize", () => {
            this.myChart.resize();
          });
    }
  }
    }
  </script>

<style scoped>
.container{
  display: flex;
  justify-content: space-between;
  margin-top: 20px;
}
.containerBox{
     padding: 100px 0 0 50px;
}
.leftBox{
  /* margin: 0 auto !important;; */
  width: 50% !important;
  position: relative;
}
.searchBox{
  position: absolute;
  display: flex;
  align-items: center;
  right: 0;
  top: -60px;
}
.searchBox .el-input{
  margin-right: 15px;
}
.searchBox span{
  margin-right: 15px;
}
#myChart{
  width: 50%;
  height: 200px;
  margin: 0 auto;
  margin-top: 5%;
}
canvas{
     aspect-ratio: auto 900 / 500;
}
</style>