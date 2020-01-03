<script src="https://cdnjs.cloudflare.com/ajax/libs/velocity/2.0.5/velocity.ui.min.js"></script>

<template>
  <div id="display">
      <div id="displayText">
        <div id = "leftOf">{{displayValue}}</div>
        <div id = "blinker"> <Blinker /> </div>
      </div>
      <div id="subText">{{subDisplayValue}}</div>
  </div>
</template>

<script>
import Blinker from "./Blinker.vue";

export default {
  name: 'display',
  props: {
      displayValue: String,
      subDisplayValue: String
  },
  components:{
    Blinker
  },
  created:function(){
    this.onLoady()
  },
  methods: {
    onLoady: function() {
      alert("loaded")
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
    font-size: 3em;
    text-align: right;
    margin-bottom: 0px;
    border: 2px solid orange;
    overflow:hidden;
    text-overflow: ellipsis;
}
#displayText{
    display: flex;
    flex-direction: row;
    height: 100px;
}

#subText{
    height: 100px;
}
</style>
