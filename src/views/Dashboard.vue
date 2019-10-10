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

        <!-- <RealTime title="Real time"/> -->
        <PowerGeneration title = "Solar" />
        <PowerGeneration title = "Power" />
        <!-- <Consumption />
        <BatteryLevel/> -->
        <!-- <Weather />
        <OperationalTime />
        <Warning /> -->

    </div>

</template>

<!-- <script src="/socket.io/socket.io.js"></script> -->
<script>

import DeviceInfo from './dashboard/dashboardcomponent/DeviceInfo.vue';
import PowerGeneration from './dashboard/dashboardcomponent/PowerGeneration.vue';
import Consumption from './dashboard/dashboardcomponent/Consumption.vue';
import BatteryLevel from './dashboard/dashboardcomponent/BatteryLevel.vue';
import OperationalTime from './dashboard/dashboardcomponent/OperationalTime.vue';
import Weather from './dashboard/dashboardcomponent/Weather.vue';
import Warning from './dashboard/dashboardcomponent/Warning.vue';
import SolarLoad from './dashboard/dashboardcomponent/solarload.vue';
import Battery from './dashboard/dashboardcomponent/battery.vue';
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
            discharging : "No Status"


        }
    },
   
    methods: {
    
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

       requestDeviceName: function () {
        
            var urlWrapper ="http://127.0.0.1:19998/deviceInformation/deviceName"
       
            axios.get(urlWrapper)
                    .then(({data}) => {
                        this.deviceName = data.finalResult
                
                    })
                    .catch(error => {
                        console.log(error.response)
                    }) 
        
        
        },

        requestDeviceLocation: function () {
        
        var urlWrapper ="http://127.0.0.1:19998/deviceInformation/deviceLocation"
       
            axios.get(urlWrapper)
                    .then(({data}) => {
                        this.deviceLocation = data.finalResult
                
                    })
                    .catch(error => {
                        console.log(error.response)
                    }) 
        
        
        },


        reloadMyFunctions : function(){
                this.requestDeviceType()
                this.requestDeviceName()
                this.requestDeviceLocation()
        },

         printJson: function(){
                console.log("One Sweet Day", this.generalInformation);
         
        },
    
        showSidebar: function(){
            this.$emit("showSidebar", true);
        },

        listenToServer : function(){

            // Solar Listener
            socket.on('solarCurrent', (data)=>{
                this.deviceName = data;
                this.solarCurrent = data;
                console.log("Device Name = "+data);
            });

            socket.on('solarPower', (data)=>{ 
                this.deviceLocation = data;
                this.solarPower = data;
                console.log("Device Location = "+data);
                });
            
            socket.on('solarVoltage', (data)=>{ 
                this.deviceType = data;
                this.solarVoltage = data
                console.log("Device Type = "+data);
                });
            
            socket.on('solarAnnual', (data)=>{
                this.solarAnnual = data;
                console.log("Solar Annual = "+data);
            });

            socket.on('solarDaily', (data)=>{
                this.solarDaily = data;
                console.log("Solar Daily = "+data);
            });

            socket.on('solarMonthly', (data)=>{
                this.solarMonthly = data;
                console.log("Solar Monthly = "+data);
            });

            socket.on('solarAnnual', (data)=>{
                this.solarAnnual = data;
                console.log("Solar Annual = "+data);
            });

            socket.on('solarTotal', (data)=>{
                this.solarTotal = data;
                console.log("Solar total = "+data);
            });

            //Load Listener

            socket.on('loadCurrent', (data)=>{
                            this.loadCurrent = data;
                            console.log("Load Current = "+data);
                });

                socket.on('loadVoltage', (data)=>{
                            this.loadVoltage = data;
                            console.log("Load Voltage = "+data);
                });

                socket.on('loadPower', (data)=>{
                            this.loadPower = data;
                            console.log("Load Power = "+data);
                });
                socket.on('loadDaily', (data)=>{
                            this.loadDaily = data;
                            console.log("Load Daily = "+data);
                });
                socket.on('loadMonthly', (data)=>{
                            this.loadMonthly = data;
                            console.log("Load Monthly = "+data);
                });

                socket.on('loadAnnual', (data)=>{
                            this.loadAnnual = data;
                            console.log("Load Annual = "+data);
                });

                socket.on('loadTotal', (data)=>{
                            this.loadTotal = data;
                            console.log("Load Total = "+data);
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
        

        DeviceInfo,
        PowerGeneration,
        Consumption,
        BatteryLevel,
        OperationalTime,
        Weather,
        Warning,
        SolarLoad,
        Battery
    },
  
    

    mounted: function(){
        
        this.listenToServer()
       
    }
   
   
}



</script>

<style>

</style>