<script>
import { Line, mixins } from 'vue-chartjs'
import Vue from 'vue'

//vue.forceUpdate()

export default({
  extends: Line,
  props : ["dataChart", "theBackgroundColor"],

  data(){
             return{
                dcValue :[],
                bgValue : ""
             }
  },  

  watch: {
        
        dataChart: function(val){
            
            this.renderChart({
     
            labels: ['0', '6.00 AM', '12.00 PM', '18.00 PM', '24.00 AM'],
            datasets: [
            {
              label: 'Amount Per Minute',
              data: this.dataChart,
              backgroundColor: this.theBackgroundColor
            }
          ]

          }, {responsive: true, maintainAspectRatio: false})

        }
  },



  mounted () {
    this.renderChart({
      //labels: ['M', 'T', 'W', 'T', 'F', 'S', 'S'],
      labels: ['0', '6.00 AM', '12.00 PM', '18.00 PM', '24.00 AM'],
      datasets: [
        {
          label: 'Amount Per Minute',
          //data: [12, 19, 3, 17, 6, 3, 7],
          //data: [0, 39, 10, 40, 39],
          data: this.dataChart,
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
    }, {responsive: true, maintainAspectRatio: false})
  }
})
</script>


