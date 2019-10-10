<template>

    <div class="row">

        <!-- <DeviceInfo
            title="Device Name"
            icon="icon-lg pe-7f-comment"
            bgclass="bg-flat-color-1"
            :counter="solarAnnual"
          
        >
        </DeviceInfo> -->
        
        <DeviceInfo
            icon="icon-lg pe-7f-info"
            bgclass="bg-flat-color-1"
            :counter="deviceType"
            title="Device Type"
        >
        </DeviceInfo>

        <!-- <DeviceInfo
            icon="icon-lg pe-7f-map-marker"
            bgclass="bg-flat-color-1"
            :counter="deviceLocation"
            title="Device Location"
        >
        </DeviceInfo> -->
        

        <!-- <RealTime title="Real time"/> -->
        <!-- <PowerGeneration /> -->
        <!-- <Consumption />
        <BatteryLevel/>
        <Weather />
        <OperationalTime />
        <Warning /> -->

        <!-- <solarload 
            :title="solarTitle" 
            :power="solarPower" 
            :current="solarCurrent"
            :voltage="solarVoltage"
            :daily="solarDaily"
            :monthly="solarMonthly"
            :annual="solarAnnual"></solarload> -->
            
        <!-- <solarload 
            title="Load"
            :power="loadPower" 
            :current="loadCurrent"
            :voltage="loadVoltage"
            :daily="loadDaily"
            :monthly="loadMonthly"
            :annual="loadAnnual"></solarload> -->

    </div>

</template>

<!-- <script src="/socket.io/socket.io.js"></script> -->
<script>

import DeviceInfo from './dashboard/dashboardcomponent/DeviceInfo.vue';
/*import PowerGeneration from './dashboard/dashboardcomponent/PowerGeneration.vue';
import Consumption from './dashboard/dashboardcomponent/Consumption.vue';
import BatteryLevel from './dashboard/dashboardcomponent/BatteryLevel.vue';
import OperationalTime from './dashboard/dashboardcomponent/OperationalTime.vue';
import Weather from './dashboard/dashboardcomponent/Weather.vue';
import Warning from './dashboard/dashboardcomponent/Warning.vue';*/
import Vue from 'vue';
import solarload from './dashboard/dashboardcomponent/solarload.vue';
import VueSocketIOExt from 'vue-socket.io-extended';
import io from 'socket.io-client';
import axios from 'axios';


const socketSolar = io('http://localhost:19997');

export default{
  
    name: 'dashboard',
    props: ['requestType'],

    data(){
        return{
            solarTitle :"",
            solarPower : "",
            solarCurrent : "",
            solarVoltage : "",
            solarAnnual : "",
            solarDaily : "",
            solarMonthly : "",
            deviceLocation : "",
            deviceType : "",

           /* loadPower : "",
            loadCurrent : "",
            loadVoltage : "",
            loadAnnual : "",
            loadDaily : "",
            loadMonthly : ""*/
        }
    },
    components: {
        
        DeviceInfo,
        /*PowerGeneration,
        Consumption,
        BatteryLevel,
        OperationalTime,
        Weather,
        Warning, */
        solarload
    },
   
    methods: {
    
        requestDeviceType: function () {
        
            var urlWrapper ="http://127.0.0.1:19998/deviceInformation/deviceType"
       
                axios.get(urlWrapper)
                .then(({data}) => {
                    console.log("Sample Data --> "+data);
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
            
                socketSolar.on('connect', function(){
                        console.log("Socket Solar is connected --> Connection Status --> "+socketSolar.disconnected);

                });
                
                socketSolar.on('disconnect', function(){
                        console.log("Socket Solar is disconnected --> Connection Status --> "+socketSolar.disconnected);
                        //console.log("Socket Solar is disconnected");
                        socketSolar.open();
                });

                //Listener for solar
                socketSolar.on('solarCurrent', function(data){
                            this.solarCurrent = data;
                            console.log("Solar Current = "+this.solarCurrent);
                });

                socketSolar.on('solarPower', function(data){
                            this.solarPower = data;
                            console.log("Solar Power = "+data);
                });

                socketSolar.on('solarVoltage', function(data){
                            this.solarVoltage = data;
                            console.log("Solar Voltage = "+data);
                });
                socketSolar.on('solarAnnual', function(data){
                            this.solarAnnual = data;
                            console.log("Solar Annual = "+data);
                });
                socketSolar.on('solarDaily', function(data){
                            this.solarDaily = data;
                            console.log("Solar Daily = "+data);
                });

                socketSolar.on('solarMonthly', function(data){
                            this.solarVoltage = data;
                            console.log("Solar Monthly = "+data);
                });

                //Listener for Battery

                socketSolar.on('battLevel', function(data){
                        
                });

                socketSolar.on('battCurrent', function(data){
            
                });

                socketSolar.on('battVoltage', function(data){
            
                });
                socketSolar.on('battPower', function(data){
            
                });
                
                socketSolar.on('charging', function(data){
            
                });

                socketSolar.on('discharging', function(data){
                
                });

                //Listener for Load

                socketSolar.on('loadCurrent', function(data){
                            this.loadCurrent = data;
                            console.log("Load Current = "+data);
                });

                socketSolar.on('loadVoltage', function(data){
                            this.loadVoltage = data;
                            console.log("Load Voltage = "+data);
                });

                socketSolar.on('loadPower', function(data){
                            this.loadPower = data;
                            console.log("Load Power = "+data);
                });
                socketSolar.on('loadDaily', function(data){
                            this.loadDaily = data;
                            console.log("Load Daily = "+data);
                });
                socketSolar.on('loadMonthly', function(data){
                            this.loadMonthly = data;
                            console.log("Load Monthly = "+data);
                });

                socketSolar.on('loadAnnual', function(data){
                            this.loadAnnual = data;
                            console.log("Load Annual = "+data);
                });

                socketSolar.on('loadTotal', function(data){
                            this.loadTotal = data;
                            console.log("loadTotal = "+data);
                });
        

         

        }

    },

    created(){
        
    },

   

    mounted: function(){
        this.solarTitle = "Solar", 
        this.listenToServer();
        this.requestDeviceType();

    }


}



</script>

<style>

</style>