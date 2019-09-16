 <template>
    <div class="col-lg-4 col-md-6">
        <div class="card">
            <div class="card-top">
                <!-- <div class="card-left float-left text-left"> -->
                    <!-- <iclass="icon-lg pe-7f-map-marker"></i> -->
                    <img src="src/images/cloudly.png" alt="" height="50" width="50"  class="float-right">
                    <h3 class="float-left bold"> <strong> Weather </strong></h3>
                <!-- </div> -->
              
                            
            </div><!-- /.card-top -->
            <!-- <div class="card-body p-0 pt-4 pb-4 download-chart"> -->
             <div class="card-body p-0 pt-5 pb-5">   
                
                <template>
                    <weather 
                        api-key="b37fd9449e44814368785a4ab52e4b08"
                        title="Seoul"
                        latitude="37.5665"
                        longitude="126.9780"
                        language="en"
                    units="uk">
                    </weather>
                </template>

            </div>
            <!-- <div class="card-footer bg-white br-0 pl-5 pr-5 pt-0 pb-5">
                
            </div> -->
        </div>
    </div>
</template>

<script>
   import VueWeatherWidget from 'vue-weather-widget';
   import 'vue-weather-widget/dist/css/vue-weather-widget.css';

    export default{
        components:{
            'weather': VueWeatherWidget
        },
      
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