<template>
  <div class="hello">
    <h1>{{ msg }}</h1>

    <div class="col-md-4 m-3">
      <table class="table table-bordered">
        <tbody>
          <tr class="output">
            <td colspan="4">
              {{ output || 0 }}
            </td>
          </tr>
          <tr>
            <td @click="clearField">C</td>
            <td @click="turnNegative">+/-</td>
            <td @click="percent">%</td>
            <td class="lastCol" @click="process('divide')">/</td>
          </tr>
          <tr>
            <td @click="getNumber('7')">7</td>
            <td @click="getNumber('8')">8</td>
            <td @click="getNumber('9')">9</td>
            <td class="lastCol" @click="process('multiply')">&#x0078;</td>
          </tr>
          <tr>
            <td @click="getNumber('4')">4</td>
            <td @click="getNumber('5')">5</td>
            <td @click="getNumber('6')">6</td>
            <td class="lastCol" @click="process('minus')">-</td>
          </tr>
          <tr>
            <td @click="getNumber('1')">1</td>
            <td @click="getNumber('2')">2</td>
            <td @click="getNumber('3')">3</td>
            <td class="lastCol" @click="process('plus')">+</td>
          </tr>
          <tr>
            <td colspan="2" @click="getNumber('0')">0</td>
            <td @click="addDot">.</td>
            <td class="lastCol" @click="equal">=</td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    msg: String,
  },
  data() {
    return {
      output: "",
      prev: null,
      operationFired: false,
      hasOp: false,
    };
  },
  methods: {
    clearField() {
      this.output = "";
    },
    turnNegative() {
      this.output = -(+this.output) + '';
    },
    percent() {
      // output强转为Number.会产生bug吗？
      this.output /= 100;
    },
    getNumber(numInString) {
      if (this.operationFired) {
        this.output = '';
        this.operationFired = false;
      }
      this.output += numInString;
    },
    addDot() {
      if (this.output.indexOf('.') === -1) {
        this.output += '.';
      }
    },
    process(op) {
      switch (op) {
        case 'plus':
          this.operation = (a, b) => {
            return +a + +b;
          }
          break;
        case 'minus':
          this.operation = (a, b) => {
            return +a - +b;
          }
          break;
        case 'multiply':
          this.operation = (a, b) => {
            return +a * +b;
          }
          break;
        case 'divide':
          this.operation = (a, b) => {
            return +a / +b;
          }
          break;
        default:
          console.log('wtf');
          break;
      }
      
      this.prev = this.output;
      this.operationFired = true;
      this.hasOp = true;
    },
    equal() {
      if (this.hasOp) {
        this.output = this.operation(+this.prev, +this.output);
        this.hasOp = false;
      }
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
.output {
  background-color: #333;
  color: #fff;
}
.lastCol {
  background-color: orange;
  color: #fff;
}
td:active {
  background-color: #333;
  color: #fff;
}
</style>
