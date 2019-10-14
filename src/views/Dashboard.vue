<template>

    <div class="row">

        <!-- <DeviceInfo
            title="Device Name"
            icon="icon-lg pe-7f-comment"
            bgclass="bg-flat-color-1"
            :counter="deviceName"
          
        >
        </DeviceInfo>
        
        <DeviceInfo
            icon="icon-lg pe-7f-info"
            bgclass="bg-flat-color-1"
            :counter="deviceType"
            title="Device Type"
        >
        </DeviceInfo>

        <DeviceInfo
            icon="icon-lg pe-7f-map-marker"
            bgclass="bg-flat-color-1"
            :counter="deviceLocation"
            title="Device Location"
        >
        </DeviceInfo> -->
        
        <SolarLoad 
            title="Solar" 
            :power="solarPower" 
            :current="solarCurrent"
            :voltage="solarVoltage"
            :daily="solarDaily"
            :monthly="solarMonthly"
            :annual="solarAnnual"
            :total="solarTotal"></SolarLoad>

        

        <Battery
            title="Battery"
            :power="battPower" 
            :current="battCurrent"
            :voltage="battVoltage"
            :level="battLevel"
            :charging="charging"
            :discharging="discharging"> </Battery>

        <SolarLoad
            title="Load"
            :power="loadPower" 
            :current="loadCurrent"
            :voltage="loadVoltage"
            :daily="loadDaily"
            :monthly="loadMonthly"
            :annual="loadAnnual"
            :total="loadTotal"> </SolarLoad>

         <!-- <div class = "small">
                             <line-chart-js
                                 :dataChart ="dataChartSolar" 
                                 theBackgroundColor = "rgb(89, 165, 89)"
                                 :labelsData ="dataLabelSolar"/>
                      </div> -->

        <!-- <RealTime title="Real time"/> -->
        <!-- <PowerGeneration title = "Solar" bgColour = "rgb(89, 165, 89)" v-bind:theDataChart ="dataChartSolar" :labelsData="dataLabelSolar" :power="solarPower"/> -->
        <!-- <PowerGeneration title = "Power" bgColour = "rgba(0, 123, 255, 0.5)" :theDataChart ="dataChartPower" :labelsData="dataLabelPower"/> -->


        <PowerGeneration title = "Solar" bgColour = "rgb(89, 165, 89)" :valueChart ="solarPower" :idxChart="idxPowerSolar" :timeChart="timePowerSolar"/>
        <PowerGeneration title = "Power" bgColour = "rgba(0, 123, 255, 0.5)" :valueChart ="loadPower" :idxChart="idxPowerLoad" :timeChart="timePowerLoad"/>

        <!-- <Consumption />
        <BatteryLevel/> -->
        <!-- <Weather />
        <OperationalTime />
        <Warning /> -->

    </div>

</template>

<!-- <script src="/socket.io/socket.io.js"></script> -->
<script>

//import DeviceInfo from './dashboard/dashboardcomponent/DeviceInfo.vue';
import PowerGeneration from './dashboard/dashboardcomponent/PowerGeneration.vue';
/*import Consumption from './dashboard/dashboardcomponent/Consumption.vue';
import BatteryLevel from './dashboard/dashboardcomponent/BatteryLevel.vue';
import OperationalTime from './dashboard/dashboardcomponent/OperationalTime.vue';
import Weather from './dashboard/dashboardcomponent/Weather.vue';
import Warning from './dashboard/dashboardcomponent/Warningdashboard/dashboardcomponent/.vue';*/
import SolarLoad from './dashboard/dashboardcomponent/solarload.vue';
import Battery from './dashboard/dashboardcomponent/battery.vue';
import LineChartJs from './dashboard/dashboardcomponent/subcharts/LineChartJConsumption.vue';
import io from 'socket.io-client';

import axios from 'axios';

const socket = io('http://localhost:19997');

