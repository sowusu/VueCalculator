<script src="https://cdnjs.cloudflare.com/ajax/libs/velocity/2.0.5/velocity.ui.min.js"></script>

<template>
  <div id="display">
      <div id="displayText">
        <div id = "leftOf">{{displayValue}}</div>
        <div id = "blinker"> <Blinker /> </div>
      </div>
      <div id="subText"><p>{{subDisplayValue}}</p></div>
  </div>
</template>

<script>
import Blinker from "./Blinker.vue";
import Velocity from "velocity-animate";

export default {
  name: 'display',
  props: {
      displayValue: String,
      subDisplayValue: String
  },
  components:{
    Blinker
  },
  mounted:function(){
    this.onLoady()
  },
  methods: {
    onLoady: function() {
      Velocity(document.getElementById("blinker"), {opacity: 0}, {loop: true});
    }
  }
  

}
</script>

<style >

import 
#display {
  width: 100%;
  border-radius: 5px;
  height: 200px;
  float: right;
}

#leftOf{
  width: 99.75%;
}

#blinker{
  width: 1.00%;
}

#displayText,  #subText{
    font-family: Lato, Verdana, sans-serif;
    text-align: right;
    margin-bottom: 0px;
    overflow:hidden;
    text-overflow: ellipsis;
}
#displayText{
    display: flex;
    flex-direction: row;
    height: 100px;
    font-size: 3em;
}

#subText{
    height: 100px;
    font-size: 1.5em;
    color: #38908f;
    border: none;
    background-color: #f9f9f9;
}
</style>
