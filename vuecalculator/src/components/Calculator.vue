<template>
  <div id="calcWrapper">
      <Display v-bind:displayValue=dispValue></Display>
      <div id="keypad">
      <Button   v-for="b in buttons" 
                v-bind:key="b.id" 
                v-bind:bValues="b"
                v-on:handle-press="handlePress" 
                v-bind:style="b.id === 1 ? bStyleObjectLarge:  bStyleObjectRegular">
      </Button>
      </div>
  </div>
</template>

<script>
import Display from './Display.vue'
import Button from './Button.vue'

export default {
  data: function () {
      return {
          dispValue: "0",
          prevValue: "0",
          prevOp: "=",
          bStyleObjectRegular:{
              width: '16%'
          },
          bStyleObjectLarge:{
              width: '39%',
          },
          buttons:[
              {
                  id: 1,
                  name: "AC"
              },
              {
                  id: 2,
                  name: "C"
              },
              {
                  id: 3,
                  name: "/"
              },
              {
                  id: 4,
                  name: "7"
              },
              {
                  id: 5,
                  name: "8"
              },
              {
                  id: 6,
                  name: "9"
              },
              {
                  id: 7,
                  name: "x"
              },
              {
                  id: 8,
                  name: "4"
              },
              {
                  id: 9,
                  name: "5"
              },
              {
                  id: 10,
                  name: "6"
              },
              {
                  id: 11,
                  name: "+"
              },
              {
                  id: 12,
                  name: "1"
              },
              {
                  id: 13,
                  name: "2"
              },
              {
                  id: 14,
                  name: "3"
              },
              {
                  id: 15,
                  name: "-"
              },
              {
                  id: 16,
                  name: "0"
              },
              {
                  id: 17,
                  name: "."
              },
              {
                  id: 18,
                  name: "+/-"
              },
              {
                  id: 19,
                  name: "="
              }
          ]
      }
  },
  components:{
      Display,
      Button
  },
  methods: {
      handlePress: function (event){
          switch (event.textContent){
              case "AC": this.clearAll();
                break;
              case "C": this.clearDisplay();
                break;
              case "0":
              case "1":
              case "2":
              case "3":
              case "4":
              case "5":
              case "6":
              case "7":
              case "8":
              case "9": this.numberPressed(event.textContent);
              break; 
              case "+": this.computeOp("+");
                break;
              case "-": this.computeOp("-");
                break;
              case "/": this.computeOp("/");
                break;
              case "x": this.computeOp("x");
                break;
              case "=": this.computeEqual(this.prevValue, this.dispValue, this.prevOp);
                break;
              default:

          }
      },
      numberPressed: function(number){
          if (this.dispValue === "0"){
              this.dispValue = number;
          }
          else {
              this.dispValue += number;
          }
          
      },
      computePlus: function (){
          this.dispValue = this.computeOps(this.prevValue, this.dispValue, "+")
      },
      computeSub: function (){
          this.dispValue = this.computeOps(this.prevValue, this.dispValue, "-")
      },
      computeDiv: function (){
          this.dispValue = this.computeOps(this.prevValue, this.dispValue, "/")
      },
      computeMult: function (){
          this.dispValue = this.computeOps(this.prevValue, this.dispValue, "x")
      },
      computeOp: function (op){
          this.computeEqual(this.prevValue, this.dispValue, this.prevOp);
          this.prevValue = this.dispValue;
          this.dispValue = "0";
          this.prevOp = op;
      },
      computeEqual: function(op1, op2, op){
          let op1_num = parseInt(op1);
          let op2_num = parseInt(op2);
          let result = 0;
          if (op === "+"){
              result = op1_num + op2_num;
          }
          else if (op === "-"){
              result = op1_num - op2_num;
          }
          else if (op === "x"){
              result = op1_num * op2_num;
          }
          else if (op === "/"){
              result = Math.floor(op1_num / op2_num);
          }
          else{
              result = op2_num;
          }
          this.dispValue = result.toString();
          this.prevValue = "0";
          this.prevOp = "=";

      },
      clearDisplay: function (){
          this.dispValue = "0";
      },
      clearAll: function (){
          this.clearDisplay();
          this.prevValue = "0";
          this.prevOp = "=";
      }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style>
#calcWrapper {
  width: 30%;
  margin: auto;
  border: 2px dashed gray;
  border-radius: 5px;
  height: 600px;
  overflow: hidden;
}

#keypad{
    margin-top: 10%;
    height: 70%;
    border: 2px dashed green;
    margin-bottom: 0px;
}
</style>
