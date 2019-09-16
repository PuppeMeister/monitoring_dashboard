<template>

    <div class="row">

        <DeviceInfo
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
        </DeviceInfo>
        

        <!-- <RealTime title="Real time"/> -->
        <PowerGeneration />
        <Consumption />
        <BatteryLevel/>
        <Weather />
        <OperationalTime />
        <Warning />

    </div>

</template>

<script>

import DeviceInfo from './dashboard/dashboardcomponent/DeviceInfo.vue';
import PowerGeneration from './dashboard/dashboardcomponent/PowerGeneration.vue';
import Consumption from './dashboard/dashboardcomponent/Consumption.vue';
import BatteryLevel from './dashboard/dashboardcomponent/BatteryLevel.vue';
import OperationalTime from './dashboard/dashboardcomponent/OperationalTime.vue';
import Weather from './dashboard/dashboardcomponent/Weather.vue';
import Warning from './dashboard/dashboardcomponent/Warning.vue';

import axios from 'axios';

export default{
    name: 'dashboard',
    props: ['requestType'],

    data(){
        return{
            deviceName: "", deviceType: "", deviceLocation: ""
		
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
        }

    },

    
    components: {
        

        DeviceInfo,
        PowerGeneration,
        Consumption,
        BatteryLevel,
        OperationalTime,
        Weather,
        Warning
    },

    mounted: function(){
        this.showSidebar()
        this.requestDeviceType()
        this.requestDeviceName()
        this.requestDeviceLocation()

        /*this.interval = setInterval(function () {
                this.reloadMyFunctions()
                console.log("Refresh the Dashboard")
        }.bind(this), 30000)*/
    }
    //},

    /*beforeDestroy: function(){  
            clearInterval(this.interval);
    }*/
   
}


</script>

<style>

</style>