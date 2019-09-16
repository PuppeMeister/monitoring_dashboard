 <template>
    <div class="col-lg-4 col-md-6">
        <div class="card">
            <div class="card-top">
                <div class="card-left float-left text-left">
                    <!-- <iclass="icon-lg pe-7f-map-marker"></i> -->

                     <!-- <img src="src/images/batteryCharging.png" alt="" height="50" width="50"> -->
                    <!-- <h2 class="card-title float-right">   <img src="src/images/batteryCharging.png" alt="" height="50" width="50"> Real-time Power Quantity / Battery Level</h2> -->
                         <img src="src/images/batteryCharging.png" alt="" height="50" width="50">
                        <h3 class="float-right bold"> <strong> Battery Level </strong> </h3>
                    <!-- <h3 class ="card-subtitle text-muted float-right"> Battery Level (Current Power / Battery Specification) </h3> -->
                </div>
              
                            
            </div><!-- /.card-top -->
            <!-- <div class="card-body p-0 pt-4 pb-4 download-chart"> -->
            <!-- <div v-if="percentageReady" class="card-body p-0 pt-4 pb-4"> -->
             <div class="card-body p-0 pt-4 pb-4">       
                <!-- <h6 class="text-center"><Strong>0.000</Strong> <span class="badge badge-info"> kWh </span></h6> -->
                 <BatteryChart :percentageValue="percentage" />

            </div>
            <div class="card-footer bg-white br-0 pl-5 pr-5 pt-5 pb-5">
                    <div class="row">
                    <div class="col-md-6">
                        <div class="item text-center">
                            <span class="badge badge-dark">Current Amount</span>
                            <h4 class="m-0 pb-1">{{currentAmount}}<span> Watt</span></h4>
                            
                        </div>
                    </div>
                    <div class="col-md-6">
                        <div class="item text-center">
                            <span class="badge badge-dark">Max Amount </span>
                             <h4 class="m-0 pb-1">{{maxAmount}}<span> Watt</span> {{percentage}}</h4>
                           
                        </div>
                    </div>
                    
                </div>
            </div>
        </div>
    </div>
</template>

<script>
    import BatteryChart from './subcharts/batteryChart.vue';
    import axios from 'axios';

    export default{
        components:{
           BatteryChart
        },

        created(){
            this.percentageSendingValue = "0"
        },

        data(){
             return{
                currentAmount: "0", maxAmount : "0", percentageValue: 0, dataReady: false
             }
        },
         methods: {

                pullCurrentAmount: function () {
        
                    var urlWrapper ="http://127.0.0.1:19998/battery/currentAmount"
       
                    axios.get(urlWrapper)
                        .then(({data}) => {
                        this.currentAmount = data.finalResult
                        console.log("[Battery Level][Current Amount] ", this.this.currentAmount)
                    })
                    .catch(error => {
                        console.log(error.response)
                    }) 
                },

                pullMaxAmount: function () {
        
                    var urlWrapper ="http://127.0.0.1:19998/battery/maxAmount"
       
                    axios.get(urlWrapper)
                        .then(({data}) => {
                        this.maxAmount = data.finalResult
                        console.log("[Battery Level][Current Amount] ", this.maxAmount)
                    })
                    .catch(error => {
                        console.log(error.response)
                    }) 
                },

                calculatePercentage: function(){
                    this.percentageValue = (this.currentAmount / this.maxAmount) * 100
                    
                }

        },

        computed: {
                percentage() {
                    //return this.percentageValue
                    this.percentageSendingValue = (this.currentAmount / this.maxAmount) * 100
                    return this.percentageSendingValue
                }
        },

        async mounted() {
        
            await this.pullCurrentAmount()
            await this.pullMaxAmount()

            //console.log("[BatteryLevel][currentAmount] = ",this.currentAmount, "|| [maxAmount] = ", this.maxAmount, " || [percentageValue] = ", this.percentageValue)
            //this.percentageValue = (this.currentAmount / this.maxAmount) * 100
            //console.log("[BatteryLevel][currentAmount] = ",this.currentAmount, "|| [maxAmount] = ", this.maxAmount, " || [percentageValue] = ", percentage())
            //this.calculatePercentage()
            //this.dataReady = true
        }

        
       
    }
</script>

<style scoped>
    .battery-chart{
        height: 225px;
    }
    canvas{
        min-width: inherit;
    }
</style>