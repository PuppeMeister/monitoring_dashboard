<script>
  import Vue from 'vue';
  import jquery from 'jquery';
 
  import '../../../../assets/js/lib/flot-chart/jquery.flot.js';
  import '../../../../assets/js/lib/flot-chart/excanvas.min.js';
  import '../../../../assets/js/lib/flot-chart/jquery.flot.pie.js';
  import '../../../../assets/js/lib/flot-chart/jquery.flot.spline.js';
  import '../../../../assets/js/lib/flot-chart/jquery.flot.time.js';
  import '../../../../assets/js/lib/flot-chart/jquery.flot.axislabels.js';
  import '../../../../assets/js/lib/flot-chart/jquery.flot.symbol.js';


  
   
  var config ={

        series: {
            lines: {
                lineWidth: 1.2,
                fill: true
            },
            bars: {
                align: "center",
                fillColor: {
                    colors: [{
                        opacity: 1
                    }, {
                        opacity: 1
                    }]
                },
                barWidth: 500,
                lineWidth: 1
            }
        },
        xaxis: {
            mode: "time",
            minTickSize: [1, "minute"],
            show: true,
            tickFormatter: function(v, axis) {
                
                var date = new Date(v);
                
                //console.log("seconds --> "+date.getSeconds()+" || "+(date.getSeconds() % 20 == 0));
                //if (date.getSeconds() % 30 == 0) {
                    var hours = date.getHours() < 10 ? "0" + date.getHours() : date.getHours();
                    var minutes = date.getMinutes() < 10 ? "0" + date.getMinutes() : date.getMinutes();
                    var seconds = date.getSeconds() < 10 ? "0" + date.getSeconds() : date.getSeconds();
                    
                    return hours + ":" + minutes + ":" + seconds;
                //} else {
                   
                    //return "";
                //}
                //return "";
            },
            axisLabel: "Time",
            axisLabelUseCanvas: true,
            axisLabelFontSizePixels: 9,
            axisLabelFontFamily: 'Verdana, Arial',
            axisLabelPadding: 10
        },
        yaxes: [{
            min: 0,
            max: 10,
            tickSize: 1,
            axisLabel: "watt",
            axisLabelUseCanvas: true,
            axisLabelFontSizePixels: 12,
            axisLabelFontFamily: 'Verdana, Arial',
            axisLabelPadding: 6
        }, {
            max: 5120,
            position: "right",
            axisLabel: "Disk",
            axisLabelUseCanvas: true,
            axisLabelFontSizePixels: 12,
            axisLabelFontFamily: 'Verdana, Arial',
            axisLabelPadding: 6
        }],
        legend: {
            noColumns: 0,
            position: "nw"
        },
        grid: {
            backgroundColor: {
                colors: ["#ffffff", "#EDF5FF"]
            }
        }
       

  };
  var now = new Date().getTime();
  var doer = jquery;

  export default{
      name: 'dashboard-realtime-chart',

      props: ['realTimeValue', 'label', 'valueCanvasId', 'updatedTime'],

      data(){
        return{
            
            plot5: "",
            updateInterval : 6000,
            data : [],
            dataset: "",
            totalPoints : 100,
            temp :""

        }
      },
      template: "<div :id='valueCanvasId'></div>",
      
      methods:{
            getUpdate: function(){
                
                this.data.pop();
                //this.temp = [now+= this.updateInterval, this.realTimeValue];
               
                
                var xData = new Date().getTime();
                var xAxisValue = xData += this.updateInterval;
                console.log("xAxisValue --> "+xAxisValue);
                this.temp = [xAxisValue, this.realTimeValue];
                this.data.unshift(this.temp);


                this.dataset = [{
                    label: this.label+this.realTimeValue+" watt",
                    data: this.data,
                    lines: {
                        /*fill: true,
                        lineWidth: 1.2*/
                    },
                    color: "#00FF00"
                }];

                 this.plot5.setData(this.dataset);
                 this.plot5.setupGrid();
                 this.plot5.draw();
                
          },

          getUpdateMocking: function(){

                this.data.pop();
                //console.log("Test Test Test --> "+this.data.length);
                var value =  Math.random() * 8;
               // console.log("Sumbu X "+ (now += this.updateInterval));

                var xData = new Date().getTime();
                this.temp = [xData += this.updateInterval, value];
                this.data.unshift(this.temp);


                this.dataset = [{
                    label: this.label+value+" watt",
                    data: this.data,
                    lines: {
                        //fill: false,
                        //lineWidth: 1.2
                    },
                    color: "#00FF00"
                }];
                
                 this.plot5 = doer.plot("#"+this.valueCanvasId,  this.dataset, config);
                 //this.plot5.setData(this.dataset);
                 //this.plot5.setupGrid();
                 //this.plot5.draw();
                
          },

          

          getInitialData: function(){
              
              for (var i = 0; i < this.totalPoints; i++) {
                  var temp = [now += this.updateInterval, 0];

                  this.data.push(temp);
              
             }
              
          } 

      },

      watch:{

          updatedTime(newValue){
              this.getUpdate()
          }

      },

      mounted () {
        
        this.getInitialData();

          this.dataset = [{
                    label: this.label+0+" watt",
                    data: this.data,
                    lines: {
                        //fill: false,
                        //lineWidth: 1.2
                    },
                    color: "#00FF00"
          }];
        
        //console.log("aaa --> "+this.valueCanvasId)
        
        this.plot5 = doer.plot("#"+this.valueCanvasId,  this.dataset, config);

        /*this.interval = setInterval(function () {
                 this.getUpdateMocking()
            }.bind(this), this.updateInterval);*/

    }
  }

</script>