<template>
  <div id="quiz">
    <quiz url="https://api.myjson.com/bins/drsmw">

      <div slot="intro" slot-scope="props">
        Esse quiz tem o tema {{props.title}}.
      </div>

      <div slot="results" slot-scope="props">
          Você acertou {{props.correct}} de
          {{props.length}} questões.
        Sua porcentagem de acertos foi {{props.perc}}%.
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
  #quiz {
    font-family: 'Avenir', Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
    margin-top: 60px;
  }
</style>
