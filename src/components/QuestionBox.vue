<template>
  <div class="question-box-container">
    <b-jumbotron>
      <template slot="lead">
        <p v-html="currentQuestion.question"></p>
      </template>

      <hr class="my-4" />

      <b-list-group>
        <b-list-group-item
          backgroud-color="#ccc"
          v-for="(answer, index) in answers"
          :key="index"
          @click="selectAnswer(index)"
          :class="[selectedAnswer === index ? 'selected' : '']"
        >
          {{ answer }}</b-list-group-item
        >
      </b-list-group>

      <b-button @click="submit" variant="primary" href="#">submit</b-button>
      <b-button @click="next" variant="success" href="#">next</b-button>
    </b-jumbotron>
  </div>
</template>

<script>
import _ from "lodash";
export default {
  props: {
    currentQuestion: Object,
    next: Function,
  },
  data() {
    return {
      selectedAnswer: null,
      suffledAnswers: [],
    };
  },
  methods: {
    selectAnswer(index) {
      this.selectedAnswer = index;
    },
    shufflesAnswers() {
      let answers = [
        ...this.currentQuestion.incorrect_answers,
        this.currentQuestion.correct_answer,
      ];
      this.suffledAnswers = _.suffled(answers);
    },
  },
  computed: {
    answers() {
      let answers = [...this.currentQuestion.incorrect_answers];
      answers.push(this.currentQuestion.correct_answer);
      return answers;
    },
    watch: {
      currentQuestion() {
        (this.selectedAnswer = null), this.shufflesAnswers();
      },
    },
  },
};
</script>
<style scoped>
.list-group {
  margin-bottom: 15px;
}
.list-group-item:hover {
  background: #eee;
  cursor: pointer;
}

.btn {
  margin: 0 5px;
}
.selected {
  background-color: lightblue;
}
.correct {
  background-color: lightgreen;
}
.incorrect {
  background-color: lightcoral;
}
</style>