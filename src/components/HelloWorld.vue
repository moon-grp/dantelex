/* eslint-disable prettier/prettier */ /* eslint-disable prettier/prettier */
<template>
  <div class="cal">
    <div class="dis ">{{ display || 0 }}</div>
    <div class="btns num">history</div>
    <div class="btns num"><i class="fas fa-ruler-horizontal"></i></div>
    <div class="btns num"><i class="fas fa-calculator"></i></div>
    <div class="btns num" @click="clear"><i class="fas fa-backspace"></i></div>
    <div class="btns num" style="color:red" @click="clear">C</div>
    <div class="op btns num">`()`</div>
    <div class="op btns num" @click="percentage">%</div>
    <div class="op btns num" @click="divide">/</div>
    <div class="btns num" @click="pick('7')">7</div>
    <div class="btns num" @click="pick('8')">8</div>
    <div class="btns num" @click="pick('9')">9</div>
    <div class="op btns num" @click="mult">x</div>
    <div class="btns num" @click="pick('4')">4</div>
    <div class="btns num" @click="pick('5')">5</div>
    <div class="btns num" @click="pick('6')">6</div>
    <div class="op btns num" @click="minus">-</div>
    <div class="btns num" @click="pick('1')">1</div>
    <div class="btns num" @click="pick('2')">2</div>
    <div class="btns num" @click="pick('3')">3</div>
    <div class="op btns num" @click="add">+</div>
    <div class="btns num" @click="negative">+/-</div>
    <div class="btns num" @click="pick('0')">0</div>
    <div class="btns num" @click="dotb">.</div>
    <div class="eq num" @click="equalsto">=</div>
  </div>
</template>

<script>
export default {
  name: "HelloWorld",
  data() {
    return {
      display: "",
      ops: null,
      previous: null,
      opsclick: false,
    };
  },
  methods: {
    setp() {
      this.previous = this.display;
      this.opsclick = true;
    },
    clear() {
      this.display = "";
    },
    negative() {
      this.display =
        this.display.charAt(0) === "-"
          ? this.display.slice(1)
          : `-${this.display}`;
    },
    percentage() {
      this.display = `${parseFloat(this.display) / 100}`;
    },
    pick(num) {
      if (this.opsclick) {
        this.display = "";
        this.opsclick = false;
      }
      this.display = `${this.display}${num}`;
    },
    dotb() {
      if (this.display.indexOf(".") === -1) {
        this.pick(".");
      }
    },
    mult() {
      this.ops = (a, b) => a * b;
      this.setp();
    },
    divide() {
      this.ops = (a, b) => a / b;
      this.setp();
    },
    minus() {
      this.ops = (a, b) => a - b;
      this.setp();
    },
    add() {
      this.ops = (a, b) => a + b;
      this.setp();
    },
    equalsto() {
      this.display = `${this.ops(
        parseFloat(this.display),
        parseFloat(this.previous)
      )}`;
      this.previous = null;
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.cal {
  width: 350px;
  margin: 0 auto;
  grid-template-columns: repeat(4, 1fr);
  grid-auto-rows: minmax(50px, auto);
  display: grid;
  font-size: 20px;
}
.dis {
  grid-column: 1 / 5;
  grid-row: 1/6;
  margin-top: 5px;
  background-color:ghostwhite;
  border: 0.5px solid #808080;
  padding-top: 50%;
  padding-left: 80%;
}
.num {
  padding-top: 10px;
}
.eq {
  background: skyblue;
  color: white;
}
.op {
  color: skyblue;
}
.btns {
  background-color: ghostwhite;
  border: 0.5px solid #808080;
}
</style>
