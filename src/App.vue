<template>
  <div class="container-fluid my-app">
    <div id='header' class='header'>
      <img src="../src/assets/Logo_Horizontal_bW_white.png" @click='goToLaClavette'>
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
                @previous="decrementIndex"
                @next="incrementIndex">
      </question>
    </div>
    <div id='results-container' v-if='endTest' class="container">
      <results :scores='scores' @retry='onBeginTest'></results>
      <div class="container" id='feedback'>
        <h4>Aidez-nous à améliorer ce quiz</h4>
        <div class='row'>
          <div class='col-sm-3'>
            Sur une échelle de 5, est-ce que le profil trouvé vous correspond ?
          </div>
          <div class='col-sm-2'>
            <div class="btn-toolbar mb-3" role="toolbar" aria-label="Toolbar with button groups">
            <div class="btn-group mr-2" role="group" aria-label="First group">
              <button type="button" class="btn btn-secondary" :class="{checked:this.feedback.note === 1}" @click="selectEval(1)">1</button>
              <button type="button" class="btn btn-secondary" :class="{checked:this.feedback.note === 2}" @click="selectEval(2)">2</button>
              <button type="button" class="btn btn-secondary" :class="{checked:this.feedback.note === 3}" @click="selectEval(3)">3</button>
              <button type="button" class="btn btn-secondary" :class="{checked:this.feedback.note === 4}" @click="selectEval(4)">4</button>
              <button type="button" class="btn btn-secondary" :class="{checked:this.feedback.note === 5}" @click="selectEval(5)">5</button>
            </div>
            </div>
          </div>
          <div class='offset-sm-1 col-sm-4'>
            <textarea v-model='feedback.commentaire' placeholder="Trouvez-vous ce quiz pertinent ? Des idées d'amélioration ? Un petit coucou ? =)"></textarea>
          </div>
          <div class='col-sm-2 no-xs'>
            <button class='btn btn-primary' @click='submitFeedback'>Envoyer</button>
          </div>
        </div>
        <div class='row'>
          <div class="col-10 col-sm-5 col-savoir-plus">
            Êtes-vous curieux d'en savoir plus sur l'ingénierie positive ?
          </div>
          <div class='col-2 col-sm-1 col-savoir-plus' >
            <div class="my-checkbox" @click="feedback.savoirPlus = !feedback.savoirPlus">
              <i class="material-icons" v-if="feedback.savoirPlus">check</i>
            </div>
          </div>
          <div class='col-sm-4 col-savoir-plus' >
            <input v-show="feedback.savoirPlus" type="email" placeholder="Votre adresse email" v-model="feedback.email">
          </div>
          <div class='no-sm col-6'>
            <button class='btn btn-primary' @click='submitFeedback'>Envoyer</button>
          </div>
           <div class='col-6 col-sm-2' id="merci" v-if="feedbackSent">
            Merci !
          </div>
        </div>
      </div>
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
            text: "Vous avez tendance à vous emmêler dans vos explications",
            coeffs:[0,1,1,0,0,-5]
          },
          {
            text: "Vous discutez facilement avec des inconnus",
            coeffs:[2,0,3,2,4,3]
          },
          {
            text: "Vous êtes pour l'écologie seulement si vous conservez votre niveau de vie",
            coeffs:[-2,1,0,-5,-2,0]
          },
          {
            text: "Acheter en kit est encore plus fun qu'acheter neuf",
            coeffs:[0,5,0,1,0,0]
          },
          {
            text: "Seul, on est plus efficace",
            coeffs:[-3,0,-4,0,-2,1]
          },
          {
            text: "Les activités manuelles vous font fuir",
            coeffs:[0,-5,0,0,0,2]
          },
          {
            text: "Vous pouvez rester facilement 3 heures sur Wikipedia",
            coeffs:[3,0,2,0,0,4]
          },
          {
            text: "Impossible de vivre sans votre téléphone",
            coeffs:[-2,1,2,-3,0,0]
          },
          {
            text: "Vous aimez réparer vous-même vos objets",
            coeffs:[0,5,0,2,0,0]
          },
          {
            text: "Vous rêvez d'avoir un brevet à votre nom",
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
            text: "Il faudrait qu'on entende plus parler des problèmes écologiques et sociaux",
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
      feedback:{
        id:null,
        note:null,
        commentaire:'',
        savoirPlus:false,
        email:'',
        profil:null
      },
      scores:[],
      responsesCoeffs:[-2,-1,0,1,2],
      feedbackSent : false
    };
  },
  methods:{
    onQuestionAnswered(args){
      this.userResponses[this.questionIndex] = args.valSelected;
      this.questionIndex ++;
      if(this.questionIndex == this.numberOfQuestions){
        this.calcScores();
        this.saveAnswersDb();
        this.endTest = true;
      }
    },
    saveAnswersDb(){
        axios.post('http://quiz.laclavette.fr/backend/sendAnswers', {
          answers:this.userResponses
      }).then(response => {
        this.feedback.id = response.data;
        console.log('reponse axios save answers: ' + response);
      })
      .catch(e => {
      console.error(e);
      console.log('reponse non traitée')
      });
    },
    calcScores(){
      var _this = this;
      var indexProfilMax = -1;
      var scoreProfilMax = -1;
      for (var i = 0; i <= 5; i++) {
        var score = 0.5;
        this.userResponses.forEach(function(element, index){
          var scoreQuestion = 0.5/60 * _this.responsesCoeffs[element] * _this.quiz.questions[index].coeffs[i];
          score += scoreQuestion;
        });
        console.log('index profil : ' + i + ', score : ' + score);
        if(score > scoreProfilMax){
          scoreProfilMax = score;
          indexProfilMax = i;
        }
        _this.scores.push(Math.round(score * 100)/100);
      }
      this.feedback.profil = indexProfilMax;

    },
    selectEval(note){
      console.log('dans la méthode selectEval, valeur : ' + note);
      this.feedback.note = note;
    },
    decrementIndex(){
      this.questionIndex --;
    },
    incrementIndex(){
      this.questionIndex ++;
    },
    onBeginTest(){
      this.beginTest = true;
      this.feedbackSent = false
      this.endTest = false;
      this.questionIndex = 0;
      this.userResponses= Array(this.numberOfQuestions).fill(-1);
      this.scores=[];
      this.feedback={
        id:null,
        note:null,
        commentaire:'',
        savoirPlus:false,
        email:'',
        profil:null
      }
    },
    goToLaClavette(){
      window.open("http://www.laclavette.fr");
    },
    submitFeedback(){
      this.feedbackSent = true;
      axios.post('http://quiz.laclavette.fr/backend/sendFeedback', {
          feedback:this.feedback
      }).then(response => {
        console.log(response);
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
@media (max-width:768px){
.header{
  text-align: center;
  cursor: pointer;
}

.header>img{
  height: 8vh;
  margin: 1.5em;
}
}

@media (min-width:768px){
  .header{
  text-align: left;
  cursor: pointer;

}
.header>img{
  height: 10vh;
  margin: 2em;
}

}
.my-app {
  font-family: 'Lato', sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: white;
}


body {
  background-color:#1565C0;
}


#feedback{
  margin-top: 3em;
  padding: 2em;
  background-color:white;
  color:rgb(83, 83, 83);
}

#feedback h4{
    margin-bottom:1rem;
    font-size: 1rem;
    font-weight: bold;
    color: rgb(63, 63, 63);
    text-transform: uppercase;
}

#feedback textarea{
  width:100%;
}

#feedback .btn.checked{
    box-shadow: 0 0 0 0.2rem rgba(108,117,125,.5);
    color: #fff;
    background-color: #545b62;
    border-color: #4e555b;
}

#feedback .col-savoir-plus{
  margin-top: .375rem;
  margin-bottom: .7rem;
}

#feedback .btn-primary{
  background-color:#1E88E5;
    border: none;
    border-radius: 0;
    box-shadow: none;
}

#feedback .btn-primary:hover{
  background-color:#1565C0;
}

#merci{
    padding-left: 2em;
    color: green;
}

.my-checkbox{
  width: 1.5rem;
    height: 1.5rem;
    border: 1px solid rgb(169, 169, 169);
    margin-top: 0.2rem;
}

.my-checkbox .material-icons{
  color:green;
  font-weight:bold;
  font-size:1.5rem;
}

#feedback input[type='email']{
  width: 100%;
}

</style>
