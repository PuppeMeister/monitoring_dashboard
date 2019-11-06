<template>
    <div class="col-lg-6">
        <div class="card">
            <div class="card-top">
                <h4 class="card-title m-0 float-left">{{ title }}</h4><!-- /.content-title -->
                <!-- <div class="float-right text-r">
                    <button class="content-settings" data-toggle="tooltip" data-placement="top" title="Settings"><i class="fa fa-cog"></i></button>
                    <button class="content-collapse" data-toggle="tooltip" data-placement="top" title="Collapse"><i class="fa fa-angle-down"></i></button>
                    <button class="content-close" data-toggle="tooltip" data-placement="top" title="Close"><i class="fa fa-close"></i></button>
                </div> -->

            </div><!-- /.card-top -->
            <div class="card-body p-0">
                <real-time-chart canvasId="valueCanvasId" class="flotRealtime2" :realTimeValue ="realTimeValue" :label="label" :valueCanvasId ="valueCanvasId" :updatedTime="updatedTime"></real-time-chart>
                <!-- <real-time-chart canvasId ="valueCanvasId" class="valueCanvasId" :realTimeValue ="realTimeValue" :label="label" :valueCanvasId ="valueCanvasId"></real-time-chart> -->
                
            </div>

        </div>
    </div>

</template>

<script>
import RealTimeChart from './subcharts/RealTimeChart.vue';

export default{
    props: ['title', 'bgclass', 'canvasId', 'realTimeValue', 'label', 'valueCanvasId', 'updatedTime'],
    components:{
        RealTimeChart
    },
    mounted () {
        
            //console.log("Test --> "+this.valueCanvasId);
        
    }

}
</script>