
<script setup>


    import {defineProps} from 'vue'
    import {useRoute, useRouter, RouterView} from 'vue-router'
    const {quize} = defineProps(['quize'])
    import QuizesView from '@/views/QuizesView.vue'

    const route = useRoute()
    const router = useRouter()



   function redirectToQuizes(){
    router.push(`/quizes/${quize.id}`)


   }


</script>

<template>

    <div>
        <img :src="quize.img" @click="redirectToQuizes" alt="">
        <div class="card-text">
            <h2>{{ quize.name }}</h2>
            <p>{{ quize.questions.length }} questions</p>
        </div>
    </div>
</template>



<style>
.card {
    width: 310px;
    overflow: hidden;
    border-radius: 2%;
    box-shadow: 1px 1px 10px rgba(0,0,0,0.1);
    margin-bottom: 35px;
    margin-right: 20px;
    cursor: pointer;
  }

  .card img {
    width: 100%;
    height: 190px;
    margin: 0
  }

  .card .card-text {
    padding: 0 5px
  }

  .card .card-text h2 {
    font-weight: bold;
  }

</style>