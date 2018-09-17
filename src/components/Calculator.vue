<template>

<!-- Basic layout for the calculator with the vue bindings needed for the functionallity -->
  <div class="calculator">
    <!-- In display show the digits entered, if empty show a "0" -->
    <div class="display">{{current || 0}}</div>
    <div @click="clear" class="btn">C</div>
    <div @click="sign" class="btn">+/-</div>
    <div @click="percent" class="btn">%</div>
    <div @click="divide" class="btn operator">&divide;</div>
    <div @click="num('7')" class="btn">7</div>
    <div @click="num('8')" class="btn">8</div>
    <div @click="num('9')" class="btn">9</div>
    <div @click="times" class="btn operator">&times;</div>
    <div @click="num('4')" class="btn">4</div>
    <div @click="num('5')" class="btn">5</div>
    <div @click="num('6')" class="btn">6</div>
    <div @click="sub" class="btn operator">-</div>
    <div @click="num('1')" class="btn">1</div>
    <div @click="num('2')" class="btn">2</div>
    <div @click="num('3')" class="btn">3</div>
    <div @click="add" class="btn operator">+</div>
    <div @click="zero" class="zero btn">0</div>
    <div @click="dot" class="btn">.</div>
    <div @click="equals" class="btn operator">=</div>
    </div>
</template>

<script>
export default {
  // At start set current to an empty string
  data() {
    return {
      current: '',
      previous: null,
      operator: null,
      operatorClicked: false,
    };
  },
  methods: {
    // clear the display, replace with an empty string
    clear() {
      this.current = '';
    },
    // reverse value of number, if posive make negative or make negative pasitive
    sign() {
      if (this.current.charAt(0) === '0' || this.current === '') {
        this.current = this.current;
      } else if (this.current !== '') {
        this.current =
            this.current.charAt(0) === '-'
              ? this.current.slice(1)
              : `-${this.current}`;
      }
    },
    // Calculate with percent numbers
    percent() {
      this.current = `${parseFloat(this.current) / 100}`;
    },
    // Add a digit to the display
    append(number) {
      if (this.operatorClicked) {
        this.current = '';
        this.operatorClicked = false;
      }
      this.current = `${this.current}${number}`;
    },
    // Check to see if number should be appended or added
    num(num) {
      if (this.current === '' || this.current.charAt(0) === 0) {
        this.current = num;
      } else {
        this.append(num);
      }
    },
    zero() {
      if (this.current === '' || this.current.charAt(0) === 0) {
        this.current = '';
      } else {
        this.append('0');
      }
    },

    // If the dot is pushed, add it to the display if it doesn't allready exists
    dot() {
      if (this.current.indexOf('.') === -1) {
        this.append('.');
      }
    },
    setPrevious() {
      this.previous = this.current;
      this.operatorClicked = true;
    },
    divide() {
      this.operator = (a, b) => b / a;
      this.setPrevious();
    },
    times() {
      this.operator = (a, b) => a * b;
      this.setPrevious();
    },
    sub() {
      this.operator = (a, b) => b - a;
      this.setPrevious();
    },
    add() {
      this.operator = (a, b) => a + b;
      this.setPrevious();
    },
    equals() {
      this.current = `${this.operator(
        parseFloat(this.current),
        parseFloat(this.previous),
      )}`;
      this.previous = null;
    },
  },
};
</script>


<style scoped>
.calculator {
  width: 400px;
  margin: 0 auto;
  border: 1px solid #333;
  font-size: 2.3rem;
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  grid-auto-rows: minmax(50px, auto);
}

.display {
  font-family: "Orbitron", sans-serif;
  color: #fff;
  height: 75px;
  font-size: 3rem;
  grid-column: 1 / 5;
  background-color: darkgray;
  text-align: right;
  padding: 10px;
}

.zero {
  grid-column: 1 / 3;
}

.btn {
  border-collapse: collapse;
  background-color: #eee;
  border: 1px solid #333;
}

.operator {
  color: #fff;
  background-color: orange;
}
</style>
