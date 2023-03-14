<template>
  <div>
    <h1 class="text-center font-bold underline underline-offset-4">
      Welcome to AWS Cloud Practitioner
      <br />
      <br />
      Knowledge Test
    </h1>
    <ul class="mt-6">
      <li class="item"><h3 class="">Each question have only one correct answer</h3></li>
      <li class="item">
        <h3 class="">
          Pass the quiz and see how many questions you can answer correctly
        </h3>
      </li>
    </ul>

    <button @click="startQuiz()" class="btn bg-blue-300 p-4 m-4">Start</button>
  </div>
</template>

<script>
export default {

  name: "InformationQuiz",
  methods: {
    startQuiz() {
    
      this.$emit('start');
      
    },
  },
};
</script>
