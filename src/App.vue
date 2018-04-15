<template>
  <div class="container-fluid my-app">
    <div id='header' class='header'>
      <img src="../src/assets/Logo_Horizontal_bW_white.png" @click='returnHome'>
    </div>
    <home v-if='!beginTest && !endTest'
          @beginTest='onBeginTest'>

    </home>
    <div id='quiz' v-if='beginTest && !endTest' class="container">
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
        <div class="btn-toolbar mb-3" role="toolbar" aria-label="Toolbar with button groups">
          <div class="btn-group mr-2" role="group" aria-label="First group">
            <button type="button" class="btn btn-secondary">1</button>
            <button type="button" class="btn btn-secondary">2</button>
            <button type="button" class="btn btn-secondary">3</button>
            <button type="button" class="btn btn-secondary">4</button>
            <button type="button" class="btn btn-secondary">5</button>
          </div>
        </div>
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

import axios from 'axios'



var quiz = {
        questions: [
          {
            text: "Vous aimez sortir de votre zone de confort",
            coeffs:[0, -2, 3, 2, 5,2]
          },
          {
            text: "Vous pensez que la science est une histoire d'experts",
            coeffs:[-2,0,-2,0,-2,-4]
          },
          {
            text: "Vous préférez la ville à la campagne",
            coeffs:[-2,0,0,-4,0,0]
          },
          {
            text: "Vous avez tendance à vous emmeler dans vos explications",
            coeffs:[0,1,1,0,0,-5]
          },
          {
            text: "Vous discutez facilement avec des inconnus",
            coeffs:[2,0,3,2,4,3]
          },
          {
            text: "Vous êtes pour l'écologie seulement si vous concervez votre niveau de vie",
            coeffs:[-2,1,0,-5,-2,0]
          },
          {
            text: "Acheter en kit est encore plus fun qu'acheter neuf",
            coeffs:[0,5,0,1,0,0]
          },
          {
            text: "Seul on est plus efficace",
            coeffs:[-3,0,-4,0,-2,1]
          },
          {
            text: "Vous n'êtes pas très manuel",
            coeffs:[0,-5,0,0,0,2]
          },
          {
            text: "Vous pouvez rester facilement 3h sur Wikipedia",
            coeffs:[3,0,2,0,0,4]
          },
          {
            text: "Vous ne pourriez pas vivre sans votre téléphone",
            coeffs:[-2,1,2,-3,0,0]
          },
          {
            text: "Vous aimez réparer vous-même vos objets",
            coeffs:[0,5,0,2,0,0]
          },
          {
            text: "Vous rêver d'avoir un brevet à votre nom",
            coeffs:[-2,3,-3,-3,-2,-2]
          },
          {
            text: "Vous avez du mal à vous mettre à la place de l'autre",
            coeffs:[2,0,-2,-2,-4,0]
          },
          {
            text: "Vous préférez imaginer que fabriquer",
            coeffs:[0,-3,0,2,0,1]
          },
          {
            text: "On n'entend pas assez parler des problèmes écologiques et sociaux",
            coeffs:[5,0,0,3,3,2]
          },
          {
            text: "Dans une organisation, la hiérarchie est plus efficace que l'horizontalité",
            coeffs:[-2,0,-4,0,-2,1]
          },
          {
            text: "Vous avez toujours été membre d'une association",
            coeffs:[3,0,4,1,4,0]
          },
          {
            text: "On vient souvent vous demander des conseils techniques",
            coeffs:[0,4,0,0,0,3]
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
      scores:'',
      idFeedback :''
    };
  },
  methods:{
    onQuestionAnswered(args){
      this.userResponses[this.questionIndex] = args.valSelected;
      this.questionIndex ++;
      if(this.questionIndex == this.numberOfQuestions){
        this.calcScores();
        this.endTest = true;
      }
    },
    calcScores(){
      this.scores = [this.userResponses[0], 2, 3, 4, 5, 6];
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
      axios.post('http://localhost:3000/sendFeedback', {
          feedback:this.feedback
      }).then(response => {
        this.idFeedback = response
      })
      .catch(e => {
      console.error(e)
    });
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
.my-app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: white;
}

body {
  background-color:#1565C0;
}

.header{
  text-align: left;
  cursor: pointer;
}

.header>img{
  width:15%;
}

</style>
