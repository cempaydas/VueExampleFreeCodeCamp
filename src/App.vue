<template>
  <div id="app">
    <Header :countQuestion="questionsLength" :current="index + 1" />
    <b-container class="bv-example-row">
      <b-row sm="6" offset="3">
        <b-col>
          <b-spinner
            style="width: 5rem; height: 5rem"
            variant="success"
            label="Spinning"
            v-if="!questions.length"
          ></b-spinner>

          <QuestionBox
            v-if="questions.length"
            :currentQuestion="questions[index]"
            :next="next"
        /></b-col>
      </b-row>
    </b-container>
  </div>
</template>

<script>
import Header from "./components/Header.vue";
import QuestionBox from "./components/QuestionBox.vue";

export default {
  name: "App",
  components: {
    Header,
    QuestionBox,
  },
  data() {
    return {
      questions: [],
      index: 0,
      questionsLength: 0,
    };
  },

  methods: {
    next() {
      console.log(this.questions.length);
      if (this.index < this.questions.length-1) {
        this.index++;
      }
    },
  },
  mounted: function () {
    fetch(
      "https://opentdb.com/api.php?amount=10&category=11&difficulty=easy&type=multiple",
      {
        method: "get",
      }
    )
      .then((response) => {
        return response.json();
      })
      .then((jsonData) => {
        this.questions = jsonData.results;
        this.questionsLength = jsonData.results.length;
      });
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
