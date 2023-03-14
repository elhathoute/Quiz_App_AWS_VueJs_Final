<template>
   

<div class="mb-20">
<ol class="flex  border-b-4 border-indigo-500 p-4 items-center w-full text-sm font-medium text-center text-gray-500 dark:text-gray-400 sm:text-base">
    <li 
    v-for="(item,key) in stepperComponent" :key="key"
    :class="{'text-blue-600 after:bg-green-300': item.isActive }"
    class="flex md:w-full items-center sm:after:content-['\'] after:w-full after:h-1 after:w-20  after:border-b after:bg-white after:border-white after:border-2  after:hidden sm:after:inline-block after:mx-6 xl:after:mx-10 dark:after:border-gray-700">
        <span class="flex items-center">
            <svg aria-hidden="true" class="w-4 h-4 mr-2 sm:w-5 sm:h-5" fill="currentColor" viewBox="0 0 20 20" xmlns="http://www.w3.org/2000/svg"><path fill-rule="evenodd" d="M10 18a8 8 0 100-16 8 8 0 000 16zm3.707-9.293a1 1 0 00-1.414-1.414L9 10.586 7.707 9.293a1 1 0 00-1.414 1.414l2 2a1 1 0 001.414 0l4-4z" clip-rule="evenodd"></path></svg>
            <span class="mr-2">{{item.id}}-</span>
            {{ item.name }}
        </span>
        
    </li>
    

</ol>
</div>




  
</template>

<script>
export default {
    name:'StepperComponent',
    props:['page_active'],
    data(){
        return{
            stepperComponent:
            {
            "Info":{id:'1',name:'Info',isActive:true},
             "Quiz" :{id:'2',name:'Quiz',isActive:false},
            //  "Result":{name:'Result',isActive:false},
            }
        }
    },
    watch:{
        page_active(){
            this.stepperComponent[this.page_active].isActive = true
        }
    }
}
</script>