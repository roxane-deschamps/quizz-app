<template>
  <div id="app">
    <home v-if='!beginTest && !endTest'
          @beginTest='beginTest = true'>

    </home>
    <div id='quiz' v-if='beginTest'>
      <h1>{{ quiz.title }}</h1>
      <question :questionIndex='questionIndex'
                :questionText='quiz.questions[questionIndex].text' 
                :answerSelected='userResponses[questionIndex]'
                :numberOfQuestions='quiz.questions.length'
                @questionAnswered="onQuestionAnswered" 
                @previous="decrementIndex">
      </question>
    </div>
  </div>
</template>

<script>
import Question from "./components/Question.vue";
import Home from "./components/Home.vue";


var quiz = {
        title: "My quiz",
        questions: [
          {
            text: "Question 1",
          },
          {
            text: "Question 2",
          }
        ]
      };
export default {
  name: "app",
  components: {
    Home,
    Question
  },
  data() {
    return {
      quiz :quiz,
      questionIndex: 0,
      userResponses: Array(quiz.questions.length).fill(-1),
      beginTest : false,
      endTest:false
    };
  },
  methods:{
    onQuestionAnswered(args){
      this.userResponses[this.questionIndex] = args.valSelected;
      this.questionIndex ++;
    },
    decrementIndex(){
      this.questionIndex --;
    }
  }
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
