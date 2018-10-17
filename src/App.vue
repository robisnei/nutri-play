<template>
  <b-container>
      <!-- <b-navbar variant="faded" type="light">
        <b-navbar-brand href="#">
          <img src="../assets/logo" alt="BV">
        </b-navbar-brand>
      </b-navbar> -->
    <div id="quiz">
      <quiz url="https://api.myjson.com/bins/drsmw">

        <div slot="intro" slot-scope="props" class="text-secondary">
          <h5 class="text-secondary ">Esse quiz tem o tema {{props.title}}</h5>
          <p>
            <b>Feito pelos aluninhos da UNIP</b>
          </p>
        </div>

        <div slot="results" slot-scope="props">
            Você acertou {{props.correct}} de
            {{props.length}} questões.
          Sua porcentagem de acertos foi {{props.perc}}%
        </div>
        
      </quiz>
    </div>
  </b-container>
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
