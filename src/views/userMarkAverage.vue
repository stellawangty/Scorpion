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
          width="100">
        </el-table-column>
        <el-table-column
          prop="Time"
          label="Time">
        </el-table-column>
        <el-table-column
          prop="AVG"
          label="AVG(temp)"
          width="100">
        </el-table-column>
        <el-table-column
        width="100"
          label="Label">
          <template slot-scope="scope">
             <el-radio-group v-model="scope.row.Label">
              <el-radio label="Hold_out">Hold-out</el-radio>
              <el-radio label="Outlier">outlier</el-radio>
            </el-radio-group>
           </template>
        </el-table-column>
        <el-table-column
        width="220"
          label="v">
           <template slot-scope="scope">
              <input type="text" v-model="scope.row.v">
           </template>
        </el-table-column>
      </el-table>
      <div id="myChart"></div>
      </div>
       <router-link to="/finalResult"><el-button type="primary" >Confirm</el-button></router-link>
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
              Label:'Hold_out',
              v:'',
            },{
              ResultId:'\u03B12',
              Time:'12PM',
              AVG:'56.6',
              Label:'outlier',
              v:'-1',
            },{
              ResultId:'\u03B13',
              Time:'1PM',
              AVG:'50',
              Label:'outlier',
              v:'-1',
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