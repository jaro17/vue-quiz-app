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
      // Tracks the index of the current question.
      currentQuestionIndex: 0,
      // Tracks the user's score.
      score: 0,
      // Indicates whether the quiz has ended.
      quizEnded: false,
    }
  },
  methods: {
    // Method to check if the selected answer is correct.
    checkAnswer(selectedIndex) {
      // If the selected answer is correct, increment the score.
      if (selectedIndex === this.currentQuestion.correctAnswer) {
        this.score++;
      }
      // Move to the next question.
      this.nextQuestion();
    },

    // Method to move to the next question.
    nextQuestion() {
      // Increment the current question index.
      this.currentQuestionIndex++;
      // If all questions have been answered, end the quiz.
      if (this.currentQuestionIndex === this.questions.length) {
        this.quizEnded = true;
      }
    }
  },
  computed: {
    // Computed property to get the current question based on the current question index.
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
      <!-- Display the current question -->
      <div id="question" class="mb-4">{{ currentQuestion.question }}</div>
      <div id="options">
        <!-- Loop through the current question's options and create a button for each option -->
        <button
            class="button mb-4 ml-3 mr-3"
            v-for="(option, index) in currentQuestion.options"
            :key="index"
            @click="checkAnswer(index)"
        >
          {{ option }}
        </button>
      </div>
      <!-- Button to manually move to the next question -->
      <button id="nextButton" @click="nextQuestion" class="button mb-4">Next</button>
    </div>
    <div v-else>
      <!-- Display the final score when the quiz ends -->
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
