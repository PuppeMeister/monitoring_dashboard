 <template>
    <div class="col-lg-4 col-md-6">
        <div class="card">
            <div class="card-top">
                <!-- <div class="card-left float-left text-left"> -->
                    <!-- <iclass="icon-lg pe-7f-map-marker"></i> -->
                    <img src="src/images/danger.png" alt="" height="50" width="50" class="float-right">
                    <h3 class="float-left bold"> <strong> Warning / Error </strong> </h3>
                <!-- </div> -->
              
                            
            </div><!-- /.card-top -->
            <!-- <div class="card-body p-0 pt-4 pb-4 download-chart"> -->
             <div class="card-body p-0 pt-4 pb-4" style = "height:342px">
                <div>
                </div>   
                <basix-alert type="warning" :withCloseBtn="true" class="mr-2 ml-2" v-if="warningAvailable">
                    <span class="badge badge-pill badge-warning">Warning</span>
                    {{warningMessage}}
                </basix-alert> 

                <basix-alert type="success" class="mr-2 ml-2" v-else>
                    <span class="badge badge-pill badge-success">Info</span>
                    There is no warning message.
                  </basix-alert>
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
    import axios from 'axios'
    export default{
        components:{
            //DownloadChart
        },

        data(){
             return{
                warningMessage: "",
                warningAvailable: false
             }
        },

        watch: {
        
            warningMessage: function(val){
            
                this.warningAvailable = true

            }
        },

        //props: ['title', 'icon', 'canvas', 'heading', 'total_1', 'total_2'],

        methods: {

                pullCurrentWarning: function () {
        
                    var urlWrapper ="http://127.0.0.1:19998/warning"
       
                    axios.get(urlWrapper)
                        .then(({data}) => {

                        if(data.finalResult != ""){
                           this.warningMessage = data.finalResult
                           console.log("[Warning][Message] ", this.warningMessage)
                        }
                        
                    })
                    .catch(error => {
                        console.log(error.response)
                    }) 
                }
        },

        mounted() {    

            this.pullCurrentWarning()
 
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