 <template>
    <div class="col-lg-6 col-md-6">
        <div class="card">
            <div class="card-top">
                <!-- <div class="card-left float-left text-left">
                    <!-- <iclass="icon-lg pe-7f-map-marker"></i> -->
                   <img src="src/images/summer.png" alt="" height="50" width="50" class="float-right">
                    <h3 class="float-left bold"> <strong>{{ title }}</strong></h3>
                <!-- </div> -->
              
                            
            </div><!-- /.card-top -->
            <!-- <div class="card-body p-0 pt-4 pb-4 download-chart"> -->
             <div class="card-body p-0 pt-0 pb-0">   
               <!-- <h6 class="text-center"><Strong>{{ totalPowerGen }}</Strong><span class="badge badge-info"> kWh </span></h6> --> 
                  
                     
                      <div class = "small">
                             <line-chart-js :dataChart = "theDataChart" 
                                             :theBackgroundColor ="bgValue"/>
                      </div>
                        <!-- <PowerChart/> -->
                  
            </div>
            <div class="card-footer bg-white br-0 pl-5 pr-5 pt-0 pb-0">
                    <!-- <div class="row">
                        <div class="col-md-4">
                            <div class="item text-center">
                                <span class="badge badge-dark">Total</span>
                                <h4 class="m-0 pb-1">{{ totalPowerGen }}<span> Watt</span></h4>
                                
                            </div> 
                        </div>   
                        <div class="col-md-4">
                            <div class="item text-center">
                                <span class="badge badge-dark">Yesterday</span>
                                <h4 class="m-0 pb-1">{{ yesterdayPowerGen }}<span> Watt</span></h4>
                                
                            </div>
                        </div>
                        <div class="col-md-4">
                            <div class="item text-center">
                                <span class="badge badge-dark">Co2 Emission</span>
                                <h4 class="m-0 pb-1">{{ co2Emission}}<span> Watt</span></h4>
                            
                            </div>
                        </div>
                    
                    </div> -->
            </div>
        </div>
    </div>
</template>

<script>
    import PowerChart from './subcharts/powerChart.vue';
    import LineChartJs from './subcharts/LineChartJConsumption.vue';
    import axios from 'axios';
    export default{
        components:{
            PowerChart,
            LineChartJs
        },

        props: [ 'title' ],
        /*props: [ 'title', 
                {'heading' : String,
                 'total_1' : String,
                 'total_2' : String,
                 'chartValue' : String} ], */
       
        
        data(){
             return{
                totalPowerGen: "0", yesterdayPowerGen : "0", co2Emission : "0", amountPerMinute: "0",
                bgValue : "rgba(0, 123, 255, 0.5)"
             }
        },

         methods: {

                pullAmountPerMinute: function () {
        
                    var urlWrapper ="http://127.0.0.1:19998/powerGeneration/amountPerMinute"
       
                    axios.get(urlWrapper)
                        .then(({data}) => {
                        this.amountPerMinute = data.finalResult
                        console.log("[Power Generation][Amount Per Minute] ", this.amountPerMinute)
                    })
                    .catch(error => {
                        console.log(error.response)
                    }) 
                },

                pullco2Emissions: function () {
        
                    var urlWrapper ="http://127.0.0.1:19998/powerGeneration/co2emissions"
       
                    axios.get(urlWrapper)
                        .then(({data}) => {
                        this.co2Emission = data.finalResult
                        console.log("[Power Generation][CO2 Emissions] ", this.co2Emission)
                    })
                    .catch(error => {
                        console.log(error.response)
                    }) 
                },

                pullYesterdayPowerCons: function () {
        
                    var urlWrapper ="http://127.0.0.1:19998/powerGeneration/yesterday"
       
                    axios.get(urlWrapper)
                        .then(({data}) => {
                        this.yesterdayPowerGen = data.finalResult
                        console.log("[Power Generation][Yesterday Power Consumption] ", this.yesterdayPowerGen)
                    })
                    .catch(error => {
                        console.log(error.response)
                    }) 
                },

                pullTotalPowerCons: function () {
        
                    var urlWrapper ="http://127.0.0.1:19998/powerGeneration/total"
       
                    axios.get(urlWrapper)
                        .then(({data}) => {
                        this.totalPowerGen = data.finalResult
                        console.log("[Power Generation][Total Power Consumption] ", this.totalPowerGen)
                    })
                    .catch(error => {
                        console.log(error.response)
                    }) 
                },

                reloadAllData: function(){
                    this.pullAmountPerMinute()
                    this.pullco2Emissions()
                    this.pullYesterdayPowerCons()
                    this.pullTotalPowerCons()
                }
        
        
        },

        computed: {
                theDataChart() {
                    console.log("My Amount Per Minute = "+this.amountPerMinute);
                    return [0, this.amountPerMinute, 0, 0, 0] 
                }
        },


        mounted: function(){
        
        /*this.pullAmountPerMinute()
        this.pullco2Emissions()
        this.pullYesterdayPowerCons()
        this.pullTotalPowerCons()*/

        /*this.interval = setInterval(function () {
                this.reloadAllData()
                console.log("Refresh the Dashboard - Power Generation")
        }.bind(this), 30000);*/
        }

    }

</script>

<style scoped>
    .small {
    max-width: 600px;
  }
</style>