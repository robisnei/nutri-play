<template>
    <b-card header-tag="header" footer-tag="footer">
        <div slot="header">
            <h5 class="mb-0"><b>Questão {{ questionNumber }}</b></h5>
            <br>
            <b-progress :value="progress" variant="primary" striped class="mb-2"></b-progress>
        </div>
        
        <h5>{{ question.text }}</h5>
        <em slot="footer"><a v-bind:href="question.more" target="_blank">Saiba mais sobre</a></em>
        <div v-if="question.type === 'mc'">
            <div v-for="(mcanswer,index) in question.answers">
                <b-alert show variant="primary">
                    <input type="radio" :id="'answer'+index" name="currentQuestion" v-model="answer" :value="mcanswer">
                    <p :for="'answer'+index">{{mcanswer}}</p>
                </b-alert>
            </div>
        </div>
    <b-button class="btn-block" variant="primary" size="lg" @click="submitAnswer">Responder</b-button>
    </b-card>
</template>

<script>
    export default {
        name: 'question',
        props:['question','question-number', 'progress'],
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
