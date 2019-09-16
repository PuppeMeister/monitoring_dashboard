 <template>
    <div class="col-lg-4 col-md-6">
        <div class="card">
            <div class="card-top">
                <!-- div class="card-left float-left text-left"> -->
                    <!-- <iclass="icon-lg pe-7f-map-marker"></i> -->
                    <img src="src/images/clock.png" alt="" height="50" width="50" class="float-right">
                   <h3 class="float-left bold"> <strong>Operational Time </strong></h3>
                <!-- </div> -->
              
                            
            </div><!-- /.card-top -->
            <!-- <div class="card-body p-0 pt-4 pb-4 download-chart"> -->
             <div class="card-body p-0 pt-5 pb-4" style = "height:342px"> 
                 <div><h1 class="text-center"><span class="badge badge-secondary">{{hour}}</span> hour <span class="badge badge-info">{{minute}}</span> minutes </h1> </div>  
                 
                 <!-- <DownloadChart/> -->
            </div>
            <!-- <div class="card-footer bg-white br-0 pl-5 pr-5 pt-0 pb-5">
                    <div class="row">
                    <div class="col-md-6">
                        <div class="item text-center">
                            <span class="badge badge-dark">Yesterday</span>
                            <h4 class="m-0 pb-1">{{total_1}}<span> kwH</span></h4>
                            
                        </div>
                    </div>
                    <div class="col-md-6">
                        <div class="item text-center">
                            <span class="badge badge-dark">Co2 Emission</span>
                             <h4 class="m-0 pb-1">{{total_2}}<span> kwH</span></h4>
                           
                        </div>
                    </div>
                    
                </div>
            </div> -->
        </div>
    </div>
</template>

<script>
    //import DownloadChart from './charts/DownloadChart.vue';
    import axios from 'axios';
    export default{
        components:{
            //DownloadChart
        },

        data(){
             return{
                currentAmount: "0", amountPerMinute : "0"
             }
        },
        
        created(){
            this.hourValue = "0", this.minuteValue = "0"
        },

        methods: {

                pullCurrentAmount: function () {
        
                    var urlWrapper ="http://127.0.0.1:19998/battery/currentAmount"
       
                    axios.get(urlWrapper)
                        .then(({data}) => {
                        this.currentAmount = data.finalResult
                        console.log("[Battery Level][Current Amount] ", this.currentAmount)
                    })
                    .catch(error => {
                        console.log(error.response)
                    }) 
                },

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
                }

         },

        computed: {
                hour() {
                    this.hourValue = (this.currentAmount / this.amountPerMinute) / 60
                    return Math.round(this.hourValue)
                },

                minute(){
                    this.minuteValue = this.currentAmount / this.amountPerMinute
                    return this.minuteValue
                }
        }, 

        async mounted() {
        
            await this.pullCurrentAmount()
            await this. pullAmountPerMinute()

            /*this.interval = setInterval(function () {
                this.doSomething()
                console.log("Refresh the Dashboard")
            }.bind(this), 30000);*/
          }
    }

</script>

<style scoped>
    .download-chart{
        height: 225px;
    }
    canvas{
        min-width: inherit;
    }
</style>