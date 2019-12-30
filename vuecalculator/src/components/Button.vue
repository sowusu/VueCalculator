<template>
  <div id="vuebutton">
      <button class="calc-button" v-on:click=buttonPressed>{{bValues.name}}</button>
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
  margin-left: 7%;
  margin-top: 5%;
  border: 2px solid black;
  border-radius: 5px;
  height: 14%;
  padding: 0px;
  box-sizing: border-box;
  float: left

}

.calc-button{
    width: 100%;
    height: 100%;
    font-family: Lato, Verdana, sans-serif;
    text-align: center;
    font-size: 30px;
}
</style>
