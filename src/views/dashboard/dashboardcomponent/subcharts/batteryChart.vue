<template>
  <div class="chart-download">
    <canvas id="battery-chart" width="200px" height="200px"></canvas>
    <span id="battery-gauge-value"> % </span>
  </div>
</template>

<script>
import Vue from 'vue';
import { Donut, Gauge } from 'gaugeJS';

  export default{
  
  //props: ['percentageValue', 'currentValue', 'maxValue'],
  props: ['percentageValue'],

  created(){
            this.percentageReceivedValue = "0"
  },
  
  watch: {
        
        percentageValue: function(val){
            
            this.fillChart()

        }
  },

  computed: {
                dynamicPercentageValue() {
                  //this.percentageReceivedValue = this.percentageValue
                  this.percentageReceivedValue = (this.currentValue / this.maxValue)*100
                   return this.percentageReceivedValue
                }
  },

  methods: {
        initializeChart: function () {

            console.log("[batteryChart][percentageValue] = ", this.dynamicPercentageValue)
          var opts = {
            lines: 14,
            angle: 0.5,
            lineWidth: 0.1,
            limitMax: 'false', 
            percentColors: [[0.0, "#cccccc" ], [0.50, "#ffff00"], [1.0, "#ff0000"]],
            strokeColor: '#ffa726',
            generateGradient: true,
            highDpiSupport: true,


            colorStart: '#cdcdcd',
            colorStop: '#D65DB1', 
            strokeColor: '#e6e9ec',
            generateGradient: true
          };
          var target = document.getElementById("battery-chart");
          var gauge = new Donut(target).setOptions(opts);
          gauge.maxValue = 100;
          gauge.animationSpeed = 40;
          gauge.set(0);
          
          gauge.setTextField(document.getElementById("battery-gauge-value"));

        },

        fillChart: function () {

            console.log("[batteryChart][percentageValue] = ", this.dynamicPercentageValue)
          var opts = {
            lines: 14,
            angle: 0.5,
            lineWidth: 0.1,
            limitMax: 'false', 
            percentColors: [[0.0, "#cccccc" ], [0.50, "#ffff00"], [1.0, "#ff0000"]],
            strokeColor: '#ffa726',
            generateGradient: true,
            highDpiSupport: true,


            colorStart: '#cdcdcd',
            colorStop: '#D65DB1', 
            strokeColor: '#e6e9ec',
            generateGradient: true
          };
          var target = document.getElementById("battery-chart");
          var gauge = new Donut(target).setOptions(opts);
          gauge.maxValue = 100;
          gauge.animationSpeed = 40;
          gauge.set(this.percentageValue);
          
          gauge.setTextField(document.getElementById("battery-gauge-value"));


        },

  },

  mounted () {
        
        this.initializeChart()
          
   }
}

</script>


<style scoped>
  #battery-chart{
    margin-left: 30%;
    margin-top: 2%;
  }
  #battery-gauge-value {
      color: #000 !important;
      -webkit-tap-highlight-color: rgba(0, 0, 0, 0);
      text-anchor: middle;
      font-family: Arial;
      font-size: 29px;
      font-weight: bold;
      fill-opacity: 1;
      position: absolute;
      left: 45%;
      top: 38%;
  }
  #battery-gauge-value:after{
    content: "%";
  }
</style>