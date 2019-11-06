 <template>
    <div class="col-xs-2 col-sm-4 ml-0 mr-0">
        <div class="card">
            <div class="card-top">
                
                   <img src="src/images/solarPanel.png" alt="" height="25" width="25" class="float-left mr-2">
                    <h6 class="float-left bold"> <strong>{{ title }}</strong></h6>
                   
                            
            </div><!-- /.card-top -->
            <!-- <div class="card-body p-0 pt-4 pb-4 download-chart"> -->

            
            <div class="card-body p-0 pt-2 pb-2">   

                  <div class="row">
                        <div class="col-md-2">
                            <div>
                                <img src="src/images/power.png" alt="" height="25" width="25" class="float-right">
                            </div>
                        </div> 
                        <div class="col-md-4">
                             <div class="item text-left pl-0">
                                <h6><small>Power (W)</small></h6> 
                            </div>
                        </div> 
                        <div class="col-md-4">
                            <div class="item text-center">
                                <!-- <span class="badge badge-dark">{{ this.power }}</span> -->
                                 <h6 class="m-0 pb-0"><small>{{ power }}</small></h6> 
                            </div> 
                        </div>   
                  </div>

                  <div class="row">
                        <div class="col-md-2">
                            <div>
                                <img src="src/images/current.png" alt="" height="25" width="25" class="float-right">
                            </div>
                        </div>
                        <div class="col-md-4">
                             <div class="item text-left">
                                <h6 class="m-0 pb-0"><small>Current (A)</small></h6> 
                            </div>
                        </div> 
                        <div class="col-md-4">
                            <div class="item text-center">
                                <!-- <span class="badge badge-dark">{{ this.current }}</span> -->
                                 <h6 class="m-0 pb-0"><small>{{current }}</small></h6> 
                            </div> 
                        </div> 
                  </div>

                  <div class="row">
                      <div class="col-md-2">
                            <div>
                                <img src="src/images/voltage.png" alt="" height="25" width="25" class="float-right">
                            </div>
                        </div> 
                        <div class="col-md-4">
                             <div class="item text-left">
                                <h6 class="m-0 pb-1"><small>Voltage (V)</small></h6> 
                            </div>
                        </div> 
                        <div class="col-md-4">
                            <div class="item text-center">
                               <!--  <span class="badge badge-dark">{{ voltage }}</span> -->
                                <h6 class="m-0 pb-0"><small>{{ voltage }}</small></h6> 
                            </div> 
                        </div> 
                  </div>

                  <div class="row">
                        <div class="col-md-2">
                            <div>
                                <img src="src/images/daily.png" alt="" height="25" width="25" class="float-right">
                            </div>
                        </div> 
                        <div class="col-md-4">
                             <div class="item text-left">
                                <h6 class="m-0 pb-1"><small>Daily (Ah)</small></h6> 
                            </div>
                        </div> 
                        <div class="col-md-4">
                            <div class="item text-center">
                                <!-- <span class="badge badge-dark">{{ daily }}</span> -->
                                 <h6 class="m-0 pb-0"><small>{{ daily }}</small></h6> 
                            </div> 
                        </div> 
                  </div>

                  <div class="row">
                      <div class="col-md-2">
                            <div>
                                <img src="src/images/monthly.png" alt="" height="25" width="25" class="float-right">
                            </div>
                        </div> 
                        <div class="col-md-4">
                             <div class="item text-left">
                                <h6 class="m-0 pb-1"><small>Monthly (A)</small></h6> 
                            </div>
                        </div> 
                        <div class="col-md-4">
                            <div class="item text-center">
                                <!-- <span class="badge badge-dark">{{ monthly }}</span> -->
                                 <h6 class="m-0 pb-0"><small>{{ monthly }}</small></h6> 
                            </div> 
                        </div> 
                  </div>
                  <div class="row">
                        <div class="col-md-2">
                            <div>
                                <img src="src/images/annual.png" alt="" height="25" width="25" class="float-right">
                            </div>
                        </div> 
                        <div class="col-md-4">
                             <div class="item text-left">
                                <h6 class="m-0 pb-1"><small>Annual (A)</small></h6> 
                            </div>
                        </div> 
                        <div class="col-md-4">
                            <div class="item text-center">
                                <!-- <span class="badge badge-dark">{{ annual }}</span> -->
                                 <h6 class="m-0 pb-0"><small>{{ annual }}</small></h6> 
                            </div> 
                        </div> 
                  </div>

                  <div class="row mb-0">
                        <div class="col-md-2">
                            <div>
                                <img src="src/images/total.png" alt="" height="25" width="25" class="float-right">
                            </div>
                        </div> 
                        <div class="col-md-4">
                             <div class="item text-left">
                                <h6 class="m-0 pb-1"><small>Total (W)</small></h6> 
                            </div>
                        </div> 
                        <div class="col-md-4">
                            <div class="item text-center">
                                <!-- <span class="badge badge-dark">{{ total }}</span> -->
                                 <h6 class="mb-2"><small>{{ total }}</small></h6> 
                            </div> 
                        </div> 
                  </div>
                   <div class="row mb-0">
                        <div class="col-md-6">
                            <div class="item text-center mb-0">
                                 <!-- <h6 class="ml-5"><small>Last Updated : </small></span></h6> -->
                                  <span class="badge badge-dark ml-5">Last Updated : {{updatedTime}}</span>
                            </div>
                        </div>
                  </div>

                 </div>
            </div>
                 
            <div class="card-footer bg-white br-0 pl-5 pr-5 pt-0 pb-0">
                   
            </div>
        </div>
    </div>
</template>

<script>
   
    export default({
       
    name: 'solarload',
    props: ['title', 'power', 'current', 'voltage', 'daily', 'monthly', 'annual', 'total', 'updatedTime'],

        methods: {

        },

        computed: {
               
        },
        
        watch: {
            
        },

        mounted: function(){
        
        }
    })
</script> 



<style scoped>
    .small {
    max-width: 600px;
  }
</style>