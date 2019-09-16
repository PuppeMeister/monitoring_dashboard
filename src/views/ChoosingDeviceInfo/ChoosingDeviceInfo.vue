<template>
    <!-- <div class="col-md-6 col-lg-3"> -->
    <div class="col-md-2">
        <div
            class="card text-white"
            :class="bgclass"
        >

            <div class="card-body" v-on:click.capture="showGoToDashboard">
                
                <div class="card-left pt-1 float-left">
                    <h4 class="mb-0 fw-r">
                        <div>
                            <span class="badge badge-secondary">{{title}}</span>
                        </div>

                    </h4>
                    <p class="text-light mt-1 m-0">
                         <i
                        class="icon fade-5 icon-sm pe-7f-map-marker"
                        ></i>
                        {{counter}}</p>
                </div>

                <div class="card-right float-right text-right">
                    <i
                        class="icon fade-5"
                        :class="icon"
                    ></i>
                </div>

            </div>
        </div>
    </div>
</template>

<script>
export default{
    name: 'info-icon-box',
    props: ['icon', 'symbol', 'counter', 'title', 'bgclass', 'deviceID'],
  
    methods: {
        showGoToDashboard: function(){
            //this.$emit("showSidebar");
            //this.$router.push({name: 'deviceDashboard', params: { userId: '123' }})
            console.log("Device ID", this.deviceID)
            this.$router.push({name: 'deviceDashboard', params: {requestType: this.deviceID}})
            //this.$router.push({name: 'deviceDashboard', params: "this.deviceID"})

        }
    }
}
</script>
