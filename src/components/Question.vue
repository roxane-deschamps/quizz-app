<template>
<div>
    <h2>{{ questionText }}</h2>
    <ul>
            <li v-for="response in responses" :key="response.value">
                <input type="radio" 
                        name = "responses"
                    :checked = "isSelected(response.value)"
                    :value="response.value" 
                    @click="onSelectAnswer(response.value)"
                >
                <label>{{response.text}}</label>
            </li>
    </ul>

    <p>
        <button @click="previous" v-show="this.questionIndex > 0">
            Question précédente
        </button>
        Progression : {{progression}}%</p>
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
</style>