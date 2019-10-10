 <template>
    <div class="col-lg-4 col-md-6">
        <div class="card">
            <div class="card-top">
                
                   <img src="src/images/battery.png" alt="" height="50" width="50" class="float-left pr-0">
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
                                <!-- <span class="badge badge-dark">{{ power }}</span> -->
                                <h4 class="m-0 pb-0">{{ power }}</h4>
                            </div> 
                        </div>   
                  </div>

                  <div class="row">
                        <div class="col-md-2">
                            <div>
                                <img src="src/images/level.png" alt="" height="45" width="45" class="float-right">
                            </div>
                        </div>
                        <div class="col-md-4">
                             <div class="item text-left">
                                <h4 class="m-0 pb-0">Level</h4> 
                            </div>
                        </div> 
                        <div class="col-md-4">
                            <div class="item text-center">
                                <!-- <span class="badge badge-dark">{{ level }}</span> -->
                                <h4 class="m-0 pb-0">{{ level }}</h4>
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
                                <h4 class="m-0 pb-1">Current</h4> 
                            </div>
                        </div> 
                        <div class="col-md-4">
                            <div class="item text-center">
                                <!-- <span class="badge badge-dark">{{ current }}</span> -->
                                <h4 class="m-0 pb-0">{{ current }}</h4>
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
                                <!-- <span class="badge badge-dark">{{ voltage }}</span> -->
                                <h4 class="m-0 pb-0">{{ voltage }}</h4>
                            </div> 
                        </div> 
                  </div>

                
                  <div class="row">
                        <div class="col-md-2">
                            <div>
                                <img src="src/images/charging.png" alt="" height="45" width="45" class="float-right">
                            </div>
                        </div> 
                        <div class="col-md-4">
                             <div class="item text-left">
                                <h4 class="m-0 pb-1">charging</h4> 
                            </div>
                        </div> 
                        <div class="col-md-4">
                            <div class="item text-center">
                                <!-- <span class="badge badge-dark">{{ charging }}</span> -->
                                <h4 class="m-0 pb-0">{{ charging }}</h4>
                            </div> 
                        </div> 
                  </div>

                  <div class="row">
                        <div class="col-md-2">
                            <div>
                                <img src="src/images/discharging.png" alt="" height="45" width="45" class="float-right">
                            </div>
                        </div> 
                        <div class="col-md-4">
                             <div class="item text-left">
                                <h4 class="m-0 pb-1">Discharging</h4> 
                            </div>
                        </div> 
                        <div class="col-md-4">
                            <div class="item text-center">
                                <!-- <span class="badge badge-dark">{{ discharging }}</span> -->
                                <h4 class="m-0 pb-0">{{ discharging }}</h4>
                            </div> 
                        </div>
                  </div>
                
                <div class="row">
                        <div class="col-md-2">
                           <div>
                                <img src="src/images/switch.png" alt="" height="45" width="45" class="float-right">
                            </div>
                        </div> 
                        <div class="col-md-4">
                             <div class="item text-left">
                                <h4 class="m-0 pb-1">Charging</h4> 
                            </div>     
                        </div>
                       
                        <div class="col-md-5">
                             <!-- <switch-button v-model="switch1">Lorem ipsum dolor sit amet</switch-button> -->
                             <!-- <switchbutton></switchbutton> -->
                            
                                <h4 class="m-0 pb-0"><switchbutton v-model="switch1"></switchbutton> </h4>
                            
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
    import axios from 'axios';
    import switchbutton from './switch-button.vue';

    /*var switchComponentButton = { template: "#switch-button",
        
        model: {
                 prop: "isEnabled",
                 event: "toggle"
         },
        props: {
            isEnabled: Boolean,
            color: {
            type: String,
            required: false,
            default: "#4D4D4D"
            }
        },
        methods: {
            toggle: function() {
            this.$emit("toggle", !this.isEnabled);
            }
        }
    }*/
    export default{
       
        name: 'battery',
       
        props: ['title', 'power', 'current', 'voltage', 'level', 'charging', 'discharging'],

        methods: {

                    sendRequest: function () {
            
                        var urlWrapper ="http://127.0.0.1:19998/powerGeneration/amountPerMinute"
        
                        axios.get(urlWrapper)
                            .then(({data}) => {
                            this.amountPerMinute = data.finalResult
                            console.log("[Power Generation][Amount Per Minute] ", this.amountPerMinute)
                        })
                        .catch(error => {
                            console.log(error.response)
                        }) 
                    }        
            
        },

        watch :{
            switch1 : function(value){
                if(value){
                    this.sendRequest();
                }
                else{
                    console.log("Boong..");
                }
                
            }
        },

        data: function() {
            return {
            switch1: false
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
</style>
