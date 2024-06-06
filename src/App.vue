<script>
export default {
  data() {
    return {
      questions: [
        {
          question: "What is the capital of France?",
          options: ["Madrid", "Berlin", "Paris", "Rome"],
          correctAnswer: 2,
        },
        {
          question: "Which planet is known as the Red Planet?",
          options: ["Mars", "Venus", "Jupiter", "Saturn"],
          correctAnswer: 0
        },
        {
          question: "What is 7 x 6?",
          options: ["56", "49", "64", "42"],
          correctAnswer: 3
        }
      ],
      currentQuestionIndex: 0,
      score: 0,
      quizEnded: false,
    }
  },
  methods: {
    checkAnswer(selectedIndex) {
      if (selectedIndex === this.currentQuestion.correctAnswer) {
        this.score++;
      }
      this.nextQuestion();
    },

    nextQuestion() {
      this.currentQuestionIndex++;
      if (this.currentQuestionIndex === this.questions.length) {
        this.quizEnded = true;
      }
    }
  },
  computed: {
    currentQuestion() {
      return this.questions[this.currentQuestionIndex]
    }
  }
}
</script>

<template>
  <div class="container">
    <h1 class="is-size-3 mt-6">Quiz App</h1>
    <div v-if="!quizEnded">
      <div id="question" class="mb-4">{{ currentQuestion.question }}</div>
      <div id="options">
        <button
            class="button mb-4 ml-3 mr-3"
            v-for="(option, index) in currentQuestion.options"
            :key="index"
            @click="checkAnswer(index)"
        >
          {{ option }}
        </button>
      </div>
      <button id="nextButton" @click="nextQuestion" class="button mb-4">Next</button>
    </div>
    <div v-else>
      <p class="mb-4 mt-4">Congratulations! You've completed the quiz.</p>
      <div id="score">Score: <span id="scoreValue">{{ score }} / {{ questions.length }}</span></div>
    </div>

  </div>
</template>

<style scoped>
.container {
  text-align: center;
}
</style>
