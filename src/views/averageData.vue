  <template>
    <div class="containerBox">
      
      <div class="container">
        <el-table
          border
          :data="resultData"
          style="width: 100%">
          <el-table-column
            prop="ResultId"
            label="Result id"
            width="180">
          </el-table-column>
          <el-table-column
            prop="Time"
            label="Time">
          </el-table-column>
          <el-table-column
            prop="AVG"
            label="AVG(temp)">
          </el-table-column>
        </el-table>
        <div id="myChart"></div>
      </div>
      <div class="echart" id="mychart2" :style="myChartStyle"></div>
       <router-link to="/userMarkAverage"><el-button type="primary" >Confirm</el-button></router-link>
    </div>
  </template>

  <script>
  // import echarts from 'echarts'	
  import * as echarts from 'echarts';
  console.log(echarts,'echarts');
      export default {
        data() {
          return {
            resultData:[{
              ResultId:'\u03B11',
              Time:'11AM',
              AVG:'34.6',
              Label:'Hodl-out',
              v:'-',
            },{
              ResultId:'\u03B12',
              Time:'12PM',
              AVG:'56.6',
              Label:'Outlier',
              v:'< -1 >',
            },{
              ResultId:'\u03B13',
              Time:'1PM',
              AVG:'50',
              Label:'Outlier',
              v:'< -1 >',
            }],
            echartsOption: {	
                  legend: {	
                      data: ['11AM', '12PM', '1PM']
                  },
                  tooltip: {   
                      trigger: 'axis'
                  },
                  series: [{
                    name: 'pie chart',
                    type: 'pie',
                    barWidth: '60%',
                    data: [	
                      {value: 0.33, name: '11AM'},		
                      {value: 0.33, name: '12PM'},
                      {value: 0.33, name: '1PM'},
                    ],
                  }],
              },
             myChart: {},
            xData: [], 
            yData: [	34.6, 56.6, 50], 
            myChartStyle: { float: "left", width: "100%", height: "400px" } 
          }
        },
        mounted(){
          let myChart = echarts.init(document.getElementById('myChart'), 'light')	
          myChart.setOption(this.echartsOption)	
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
                type: "line" 
              }
            ]
          };
          this.myChart = echarts.init(document.getElementById("mychart2"));
          this.myChart.setOption(option);
          window.addEventListener("resize", () => {
            this.myChart.resize();
          });
    }
        }
      }
    </script>

  <style scoped>
  .containerBox{
    padding: 100px 0 0 50px;
  }
  .container{
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-top: 20px;
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