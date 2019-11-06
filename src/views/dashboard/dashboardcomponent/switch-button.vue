<template id="switch-button">
  <div class="switch-button-control">
      <div class="switch-button-label">
        <slot><small>Off</small></slot>
     </div>
    <div class="switch-button" :class="{ enabled: isEnabled }" @click="toggle" :style="{'--color': color}">
      <div class="button"></div>
    </div>
    <div class="switch-button-label">
      <slot><small>On</small></slot>
    </div>
  </div>
</template>


<script>
    export default{
       
        name: 'switch-button',
       
        template: "#switch-button",
        
        model: {
                 prop: "isEnabled",
                 event: "toggle"
         },
        props: {
            isEnabled: Boolean,
            color: {
            type: String,
            required: false,
            default: "#4D4D4D"
            }
        },
        methods: {
            toggle: function() {
            this.$emit("toggle", !this.isEnabled);
            }
        }
    }
</script> 
