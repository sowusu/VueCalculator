<template>
  <div id="vuebutton">
      <button class="calc-button" 
              v-on:click=buttonPressed
              v-bind:class="{opButton: bValues.isOp, regButton: bValues.isReg}">
               {{bValues.name}}
      </button>
  </div>
</template>

<script>
export default {
  name: 'vuebutton',
  props: {
      bValues: Object
  },
  methods:{
      buttonPressed: function(event){
          this.$emit('handle-press', event.target)
      }
  }

}
</script>

<style>
#vuebutton {
  margin: 0px;
  height: 100px;
  box-sizing: border-box;
  float: left;

}

.calc-button{
    width: 100%;
    height: 100%;
    font-family: Lato, Verdana, sans-serif;
    text-align: center;
    font-size: 30px;
    color: white;
}

.opButton{
    background-color: #38908f;
}
.regButton{
    background-color: #676767;
}
</style>
