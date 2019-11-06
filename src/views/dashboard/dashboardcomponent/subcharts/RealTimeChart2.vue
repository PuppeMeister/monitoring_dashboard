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
                lineWidth: 1.2
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
            tickSize: [1, "minute"],
            tickFormatter: function(v, axis) {
                var date = new Date(v);
                
                //console.log("seconds --> "+date.getSeconds()+" || "+(date.getSeconds() % 20 == 0));
                //if (date.getSeconds() % 30 == 0) {
                    var hours = date.getHours() < 10 ? "0" + date.getHours() : date.getHours();
                    var minutes = date.getMinutes() < 10 ? "0" + date.getMinutes() : date.getMinutes();
                    var seconds = date.getSeconds() < 10 ? "0" + date.getSeconds() : date.getSeconds();

                    return hours + ":" + minutes + ":" + seconds;
                /*} else {
                   
                    return "";
                }*/
                
                /*function AddMinutesToDate(date, minutes) {
                        return new Date(date.getTime() + minutes*60000);
                 
                }
                function DateFormat(date){
                    var hours = date.getHours();
                    var minutes = date.getMinutes();
                    minutes = minutes < 10 ? '0' + minutes : minutes;
                    var strTime = hours + ':' + minutes;
                    return strTime;
                }

                function msToTime(duration) {
                   // var milliseconds = parseInt((duration % 1000) / 100),
                        //seconds = Math.floor((duration / 1000) % 60),
                    var minutes = Math.floor((duration / (1000 * 60)) % 60);
                    var hours = Math.floor((duration / (1000 * 60 * 60)) % 24);

                    hours = (hours < 10) ? "0" + hours : hours;
                    minutes = (minutes < 10) ? "0" + minutes : minutes;
                    

                    return hours + ":" + minutes;
                }

                //Calculate one hour Different
                var res = []; var now = "";
                if(timeSaver  == ""){
                    now = new Date();
                    timeSaver = DateFormat(now);
                    now = now.getTime();
                    //res.push(timeSaver);    
                }

                for(var i=0; i<3; i++){
                    
                    now = (now + 15*60000);
                    //now = AddMinutesToDate(now, 15);
                    console.log(now);
                    timeSaver =  msToTime(now);
                    console.log("timeSaver --> "+timeSaver);
                    res.push(timeSaver);
                    
                }

                //console.log("Diff --> "+ res[3] - res[0]);
                console.log("res --> "+res); */
                //console.log(DateFormat(now));
               // var next = AddMinutesToDate(now, 15);
               // return (DateFormat(next));
               
               //return res;
               

            },
            axisLabel: "Time",
            axisLabelUseCanvas: true,
            axisLabelFontSizePixels: 9,
            axisLabelFontFamily: 'Verdana, Arial',
            axisLabelPadding: 10,
            
        },
        yaxes: [{
            min: 0,
            max: 10,
            tickSize: 1,
            /*tickFormatter: function(v, axis) {
                if (v % 10 == 0) {
                    return v + "%";
                } else {
                    return "";
                }
            },*/
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
  var nowIntialize = "";
  var timeSaver = "";
  var doer = jquery;

  export default{
      name: 'dashboard-realtime-chart',

      props: ['realTimeValue', 'label', 'valueCanvasId', 'updatedTime'],

      data(){
        return{
            
            color: "#8d1aff",
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
                this.temp = [xData += this.updateInterval,  this.realTimeValue];
                this.data.unshift(this.temp);


                this.dataset = [{
                    label: this.label+this.realTimeValue+" watt",
                    data: this.data,
                    lines: {
                        fill: true,
                        lineWidth: 1.2
                    },
                    color: this.color
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
                        fill: true,
                        lineWidth: 1.2
                    },
                    color: this.color
                }];

                //this.plot5 = jQuery.plot('#flotRealtime2',   this.dataset, config);
                 
                 this.plot5.setData(this.dataset);
                 this.plot5.setupGrid();
                 this.plot5.draw();
                
          },

          

          getInitialData: function(){
              
              nowIntialize = new Date();
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
                        fill: true,
                        lineWidth: 1.2
                    },
                    color: this.color
          }];
        
        //console.log("aaa --> "+this.valueCanvasId)
        
        this.plot5 = doer.plot("#"+this.valueCanvasId,  this.dataset, config);

        this.interval = setInterval(function () {
                 this.getUpdateMocking()
            }.bind(this), this.updateInterval);
    }
  }

</script>