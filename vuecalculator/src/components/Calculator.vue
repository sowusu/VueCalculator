<template>
  <div id="calcWrapper">
      <Display v-bind:displayValue=dispValue v-bind:subDisplayValue=subDispValue></Display>
      <Button   v-for="b in buttons" 
                v-bind:key="b.id" 
                v-bind:bValues="b"
                v-on:handle-press="handlePress" 
                v-bind:style="b.id === 1 ? bStyleObjectLarge:  bStyleObjectRegular">
      </Button>
  </div>
</template>

<script>
import Display from './Display.vue'
import Button from './Button.vue'

export default {
  data: function () {
      return {
          dispValue: "0",
          subDispValue: "_",
          prevValue: "0",
          prevOp: "=",
          bStyleObjectRegular:{
              width: '25%'
          },
          bStyleObjectLarge:{
              width: '50%',
          },
          buttons:[
              {
                  id: 1,
                  name: "AC",
                  isReg: true,
                  isOp: false
              },
              {
                  id: 2,
                  name: "C",
                  isReg: true,
                  isOp: false
              },
              {
                  id: 3,
                  name: "/",
                  isReg: false,
                  isOp: true
              },
              {
                  id: 4,
                  name: "7",
                  isReg: true,
                  isOp: false
              },
              {
                  id: 5,
                  name: "8",
                  isReg: true,
                  isOp: false
              },
              {
                  id: 6,
                  name: "9",
                  isReg: true,
                  isOp: false
              },
              {
                  id: 7,
                  name: "x",
                  isReg: false,
                  isOp: true
              },
              {
                  id: 8,
                  name: "4",
                  isReg: true,
                  isOp: false
              },
              {
                  id: 9,
                  name: "5",
                  isReg: true,
                  isOp: false
              },
              {
                  id: 10,
                  name: "6",
                  isReg: true,
                  isOp: false
              },
              {
                  id: 11,
                  name: "+",
                  isReg: false,
                  isOp: true
              },
              {
                  id: 12,
                  name: "1",
                  isReg: true,
                  isOp: false
              },
              {
                  id: 13,
                  name: "2",
                  isReg: true,
                  isOp: false
              },
              {
                  id: 14,
                  name: "3",
                  isReg: true,
                  isOp: false
              },
              {
                  id: 15,
                  name: "-",
                  isReg: false,
                  isOp: true
              },
              {
                  id: 16,
                  name: "0",
                  isReg: true,
                  isOp: false
              },
              {
                  id: 17,
                  name: ".",
                  isReg: true,
                  isOp: false
              },
              {
                  id: 18,
                  name: "\u00b1",
                  isReg: true,
                  isOp: false
              },
              {
                  id: 19,
                  name: "=",
                  isReg: false,
                  isOp: true
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
          var number = event.textContent.trim();
          switch (number){
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
              case "9": this.numberPressed(number);
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
              case ".": this.addPoint();
                  break;
              case "\u00b1": this.negateValue();
                  break;
              default:
                  alert("KEY ERROR: in default");
          }
      },
      negateValue: function(){
          if (this.dispValue != "0"){
              if (this.dispValue.indexOf("-") < 0){
              this.dispValue = "-" + this.dispValue;
            }
            else{
                this.dispValue = this.dispValue.substring(1);
            }
          }
          
      },
      addPoint: function() {
          if (this.dispValue.indexOf(".") < 0){
              this.dispValue += "."
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
          let op1_num = parseFloat(op1);
          let op2_num = parseFloat(op2);
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
              if (op2_num == 0){
                  alert("Math Error: Cannot divide by 0");
              }
              else{
                  result = op1_num / op2_num;
              }
              
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
  width: 40%;
  margin: auto;
  border: 15px solid black;
  border-radius: 5px;
  height: 700px;
  overflow: hidden;
  box-shadow: 5px 5px 5px #4b4b4c;
}
</style>
