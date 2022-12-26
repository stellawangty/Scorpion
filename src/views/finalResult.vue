<template>
  <div class="about">
    <div class="container">
         <el-table
      :data="tableData"
      border
      style="width: 100%">
      <el-table-column
        prop="Tuple_id"
        label="Tuple_id"
        width="100">
      </el-table-column>
      <el-table-column
        prop="Time"
        label="Time"
        width="100">
      </el-table-column>
      <el-table-column
        prop="SensorID"
        label="SensorID">
      </el-table-column>
      <el-table-column
        prop="Voltage"
        label="Voltage">
      </el-table-column>
      <el-table-column
        prop="Humidity"
        label="Humidity">
      </el-table-column>
      <el-table-column
        prop="Temp"
        label="Temp">
      </el-table-column>
    </el-table>
     <div id="myChart"></div>
    </div>
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
            Tuple_id: 'T6`',
            Time: '12PM',
            SensorID: 3,
            Voltage:2.3,
            Humidity:0.4,
            Temp:100
          },{
            Tuple_id: 'T9',
            Time: '1PM',
            SensorID: 3,
            Voltage:2.3,
            Humidity:0.5,
            Temp:35
          }],
           echartsOption: {	
                legend: {	
                    data: [ '12PM', '1PM']
                },
                tooltip: {   
                    trigger: 'axis'
                },
                series: [{
                  name: 'pie chart',
                  type: 'pie',
                  barWidth: '60%',
                  data: [	
                    {value: 0.5, name: '12PM'},	
                    {value: 0.5, name: '1PM'},
                  ],
                }],
            }
        }
      },
      mounted(){
        let myChart = echarts.init(document.getElementById('myChart'), 'light')	
        myChart.setOption(this.echartsOption)	
      }
    }
  </script>

<style scoped>
.container{
  display: flex;
  justify-content: space-between;
  align-items: center;
    padding: 100px 0 0 50px;
}
.el-table{
  /* margin: 0 auto !important;; */
  width: 50% !important;
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