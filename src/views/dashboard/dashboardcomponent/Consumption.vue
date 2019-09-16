 <template>
    <div class="col-lg-4 col-md-6">
        <div class="card">
            <div class="card-top">
               <!--  <div class="card-left float-left text-left"> -->
                    <!-- <iclass="icon-lg pe-7f-map-marker"></i> -->
                    <img src="src/images/home.png" alt="" height="50" width="50" class="float-right">
                    <h3 class="float-left bold"> <strong>Consumption</strong></h3>
                <!-- </div> -->
              
                            
            </div><!-- /.card-top -->
            <!-- <div class="card-body p-0 pt-4 pb-4 download-chart"> -->
             <div class="card-body p-0 pt-0 pb-0">   
                <!-- <h6 class="text-center"><Strong>{{totalConsumption}}</Strong> <span class="badge badge-info"> kWh </span></h6> -->
                 
                 
                 <div class = "small">
                    <line-chart-js :dataChart = "theDataChart" 
                    :theBackgroundColor ="bgValue"/>
                </div>
            </div>
            <div class="card-footer bg-white br-0 pl-5 pr-5 pt-0 pb-0">
                    <div class="row">
                    
                    <div class="col-md-6">
                        <div class="item text-center">
                            <span class="badge badge-dark">Total</span>
                             <h4 class="m-0 pb-1">{{totalConsumption}}<span> Watt</span></h4>
                           
                        </div>
                    </div>
                    <div class="col-md-6">
                        <div class="item text-center">
                            <span class="badge badge-dark">Yesterday</span>
                            <h4 class="m-0 pb-1">{{yesterdayConsumption}} <span> Watt </span></h4>
                        </div>
                    </div>
                    
                </div>
            </div>
        </div>
    </div>
</template>

<script>
    import ConsumptionChart from './subcharts/consumptionChart.vue';
    import LineChartJs from './subcharts/LineChartJConsumption.vue';
    import axios from 'axios';


    export default{
        components:{
            ConsumptionChart,
            LineChartJs,
        },

        data(){
             return{
                totalConsumption: "0", yesterdayConsumption : "0", amountPerMinute: "0",
                bgValue : "rgba(46, 204, 113, 0.6)",
                dataChart :[]
             }
        },
         methods: {

                pullAmountPerMinute: function () {
        
                    var urlWrapper ="http://127.0.0.1:19998/consumption/amountPerMinute"
       
                    axios.get(urlWrapper)
                        .then(({data}) => {
                        this.amountPerMinute = data.finalResult
                        console.log("[Consumption][Amount Per Minute] ", this.amountPerMinute)
                    })
                    .catch(error => {
                        console.log(error.response)
                    }) 
                },

                pullTotalConsumption: function () {
        
                    var urlWrapper ="http://127.0.0.1:19998/consumption/total"
       
                    axios.get(urlWrapper)
                        .then(({data}) => {
                        this.totalConsumption = data.finalResult
                        console.log("[Consumption][Total] ", this.totalConsumption)
                    })
                    .catch(error => {
                        console.log(error.response)
                    }) 
                },

                pullYesterdayConsumption: function () {
        
                    var urlWrapper ="http://127.0.0.1:19998/consumption/yesterday"
       
                    axios.get(urlWrapper)
                        .then(({data}) => {
                        this.yesterdayConsumption = data.finalResult
                        console.log("[Consumption][Yesterday] ", this.yesterdayConsumption)
                    })
                    .catch(error => {
                        console.log(error.response)
                    }) 
                },

                refreshAllConFunction: function(){
                    this.pullAmountPerMinute(),
                    this.pullTotalConsumption(),
                    this.pullYesterdayConsumption()

                }

        },
        
        computed: {
                theDataChart() {
                    console.log("My Amount Per Minute = "+this.amountPerMinute);
                    return [0, this.amountPerMinute, 0, 0, 0] 
                }
        },



        //mounted: function(){
        async mounted(){
            await this.pullAmountPerMinute()
            this.pullTotalConsumption()
            this.pullYesterdayConsumption()

            /*this.interval = setInterval(function () {
                this.$forceUpdate()
                console.log("Refresh the Dashboard")
        }.bind(this), 300);*/

        }
        
    }

</script>

<style scoped>
    /*canvas{
        min-width: inherit;
    },*/

  .small {
    max-width: 600px;
  }

</style>