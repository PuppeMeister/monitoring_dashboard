<script>
import { Line, mixins } from 'vue-chartjs'
import Vue from 'vue'

//vue.forceUpdate()

export default({
  extends: Line,
  //props : ["dataChart", "labelsData", "theBackgroundColor", "forTest"],
  props : ["valueChart", "idxChart", "theBackgroundColor", "timeChart"],

  data(){
             return{
                dcValue :[],
                bgValue : "",
                arrayChart : [0,0,0,0,0,0],
                labelChart : [0,0,0,0,0,0]

             }
  },  

  methods: {
    
        renderTheChart: function () {

            this.renderChart({
                //labels: ['M', 'T', 'W', 'T', 'F', 'S', 'S'],
                //labels: ['0', '6.00 AM', '12.00 PM', '18.00 PM', '24.00 AM'],
                labels: this.labelChart,
                datasets: [
                  {
                    label: 'Amount Per Minute',
                    //data: [12, 19, 3, 17, 6, 3, 7],
                    //data: [0, 39, 10, 40, 39],
                    //data: this.dataChart,
                    data: this.arrayChart,
                    //backgroundColor: "rgba(46, 204, 113, 0.6)"
                    backgroundColor: this.theBackgroundColor
                  }
                ]

                /*scales: {
                    yAxes: [{
                        ticks: {
                        
                                //stepSize: 50,
                                //maxTicksLimit: 3
                                //min: 50,
                                //max: 100
                              }
                        }]    
                }*/
              }, 
          {responsive: true, maintainAspectRatio: false})
        }

  },
  
  watch: {
        
        idxChart(data){
         
          this.arrayChart[this.idxChart] = this.valueChart;
          this.labelChart[this.idxChart] = this.timeChart;
          
          console.log("LINE --> Solar Data Chart idx || "+this.idxChart+" || "+ this.arrayChart[this.idxChart]);

          this.renderTheChart();

          
        }
  },



  mounted () {
      this.renderTheChart()
  }
})
</script>


