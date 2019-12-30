<template>
  <div id="display">
      <div id="displayText">{{displayValue}}</div>
  </div>
</template>

<script>
export default {
  name: 'display',
  props: {
      displayValue: String
  }

}
</script>

<style>
#display {
  width: 90%;
  margin-left: 5%;
  margin-top: 5%;
  border: 2px solid black;
  border-radius: 5px;
  height: 20%;
}

#displayText{
    font-family: Lato, Verdana, sans-serif;
    font-size: 6em;
    text-align: right;
    margin-bottom: 0px;
}
</style>
