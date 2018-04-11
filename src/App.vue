<template>
  <div id="app" class="container-fluid">
    <div id='header' class='header'>
      <img src="../src/assets/Logo_Horizontal_bW_white.png" width="300" @click='returnHome'>
    </div>
    <home v-if='!beginTest && !endTest'
          @beginTest='onBeginTest'>

    </home>
    <div id='quiz' v-if='beginTest && !endTest' class="container">
      <h1>{{ quiz.title }}</h1>
      <question :questionIndex='questionIndex'
                :questionText='quiz.questions[questionIndex].text' 
                :answerSelected='userResponses[questionIndex]'
                :numberOfQuestions='numberOfQuestions'
                @questionAnswered="onQuestionAnswered" 
                @previous="decrementIndex">
      </question>
    </div>
    <div id='results-container' v-if='endTest' class="container">
      <results :scores='scores'></results>
      <div id='feedback'>
        <h3>Aidez-moi à améliorer ce test !</h3>
        <input type='text' v-model='feedback'>
        <button @click='submitFeedback'>Envoyer</button>
      </div>
      <button @click='onBeginTest'>Recommencer le test</button>
    </div>
  </div>
</template>

<script>
import Question from "./components/Question.vue";
import Home from "./components/Home.vue";
import Results from "./components/Results.vue";



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
    Question,
    Results
  },
  data() {
    return {
      quiz :quiz,
      questionIndex: 0,
      userResponses: '',
      beginTest : false,
      endTest:false,
      feedback:'',
      scores:''
    };
  },
  methods:{
    onQuestionAnswered(args){
      this.userResponses[this.questionIndex] = args.valSelected;
      this.questionIndex ++;
      if(this.questionIndex == this.numberOfQuestions){
        this.scores = [this.userResponses[0], 2, 3, 4, 5];
        this.endTest = true;
      }
    },
    decrementIndex(){
      this.questionIndex --;
    },
    onBeginTest(){
      this.beginTest = true;
      this.endTest = false;
      this.questionIndex = 0;
      this.userResponses= Array(this.numberOfQuestions).fill(-1);
    },
    returnHome(){
      this.beginTest = false;
      this.endTest = false;
      this.questionIndex = 0;
      this.userResponses= Array(this.numberOfQuestions).fill(-1);
    },
    submitFeedback(){
      alert('feedback submited : ' + this.feedback);
    }
  },
  computed:{
    numberOfQuestions(){
      return this.quiz.questions.length;
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
  color: white;
  background-color:#b6ce28;
  background-color:rgb(15, 148, 239);
}

.header{
  text-align: left;
  cursor: pointer; 
}
</style>
