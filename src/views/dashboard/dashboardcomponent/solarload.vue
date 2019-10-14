 <template>
    <div class="col-lg-4 col-md-6">
        <div class="card">
            <div class="card-top">
                
                   <img src="src/images/solarPanel.png" alt="" height="50" width="50" class="float-left pr-0">
                    <h3 class="float-left bold pb-0"> <strong>{{ title }}</strong></h3>
                            
            </div><!-- /.card-top -->
            <!-- <div class="card-body p-0 pt-4 pb-4 download-chart"> -->

            
            <div class="card-body p-0 pt-2 pb-2">   

                  <div class="row">
                        <div class="col-md-2">
                            <div>
                                <img src="src/images/power.png" alt="" height="45" width="45" class="float-right">
                            </div>
                        </div> 
                        <div class="col-md-4">
                             <div class="item text-left pl-0">
                                <h4>Power</h4> 
                            </div>
                        </div> 
                        <div class="col-md-4">
                            <div class="item text-center">
                                <!-- <span class="badge badge-dark">{{ this.power }}</span> -->
                                 <h4 class="m-0 pb-0">{{ power }}</h4> 
                            </div> 
                        </div>   
                  </div>

                  <div class="row">
                        <div class="col-md-2">
                            <div>
                                <img src="src/images/current.png" alt="" height="45" width="45" class="float-right">
                            </div>
                        </div>
                        <div class="col-md-4">
                             <div class="item text-left">
                                <h4 class="m-0 pb-0">Current</h4> 
                            </div>
                        </div> 
                        <div class="col-md-4">
                            <div class="item text-center">
                                <!-- <span class="badge badge-dark">{{ this.current }}</span> -->
                                 <h4 class="m-0 pb-0">{{current }}</h4> 
                            </div> 
                        </div> 
                  </div>

                  <div class="row">
                      <div class="col-md-2">
                            <div>
                                <img src="src/images/voltage.png" alt="" height="45" width="45" class="float-right">
                            </div>
                        </div> 
                        <div class="col-md-4">
                             <div class="item text-left">
                                <h4 class="m-0 pb-1">Voltage</h4> 
                            </div>
                        </div> 
                        <div class="col-md-4">
                            <div class="item text-center">
                               <!--  <span class="badge badge-dark">{{ voltage }}</span> -->
                                <h4 class="m-0 pb-0">{{ voltage }}</h4> 
                            </div> 
                        </div> 
                  </div>

                  <div class="row">
                        <div class="col-md-2">
                            <div>
                                <img src="src/images/daily.png" alt="" height="45" width="45" class="float-right">
                            </div>
                        </div> 
                        <div class="col-md-4">
                             <div class="item text-left">
                                <h4 class="m-0 pb-1">Daily</h4> 
                            </div>
                        </div> 
                        <div class="col-md-4">
                            <div class="item text-center">
                                <!-- <span class="badge badge-dark">{{ daily }}</span> -->
                                 <h4 class="m-0 pb-0">{{ daily }}</h4> 
                            </div> 
                        </div> 
                  </div>

                  <div class="row">
                      <div class="col-md-2">
                            <div>
                                <img src="src/images/monthly.png" alt="" height="45" width="45" class="float-right">
                            </div>
                        </div> 
                        <div class="col-md-4">
                             <div class="item text-left">
                                <h4 class="m-0 pb-1">Monthly</h4> 
                            </div>
                        </div> 
                        <div class="col-md-4">
                            <div class="item text-center">
                                <!-- <span class="badge badge-dark">{{ monthly }}</span> -->
                                 <h4 class="m-0 pb-0">{{ monthly }}</h4> 
                            </div> 
                        </div> 
                  </div>
                  <div class="row">
                        <div class="col-md-2">
                            <div>
                                <img src="src/images/annual.png" alt="" height="45" width="45" class="float-right">
                            </div>
                        </div> 
                        <div class="col-md-4">
                             <div class="item text-left">
                                <h4 class="m-0 pb-1">Annual</h4> 
                            </div>
                        </div> 
                        <div class="col-md-4">
                            <div class="item text-center">
                                <!-- <span class="badge badge-dark">{{ annual }}</span> -->
                                 <h4 class="m-0 pb-0">{{ annual }}</h4> 
                            </div> 
                        </div> 
                  </div>

                  <div class="row">
                        <div class="col-md-2">
                            <div>
                                <img src="src/images/total.png" alt="" height="45" width="45" class="float-right">
                            </div>
                        </div> 
                        <div class="col-md-4">
                             <div class="item text-left">
                                <h4 class="m-0 pb-1">Total</h4> 
                            </div>
                        </div> 
                        <div class="col-md-4">
                            <div class="item text-center">
                                <!-- <span class="badge badge-dark">{{ total }}</span> -->
                                 <h4 class="m-0 pb-0">{{ total }}</h4> 
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
    import axios from 'axios';
    export default({
       
    name: 'solarload',
    props: ['title', 'power', 'current', 'voltage', 'daily', 'monthly', 'annual', 'total'],

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