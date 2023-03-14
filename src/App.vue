<template>

<StepperComponent :page_active="page" />

  <InformationQuiz v-if="!etat" @start="startQuiz"/>

  <QuizApp v-if="etat" @pageActive="detectPage" />




</template>

<script>
import QuizApp from './components/QuizApp.vue';
import StepperComponent from './components/StepperComponent.vue';
import InformationQuiz from './components/InformationQuiz.vue';


export default {
  data(){
   return {
    etat:false,
    page:null
   }
  },
  components:{
    QuizApp,
    InformationQuiz,
    StepperComponent,
  

  },
 
  methods:{
    
    startQuiz(){
      this.etat=!this.etat
    },
    detectPage(page){
     
      this.page=page      
    }
  }
}

</script>