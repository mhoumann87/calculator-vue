<template>
  <div class="calculator">
    <div class="display">{{current || 0}}</div>
    <div class="btn">C</div>
    <div class="btn">+/-</div>
    <div class="btn">%</div>
    <div class="btn operator">&divide;</div>
    <div class="btn">7</div>
    <div class="btn">8</div>
    <div class="btn">9</div>
    <div class="btn operator">&times;</div>
    <div class="btn">4</div>
    <div class="btn">5</div>
    <div class="btn">6</div>
    <div class="btn operator">-</div>
    <div class="btn">1</div>
    <div class="btn">2</div>
    <div class="btn">3</div>
    <div class="btn operator">+</div>
    <div class="zero btn">0</div>
    <div class="btn">.</div>
    <div class="btn operator">=</div>
    </div>
</template>

<script>
export default {
  data() {
    return {
      current: '',
    };
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
  color: #fff;
  height: 75px;
  font-size: 4.5rem;
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
