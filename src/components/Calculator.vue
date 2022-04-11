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
            <td class="lastCol">/</td>
          </tr>
          <tr>
            <td @click="getNumber('7')">7</td>
            <td @click="getNumber('8')">8</td>
            <td @click="getNumber('9')">9</td>
            <td class="lastCol">&#x0078;</td>
          </tr>
          <tr>
            <td @click="getNumber('4')">4</td>
            <td @click="getNumber('5')">5</td>
            <td @click="getNumber('6')">6</td>
            <td class="lastCol">-</td>
          </tr>
          <tr>
            <td @click="getNumber('1')">1</td>
            <td @click="getNumber('2')">2</td>
            <td @click="getNumber('3')">3</td>
            <td class="lastCol">+</td>
          </tr>
          <tr>
            <td colspan="2" @click="getNumber('0')">0</td>
            <td @click="addDot">.</td>
            <td class="lastCol">=</td>
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
      output: "222",
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
      this.output += numInString;
    },
    addDot() {
      if (this.output.indexOf('.') === -1) {
        this.output += '.';
      }
    }
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
.lastCol:active {
  background-color: #333;
  color: #fff;
}
</style>
