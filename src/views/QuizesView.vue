
<script setup>
import {ref, watch, computed} from 'vue'
import quizes from '@/data/quizes.json'
import {useRoute} from 'vue-router'
import QuizHeader from '@/components/QuizHeader.vue'
import Question from '@/components/Question.vue'
import Results from '@/components/Results.vue'


const currentQuestionIndex = ref(0)
const numberOfCorrectAnswers = ref(0)

const route = useRoute()
const quizId = parseInt(route.params.id)

const quiz = quizes.find((q)=>{
    return q.id === quizId
})

/*const questionStatus = ref(`${currentQuestionIndex.value}/${quiz.questions.length}`)

watch(currentQuestionIndex, ()=>{
    questionStatus.value = `${currentQuestionIndex.value}/${quiz.questions.length}`
})*/

const questionStatus = computed(()=>{
    return `${currentQuestionIndex.value}/${quiz.questions.length}`
})

const barPercentage = computed(()=>{
    return `${currentQuestionIndex.value/quiz.questions.length * 100}%`
})

const showResults = ref(false)
function onSelectedOptions(isCorrect){
    if(isCorrect){
        numberOfCorrectAnswers.value++
    }

    if(quiz.questions.length -1 === currentQuestionIndex.value ){
            showResults.value = true
        }
    currentQuestionIndex.value++


}

</script>

<template>
    <div>
        <QuizHeader

            :questionStatus="questionStatus"
            :barPercentage="barPercentage"
        />
        <div>
            <Question
                v-if="!showResults"
                :questions = "quiz.questions[currentQuestionIndex]"
                @selectedOptions="onSelectedOptions"
            />

            <Results
                v-else
                :quizQuestionLength="quiz.questions.length"
                :numberOfCorrectAnswers = "numberOfCorrectAnswers"
            />

        </div>

    </div>

</template>

