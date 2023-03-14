<template>
     <div  class="w-full max-w-xl  bg-gray-200 ">
            <h1 class="font-bold text-3xl text-center text-indigo border-double border-4 border-indigo-600">Simple Quiz
                AWS</h1>
            <div class="bg-white p-12 rounded-lg shadow-lg w-full mt-8">
                <div v-if="index<count">
                    <p class="text-2xl font-bold text-center underline underline-offset-8">
                        {{ questions[index]['question']}}
                    </p>
                    <label
                     :for="key" class="block mt-4 border   border-gray-300 rounded-lg py-2 px-6 text-lg"
                        v-for="(answer,key) in questions[index]['answers'] " :key="key" 
                        :class="{
                        'hover:bg-blue-200  cursor-pointer': selectedAnswer === '',
                        'bg-green-400': key === questions[index]['correct_answer'] && selectedAnswer !=='',
                        'bg-red-400': key !== questions[index]['correct_answer'] && key ===selectedAnswer
                        
                        }">
                        <input type="radio" :id="key" class="hidden" :value="key" @change=answered($event)
                            :disabled="selectedAnswer !=''" :checked="selectedAnswer !=''">
                        {{ answer }}
                    </label>

                    <div class="mt-6 flow-root">
                        <button class="float-right p-3 bg-indigo-500 text-white text-sm font-bold rounded "
                            v-show="selectedAnswer!='' && index!=count-1 " @click="nextQuestion">Next
                        </button>
                        <button class="float-right p-3 bg-indigo-500 text-white text-sm font-bold rounded "
                            v-show="selectedAnswer !='' && index==count-1" @click="ShowResult">Finish
                        </button>
                    </div>
                </div>
                <div v-else class="flex flex-col items-center ">
                 <h2 class="text-bold text-3xl text-center"> Result :</h2>  
                 <div class="flex justify-start space-x-4 mt-6">
                    <p class="text-gray-500">Correct answers: 
                        <span class="text-2xl text-green-400 font-bold">
                            {{ correctAnswers }}
                        </span>
                    </p>
                    <p class="text-gray-500">Wrong answers: 
                        <span class="text-2xl text-red-400 font-bold">
                            {{ wrongAnswers }}
                        </span>
                    </p>
                 </div>

                 <!-- correct answer -->
                 <div class="my-4">
                    <h2 class="text-bold text-3xl text-center mb-4" v-if="explicationCorrect.length>0"> Explication :</h2>  

                    <ul>
                        <li v-for="(expli,index) in explicationCorrect " :key="index" class="m-2 flex items-center font-bold text-green-600">
                         <span class="text-gray-500 mx-1">Q-{{(expli.key)+1}}  :</span> {{ expli.explication}}
                        </li>
                    </ul>

                 </div>

                 <div class="mt-6 flow-root">
                    <button class="float-right p-3 bg-indigo-500 text-white text-sm font-bold rounded "
                         
                        @click="resetQuiz">Play again
                    </button>
                 </div>
                    
                </div>

            </div>

            <div v-if="index<questions.length" class="border-double border-4 bg-green-200 shadow-lg font-bold border-indigo-600">{{index+1}}/{{ questions.length }}</div>

        </div>
</template>

<script>
export default {
    name:'QuizApp',
    data() {
        return {
            etat:false,
            index:0,
            selectedAnswer:'',
            count:3,
            correctAnswers:0,
            wrongAnswers:0,
            explicationCorrect:[],

            questions:[
                {
                    question:"what is css",
                    answers:{
                        a:'nothing ',
                        b:'style sheet',
                        c:'nothing ',
                        d:'nothing ',
                    },
                    correct_answer:'b',
                    explication:'css is a stand for cascading',
                },
                {
                    question:"what is html",
                    answers:{
                        a:'nothing ',
                        b:'hyperText',
                        c:'nothing ',
                        d:'nothing ',
                    },
                    correct_answer:'b',
                    explication:'html is a stand for hypertext',

                },
                {
                    question:" php  for static websites",
                    answers:{
                        a:'true ',
                        b:'false',
                    },
                    correct_answer:'b',
                    explication:'php is a stand for preprocessor',

                },
               
            ]
        }
    },
    methods: {
        answered(event){
         
            this.selectedAnswer = event.target.value
            if(this.selectedAnswer==this.questions[this.index]['correct_answer']){
                this.correctAnswers++
          var newCorrAnswer ={"key":this.index,"explication":this.questions[this.index]['explication']}
                this.explicationCorrect.push(newCorrAnswer)
              
            }else
            {
                this.wrongAnswers++
                
            }

        },
        nextQuestion(){
            this.index++;
            this.selectedAnswer=''
            // console.log(this.selectedAnswer)
        },
        ShowResult(){

            this.index++;
        },
        resetQuiz(){
           this.index=0
           this.selectedAnswer=''
           this.correctAnswers=0
           this.wrongAnswers=0 
        }
    },
    mounted(){
        this.$emit('pageActive','Quiz')
    }
}
</script>