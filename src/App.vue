<template>
  <div class="app">
    <div class="app__buttons">
      <button class="app__button">Запустить вычисление через threader</button>
      <button class="app__button" @click="startRegular(test)">Запустить обычное вычисление</button>
    </div>
    <div class="app__result">Результат вычислений: {{ test }}</div>
    <div class="app__render" :style="{color: colors[colorIndex], marginLeft: `${(colorIndex/colors.length)*20}%`}">Я меняю цвет</div>
  </div>
</template>

<script>
export default {
  name: 'App',
  data: () => ({
    test: 2,
    iterationNum: 10000,
    colorIndex: 0,
    colors: ["yellow", "green", "blue", "black", "orange", "purple", "red"]
  }),
  methods: {
    startRegular(num = 2) {
      let n = num;
      for (let i = 0; i < this.iterationNum; i++) {
        for (let j = 0; j < this.iterationNum; j++) {
          n = n + (2*i) - j;
        }
      }
      this.test = n;
    },
    changeColor() {
      if (this.colors[this.colorIndex+1]) this.colorIndex++;
      else this.colorIndex = 0;
      setTimeout(() => this.changeColor(), 500);
    },
  },
  mounted() {
    this.changeColor();
  }
}
</script>
<style>
.app__buttons {
  display: flex;
  flex-direction: row;
  margin-top: 30px;
}
.app__button {
  padding: 10px 20px;
  font-size: 16px;
  cursor: pointer;
  margin: 0 10px;
}
.app__render {
  transition: .3s;
  font-weight: 700;
  font-size: 25px;
}
</style>
