 <template>
    <div class="col-lg-6 col-md-6">
        <div class="card">
            <div class="card-top">
                <!-- <div class="card-left float-left text-left"> -->
                    <!-- <iclass="icon-lg pe-7f-map-marker"></i> -->
                   <img src="src/images/summer.png" alt="" height="50" width="50" class="float-right">
                    <h3 class="float-left bold"> <strong>{{ title }}</strong></h3>
                <!-- </div> -->
              
                            
            </div><!-- /.card-top -->
            <!-- <div class="card-body p-0 pt-4 pb-4 download-chart"> -->
             <div class="card-body p-0 pt-0 pb-0">   
               <!-- <h6 class="text-center"><Strong>{{ totalPowerGen }}</Strong><span class="badge badge-info"> kWh </span></h6> --> 
                  
                     
                     <div class = "small">
                             <line-chart-js
                                 :valueChart ="valueChart" 
                                 :theBackgroundColor ="bgColour"
                                 :idxChart ="idxChart"
                                 :timeChart ="timeChart"/>
                           
                      </div>
                        <!-- <h3 class="float-left bold"> <strong>{{ theDataChart }}</strong></h3> -->
                        <!-- <PowerChart/> -->
                  
            </div>
            <div class="card-footer bg-white br-0 pl-5 pr-5 pt-0 pb-0">
                    <!-- <div class="row">
                        <div class="col-md-4">
                            <div class="item text-center">
                                <span class="badge badge-dark">Total</span>
                                <h4 class="m-0 pb-1">{{ totalPowerGen }}<span> Watt</span></h4>
                                 <div class = "small">
                             <line-chart-js
                                 :dataChart ="theDataChart" 
                                 :theBackgroundColor ="bgColour"
                                 :labelsData ="labelsData"/>
                      </div>
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
    //import PowerChart from './subcharts/powerChart.vue';
    import LineChartJs from './subcharts/LineChartJConsumption.vue';
  
    
    export default {
        
        components:{
           LineChartJs
        
        },

       props : [ 'title', 'bgColour', 'valueChart', 'idxChart', 'timeChart'],
       
         methods: {

                
        
        },

        computed: {
           
        },
        
        watch: {
             
        },

        mounted: function(){
        

        }

    }

</script>

<style scoped>
    .small {
    max-width: 1000px;
  }
</style>