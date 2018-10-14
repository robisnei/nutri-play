<!--<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png">
    <HelloWorld msg="Welcome to Your Vue.js App"/>
  </div>
</template>-->
<template>
  <div id="quiz">
    <quiz url="https://api.myjson.com/bins/ahn1p">

      <div slot="intro" slot-scope="props">
        This is my custom quiz header for {{props.title}}.
      </div>

      <div slot="results" slot-scope="props">
        <h1>WOWOWOW!</h1>
          You got {{props.correct}} right out of
          {{props.length}} questions.
        Your percentage is {{props.perc}}%.
      </div>

    </quiz>
  </div>
</template>

<script>
import Quiz from './components/Quiz.vue'

export default {
  name: 'app',
  components: {
    Quiz
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
