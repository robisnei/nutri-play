<template>
    <div>
        <strong>Questão {{ questionNumber }}:</strong><br/>
        <strong>{{ question.text }} </strong>

        <div v-if="question.type === 'tf'">
            <input type="radio" name="currentQuestion" id="trueAnswer" v-model="answer" value="t"><label for="trueAnswer">True</label><br/>
            <input type="radio" name="currentQuestion" id="falseAnswer" v-model="answer" value="f"><label for="falseAnswer">False</label><br/>
        </div>

        <div v-if="question.type === 'mc'">
            <div v-for="(mcanswer,index) in question.answers">
            <input type="radio" :id="'answer'+index" name="currentQuestion" v-model="answer" :value="mcanswer"><label :for="'answer'+index">{{mcanswer}}</label><br/>
            </div>
        </div>
        <br>
        <button @click="submitAnswer">Responder</button>
        <br><br>
        <a v-bind:href="question.more" target="_blank">Saiba mais sobre</a>
    </div>
</template>

<script>
    export default {
        name: 'question',
        props:['question','question-number'],
        data() {
            return {
                answer:''
            }
        },
        methods:{
            submitAnswer:function() {
                this.$emit('answer', {answer:this.answer});
                this.answer = null;
            }
        }
    }
</script>
