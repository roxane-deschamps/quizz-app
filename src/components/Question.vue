<template>
<div class='container'>
    <div class='row question'>
        <h2>{{ questionIndex + 1 }} - {{ questionText }}</h2>
    </div>
    <div class='row responses' >
            <div class='col-sm' v-for="response in responses" :key="response.value">
                <div class='radiolabel' :class='{checked:isSelected(response.value)}'>
                    <div 
                    class='radiolabel-top' 
                    @click="onSelectAnswer(response.value)">
                        {{response.text}}
                    </div>
                    <div class='radiolabel-bottom'></div>
                </div>
            </div>
    </div>
    <div class='row'>
        <div class='col-sm-2'>
        <div @click="previous" v-show="this.questionIndex > 0" class="nav-button">
                    <i class="material-icons">navigate_before</i>
        </div>
        </div>
        <div class='col-sm-8'>
            <div class="progress">
                <div class="progress-bar" role="progressbar" :style="'width:'+ progression + '%'" :aria-valuenow="questionIndex" aria-valuemin="0" :aria-valuemax="numberOfQuestions">
                </div>
            </div>
        </div>
         
    </div>



   
    
   
</div>
</template>

<script>
var responses = [{text: "Pas du tout", value: 0}, {text: "Plutôt non", value: 1}, {text: "Sans opinion", value:2}, {text: "Plutôt oui", value:3}, {text: "Tout à fait", value: 4}]
export default{
    props: {
        questionIndex: Number,
        questionText : String,
        answerSelected:Number,
        numberOfQuestions:Number
    },
    data(){
        return {
            responses:responses
        }
    },
    methods:{
        onSelectAnswer(valSelected){
            this.$emit('questionAnswered', {valSelected : valSelected})
        },
        previous(){
            this.$emit('previous')
        },
        isSelected(val){
            return val === this.answerSelected;
        }
    },
    computed:{
        progression(){
            return (this.questionIndex) / this.numberOfQuestions * 100;
        }
    }
    
}



</script>

<style>

.radiolabel-top{
    margin:auto;
    color: #000;
    width:80%;
    text-align: center;
    background: white;
    height: 29vh;
    padding-top: 20%;
    cursor: pointer; 
}

.radiolabel-bottom{
    margin:auto;
    width:80%;
    background-color: white;
    height: 2vh;
}

.radiolabel:hover>.radiolabel-bottom{
    background-color:#b6ce28;;
    transition: background-color 1s;
}

.radiolabel.checked>.radiolabel-bottom{
    background-color:#b6ce28;
}

.progress-bar{
    background-color: #b6ce28;
}

.col-sm{
    text-align:center;
}

.row.responses{
    margin-bottom:4rem;
}

.row.question{
    margin-bottom:4rem;
    margin-top:2rem;
}

.nav-button.material-icons{
    font-size:2rem;
}

.nav-button{
    cursor:pointer;
}



</style>