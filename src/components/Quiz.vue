<template>
  <div>
    <div v-if="introStage">
      <slot name="intro" :title="title">
      <h1>tema: {{title}}</h1>
      <p>
        Some kind of text here. Blah blah.
      </p>
      </slot>
      <button @click="startQuiz">Começar!</button>
    </div>

    <div v-if="questionStage">
      <question
                :question="questions[currentQuestion]"
                v-on:answer="handleAnswer"
                :question-number="currentQuestion+1"
      ></question>
    </div>

    <div v-if="resultsStage">
      <slot name="results" :length="questions.length" :perc="perc" :correct="correct">
      Você acertou {{correct}} de {{questions.length}} questões. Sua pontuação foi de {{perc}}%
      </slot>
      <button @click="startQuiz">Tentar Novamente</button>
    </div>
  </div>
</template>

<script>
  import rankJson from './rank.json'
  import Question from './Question.vue'
  export default {
    name: 'Quiz',
    components: {
       Question
    },
    props:['url'],
    data() {
      return {
        rank: rankJson,
        introStage:false,
        questionStage:false,
        resultsStage:false,
        title:'',
        questionsJson:[],
        questions:[],
        currentQuestion:0,
        answers:[],
        correct:0,
        perc:null
      }
    },
    created() {
      fetch(this.url)
      .then(res => res.json())
      .then(res => {
        this.title = res.title;
        this.questionsJson = res.questions;
        this.introStage = true;
      })
    },
    methods:{
      startQuiz() {
        this.generateRandanQuestions();
        this.introStage = false;
      },
      generateRandanQuestions() {
        var arr = [];
          while(arr.length < 12){
              var randomnumber = Math.floor(Math.random()*this.questionsJson.length-1) + 1;
              if(arr.indexOf(randomnumber) > -1) continue;
              arr[arr.length] = randomnumber;
          }
          for(var i=0; i < arr.length; i++){
            this.questions[i] = this.questionsJson[arr[i]];
          }
          this.questionStage = true;
          this.perc = null;
          this.correct = 0;
          this.resultsStage = false;
          this.currentQuestion = 0;
          this.answers = [];
      },
      handleAnswer(e) {
        this.answers[this.currentQuestion]=e.answer;
        if((this.currentQuestion+1) === this.questions.length) {
          this.handleResults();
          this.questionStage = false;
          this.resultsStage = true;
        } else {
          this.currentQuestion++;
        }
      },
      handleResults() {
        this.questions.forEach((a, index) => {
          if(this.answers[index] === a.answer) this.correct++;
        });
        this.perc = ((this.correct / this.questions.length)*100).toFixed(2);
      }
    }
}
</script>

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
</style>