export default{
    
    name: 'dashboard',
    props: ['requestType'],

    data(){
        return{
            deviceName: "", deviceType: "", deviceLocation: "",
            
           
            solarPower : "0",
            solarCurrent : "0",
            solarVoltage : "0",
            solarAnnual : "0",
            solarDaily : "0",
            solarMonthly : "0",
            solarTotal: "0",

            loadPower : "0",
            loadCurrent : "0",
            loadVoltage : "0",
            loadAnnual : "0",
            loadDaily : "0",
            loadMonthly : "0",
            loadTotal : "0",

            battPower: "0", 
            battCurrent: "0",
            battVoltage:"0",
            battLevel:"0",
            charging : "No Status",
            discharging : "No Status",

            
            idxPowerSolar: 0,
            idxPowerLoad: 0,
            timePowerSolar: "",
            timePowerLoad: ""


        }
    },
   
    methods: {
        
        getCurrentTime: function(){
	
          var today = new Date();
          var date = today.getFullYear()+'-'+(today.getMonth()+1)+'-'+today.getDate();
          var time = today.getHours() + ":" + today.getMinutes() + ":" + today.getSeconds();
          var dateTime = date+' '+time;

          return dateTime;
        },

        requestDeviceType: function () {
        
            var urlWrapper ="http://127.0.0.1:19998/deviceInformation/deviceType"
       
                axios.get(urlWrapper)
                .then(({data}) => {
                    this.deviceType = data.finalResult
            
                })
                .catch(error => {
                    console.log(error.response)
                }) 
        },
       
        showSidebar: function(){
            this.$emit("showSidebar", true);
        },

        listenToServer : function(){

            // Solar Listener
            socket.on('solarCurrent', (data)=>{
                this.solarCurrent = data;
                //console.log("Solar Current = "+data);
            });

            socket.on('solarPower', (data)=>{ 
                this.solarPower = data;
                this.idxPowerSolar = localStorage.idxSolar;
                this.timePowerSolar = this.getCurrentTime();

                console.log("Solar Power = "+data+" || Time = "+this.timePowerSolar+" || idx = "+this.idxPowerSolar);
    
               
                
                //this.dataChartSolar[localStorage.count] = data;
                //console.log("Solar Data Chart idx || "+localStorage.count+" || "+ this.dataChartSolar[localStorage.count]);
                if(localStorage.idxSolar == 5){
                    localStorage.idxSolar = 0;
                }else{
                    localStorage.idxSolar++;
                }

            });
            
            socket.on('solarVoltage', (data)=>{ 
                this.deviceType = data;
                this.solarVoltage = data
                //console.log("Device Type = "+data);
                });
            
            socket.on('solarAnnual', (data)=>{
                this.solarAnnual = data;
                //console.log("Solar Annual = "+data);
            });

            socket.on('solarDaily', (data)=>{
                this.solarDaily = data;
                //console.log("Solar Daily = "+data);
            });

            socket.on('solarMonthly', (data)=>{
                this.solarMonthly = data;
                //console.log("Solar Monthly = "+data);
            });

            socket.on('solarAnnual', (data)=>{
                this.solarAnnual = data;
                //console.log("Solar Annual = "+data);
            });

            socket.on('solarTotal', (data)=>{
                this.solarTotal = data;
                //console.log("Solar total = "+data);
            });

            //Load Listener

            socket.on('loadCurrent', (data)=>{
                            this.loadCurrent = data;
                            //console.log("Load Current = "+data);
                });

                socket.on('loadVoltage', (data)=>{
                            this.loadVoltage = data;
                            //console.log("Load Voltage = "+data);
                });

                socket.on('loadPower', (data)=>{
                
                        this.loadPower = data;
                        this.idxPowerLoad = localStorage.idxLoad;
                        this.timePowerLoad = this.getCurrentTime();

                        console.log("Load Power = "+this.loadPower+" || Time = "+this.timePowerLoad+" || idx = "+this.idxPowerLoad);
            
                    
                        if(localStorage.idxLoad == 5){
                            localStorage.idxLoad = 0;
                        }else{
                            localStorage.idxLoad++;
                        }
                
                });

                socket.on('loadDaily', (data)=>{
                            this.loadDaily = data;
                            //console.log("Load Daily = "+data);
                });
                socket.on('loadMonthly', (data)=>{
                            this.loadMonthly = data;
                            //console.log("Load Monthly = "+data);
                });

                socket.on('loadAnnual', (data)=>{
                            this.loadAnnual = data;
                            //console.log("Load Annual = "+data);
                });

                socket.on('loadTotal', (data)=>{
                            this.loadTotal = data;
                            //console.log("Load Total = "+data);
                });
            
            //battery listener

                socket.on('battLevel', (data)=>{
                    this.battLevel= data;
                    console.log("Battery Level = "+data);
                });

                socket.on('battCurrent', (data)=>{
                    this.battCurrent= data;
                    console.log("Battery Current = "+data);
                });

                socket.on('battVoltage', (data)=>{
                    this.battVoltage= data;
                    console.log("Battery Voltage = "+data);
                });
                socket.on('battPower', (data)=>{
                    this.battPower= data;
                    console.log("Battery Power = "+data);
                });
                
                socket.on('charging', (data)=>{
                    this.charging= data;
                    console.log("Battery Charging = "+data);
                });

                socket.on('discharging', (data)=>{
                    this.discharging= data;
                    console.log("Battery Discharging = "+data);
                });

        }
    

    },

    
    components: {
        
         LineChartJs,
        //DeviceInfo,
        PowerGeneration,
        /*Consumption,
        BatteryLevel,
        OperationalTime,
        Weather,
        Warning,*/
        SolarLoad,
        Battery
    },
  
    

    mounted: function(){
        localStorage.idxSolar = 0;
        localStorage.idxLoad = 0;
        
        this.listenToServer();
       
    }
   
   
}



</script>

<style>

</style>