 <template>
    <div class="col-xs-2 col-sm-4 ml-0 mr-0">
        <div class="card">
            <div class="card-top">
                
                   <img src="src/images/battery.png" alt="" height="25" width="25" class="float-left mr-2">
                    <h6 class="float-left bold"> <strong>{{ title }}</strong></h6>
                            
            </div><!-- /.card-top -->
            <!-- <div class="card-body p-0 pt-4 pb-4 download-chart"> -->

            
            <div class="card-body p-0 pt-2 pb-2">   

                  <div class="row">
                        <div class="col-sm-2">
                            <div>
                                <img src="src/images/power.png" alt="" height="25" width="25" class="float-right">
                            </div>
                        </div> 
                        <div class="col-sm-4">
                             <div class="item text-left pl-0">
                                <h6><small>Power (W)</small></h6> 
                            </div>
                        </div> 
                        <div class="col-sm-4">
                            <div class="item text-center">
                                <!-- <span class="badge badge-dark">{{ power }}</span> -->
                                <h6 class="m-0 pb-0"><small>{{ power }}</small></h6>
                            </div> 
                        </div>   
                  </div>

                  <div class="row">
                        <div class="col-md-2">
                            <div>
                                <img src="src/images/level.png" alt="" height="25" width="25" class="float-right">
                            </div>
                        </div>
                        <div class="col-md-4">
                             <div class="item text-left">
                                <h6 class="m-0 pb-0"><small>Level</small></h6> 
                            </div>
                        </div> 
                        <div class="col-md-4">
                            <div class="item text-center">
                                <!-- <span class="badge badge-dark">{{ level }}</span> -->
                                <h6 class="m-0 pb-0"><small>{{ level }}</small></h6>
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
                                <h6 class="m-0 pb-1"><small>Current (A)</small></h6> 
                            </div>
                        </div> 
                        <div class="col-md-4">
                            <div class="item text-center">
                                <!-- <span class="badge badge-dark">{{ current }}</span> -->
                                <h6 class="m-0 pb-0"><small>{{ current }}</small></h6>
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
                                <!-- <span class="badge badge-dark">{{ voltage }}</span> -->
                                <h6 class="m-0 pb-0"><small>{{ voltage }}</small></h6>
                            </div> 
                        </div> 
                  </div>

                    <div class="row">
                        <div class="col-md-2">
                           <div>
                                <img src="src/images/switch.png" alt="" height="25" width="25" class="float-right">
                            </div>
                        </div> 
                        <div class="col-md-4">
                             <div class="item text-left">
                                <h6 class="m-0 pb-1"><small>Charging</small></h6> 
                            </div>     
                        </div>
                       
                        <div class="col-md-5">
                             
                                <h6 class="m-0 pb-0"><small><switchbutton v-model="switch1"></switchbutton></small></h6>
                            
                        </div>
                  </div>

                  <div class="row" >
                        <div class="col-md-2">
                            <div>
                                <img src="src/images/discharging.png" alt="" height="25" width="25" class="float-right">
                            </div>
                        </div> 
                        <div class="col-md-4">
                             <div class="item text-left">
                                <h6 class="m-0 pb-10"><small>Discharging</small></h6> 
                            </div>
                        </div> 
                        <div class="col-md-5 pb-10 mb-4">
                          
                                <h6 class="m-0 pb-10"><small><switchbutton v-model="switch2"></switchbutton></small></h6>
                            
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
    <!-- </div> -->
</template>



<script>
   
    import switchbutton from './switch-button.vue';

 
    export default{
       
        name: 'battery',
       
        props: ['title', 'power', 'current', 'voltage', 'level', 'charging', 'discharging', 'updatedTime'],

        methods: {
            
            getCurrentTime: function(){
	
          var today = new Date();
          var date = today.getFullYear()+'-'+(today.getMonth()+1)+'-'+today.getDate();
          var time = today.getHours() + ":" + today.getMinutes() + ":" + today.getSeconds()+":"+today.getMilliseconds();
          var dateTime = date+' '+time;

          return dateTime;
        }
            
        },

        watch :{
            switch1 : function(value){
                this.updatedTime = this.getCurrentTime();
                if(value){
                   
                    console.log("Charging on");
                    this.$emit('charging', 1);
                }
                else{
                     console.log("Charging off");
                     this.$emit('charging', 0);
                    
                }
                
            },

            switch2 : function(value){
                this.updatedTime = this.getCurrentTime();
                if(value){
                  
                    console.log("Discharging on");
                    this.$emit('discharging', 1);
                }
                else{
                     console.log("Discharging off");
                     this.$emit('discharging', 0);
                   
                }
                
            }
        },

        data: function() {
            return {
                switch1: false,
                switch2: false
            };
        },

       components: {
           switchbutton
        }  
    }
</script> 



<style scoped>
    .small {
        max-width: 600px;
    }
    .ml-1 {
    margin-button: 10px;
    }



</style>
