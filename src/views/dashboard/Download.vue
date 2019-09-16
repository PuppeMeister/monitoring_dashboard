 <template>
    <div class="col-lg-3 col-md-6">
        <div class="card">
            <div class="card-top">
                <div class="card-left float-left text-left">
                    <!-- <iclass="icon-lg pe-7f-map-marker"></i> -->
                    <img src="src/images/summer.png" alt="">
                    <h2 class="card-title float-right">Power Generation</h2>
                </div>
              
                            
            </div><!-- /.card-top -->
            <!-- <div class="card-body p-0 pt-4 pb-4 download-chart"> -->
             <div class="card-body p-0 pt-4 pb-4">   
                <h6 class="text-center">{{heading}}</h6> 
                 <DownloadChart/>
            </div>
            <div class="card-footer bg-white br-0 pl-5 pr-5 pt-0 pb-5">
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
            </div>
        </div>
    </div>
</template>

<script>
    import DownloadChart from './charts/DownloadChart.vue';
    export default{
        components:{
            DownloadChart
        },
        props: ['title', 'icon', 'canvas', 'heading', 'total_1', 'total_2']
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