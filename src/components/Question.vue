<template>
<div class='container'>
    <div class='row question'>
        <h2>{{ questionIndex + 1 }} - {{ questionText }}</h2>
    </div>
    <div class='row responses' >
            <div class='col-sm-1 col-thumb'>
                <i class="material-icons">thumb_down</i>
            </div>
            <div class='col-sm-2 col-question' v-for="response in responses" :key="response.value">
                <div class='radiolabel' :class='{checked:isSelected(response.value)}'>
                    <div 
                    class='radiolabel-top' 
                    @click="onSelectAnswer(response.value)">
                        {{response.text}}
                    </div>
                    <div class='radiolabel-bottom'></div>
                </div>
            </div>
            <div class='col-sm-1 col-thumb'>
                <i class="material-icons">thumb_up</i>
            </div>
    </div>
    <div class='row'>
        <div class='col-2 col-nav'>
        <div @click="previous" v-show="this.questionIndex > 0" class="nav-button">
                    <i class="material-icons">navigate_before</i>
        </div>
        </div>
        <div class='col-8 col-progress'>
            <div class="progress">
                <div class="progress-bar" role="progressbar" :style="'width:'+ progression + '%'" :aria-valuenow="questionIndex" aria-valuemin="0" :aria-valuemax="numberOfQuestions">
                </div>
            </div>
        </div>
        <div class='col-2 col-nav'>
        <div @click="next" v-show="this.answerSelected !== -1" class="nav-button">
                    <i class="material-icons">navigate_next</i>
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
        next(){
            this.$emit('next')
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

@media (max-width:768px){
    .radiolabel-bottom{
        display:none;
    }

    .question h2{
        font-size:1.2rem;
    }

    .radiolabel-top{
        margin: auto;
        color: #000;
        font-weight: bold;
        width: 85%;
        text-align: center;
        background: white;
        cursor: pointer;
        margin-bottom: 0.3rem;
        padding: 0.2rem;
        border-left:0.3rem solid #b6ce28;
    }
    .col-thumb{
    text-align:center;
    }

    .row.question{
        margin-bottom:1rem;
        height: 4rem;
    }
    

    .row.responses{
        margin-bottom:2rem;
    }

    .col-progress{
    padding-top: 0.15em
    }

    .radiolabel.checked>.radiolabel-top{
        background-color:#b6ce28;
        color:white;
    }

}

@media (min-width:768px){

    .col-progress{
    padding-top: 0.65em
    }

    .nav-button .material-icons{
        font-size:2.5em;
    }

    .row.responses{
        
        margin-bottom:4rem;
    }

    .row.question{
        margin-bottom:4rem;
        margin-top:2rem;
    }
    .radiolabel-top{
        margin:auto;
        color: #000;
        font-weight:bold;
        width:85%;
        text-align: center;
        background: white;
        height: 22vh;
        padding-top: 25%;
        cursor: pointer; 
    }

    .radiolabel-bottom{
        margin:auto;
        width:85%;
        background-color: white;
        height: 2vh;
    }

    .radiolabel:hover>.radiolabel-bottom{
        background-color:#b6ce28;
        transition: background-color 1s;
    }

    .radiolabel.checked>.radiolabel-bottom{
        background-color:#b6ce28;
    }

    .col-thumb{
        text-align:center;
        padding-top: 9vh;
    }
    
}

.progress{
    border-radius:.5rem;
}

.progress-bar{
    background-color: #b6ce28;
}

.col-question{
    text-align:center;
}

.nav-button{
    cursor:pointer;
}

.col-nav{
    text-align:center;
}





</style>