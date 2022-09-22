<template>
<div id="app">
  <div class="screen">
    <input v-model.number="operand1" />
    {{ item }}
    <input v-model.number="operand2" />
    =
    {{ result }}

  </div>
  <div class="keyboard">
    <button v-for="(item, index) in operators"
            v-bind:key="index"
        @click="getResult(item)">{{ item }}</button>
<!--    <button @click = "operator = '-'">-</button>-->
<!--    <button @click = "operator = '*'">*</button>-->
<!--    <button @click = "operator = '/'">/</button>-->
<!--    <button @click = "operator = '^'">^</button>-->
<!--    <button @click = "operator = '%'">%</button>-->
<!--    <button @click = "getResult">=</button>-->
  </div>
  <input type="checkbox" id="checkbox" v-model="checked">
  <label for="checkbox">Открыть экранную клавиатуру</label>
  <div  v-show="checked">
    <button v-for="(num, index) in numbers"
            v-bind:key="index"
            @click="input(num)">{{ num }}
    </button>
    <button @click="reset">R</button>
    <div>
    <input type="radio" id="one" value="1"  v-model="picked">
    <label for="one">Один</label>
    <br>
    <input type="radio" id="two" value="2" v-model="picked">
    <label for="two">Два</label>
    </div>
  </div>
</div>
</template>

<script>


export default {
  name: 'App',
  data() {
    return {
      operand1: " ",
      operand2: " ",
      result: 0,
      checked: false ,
      operators: ['+', '-', '*', '/', '^', '%'],
      numbers: [0,1,2,3,4,5,6,7,8,9],
      test: " ",
      picked: "1",
    }
  },
  methods: {

    getResult(operator) {
      switch (operator) {
        case '+':
          this.result = Number(this.operand1) + Number(this.operand2)
              break;
        case '-':
          this.result = this.operand1 - this.operand2
          break;
        case '*':
          this.result = this.operand1 * this.operand2
          break;
        case '/':
          this.result = this.operand1 / this.operand2
          break;
        case '^':
          this.result = Math.pow(this.operand1, this.operand2)
          break;
        case '%':
          this.result = Math.floor(this.operand1 % this.operand2)
          break;

          default:
            this.result = "Error"
              break;
      }
    },
    input: function(char) {
      if (this.picked === "1") {
        this.operand1 = this.operand1.toString();
        this.operand1+=char;
      } else {
        this.operand2 = this.operand2.toString();
        this.operand2+=char;
      }

    },
    reset() {
      this.operand1 = " ";
      this.operand2 = " ";
      this.result = 0;
    }

  }


}
</script>

<style lang="css">
 #app {

  text-align: center;
  margin-top: 60px;
}
</style>
