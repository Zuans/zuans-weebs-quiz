<template>
  <div>
    <b-jumbotron class="jumbotron">
      <template v-slot:lead>
        <h3 class="text-white">Weaboo Quiz By Zuans</h3>
      </template>
      <div v-if="!submit">
        <Form :submitted="submitted" :changeValue="changeValue " />
      </div>
      <div v-if="submit">
        <h3 class="mt-5 text-white">Question ?</h3>
        <p class="text-white">{{ currentQuestion.question }}</p>
        <hr class="my-4" />
        <b-list-group>
          <b-list-group-item
            v-for="(answer,index) in shuffleAnswer"
            @click="selectAnswer(index)"
            :key="index"
            :class="answerClass(index)"
          >{{ answer }}</b-list-group-item>
        </b-list-group>
        <b-button
          variant="primary"
          @click="submitAnswer"
          :disabled="selectedIndex === null || answered"
          class="mt-5 mr-3"
          href="#"
        >Submit</b-button>
        <b-button variant="success" class="mt-5" v-on:click="next" href="#">Next</b-button>
        <button @click="reset" class="btn btn-danger mt-3 ml-auto d-block">Reset</button>
      </div>
    </b-jumbotron>
  </div>
</template>

<script>
import _ from "lodash";
import Form from "./form";
export default {
  name: "QuizBox",
  components: {
    Form
  },
  props: {
    currentQuestion: Object,
    next: Function,
    increment: Function,
    changeValue: Function
  },
  data() {
    return {
      shuffleAnswer: [],
      selectedIndex: null,
      correctIndex: null,
      answered: false,
      submit: false
    };
  },
  mounted() {
    this.shuffleAnswers();
  },
  watch: {
    currentQuestion: {
      immediate: true,
      handler() {
        this.shuffleAnswers();
        this.selectedIndex = null;
        this.answered = false;
      }
    }
  },
  methods: {
    selectAnswer(index) {
      this.selectedIndex = index;
    },
    shuffleAnswers() {
      this.shuffleAnswer = _.shuffle(this.answers);
      this.correctIndex = this.shuffleAnswer.indexOf(
        this.currentQuestion.correct_answer
      );
    },
    submitAnswer() {
      let isCorrect = false;
      if (this.selectedIndex === this.correctIndex) {
        isCorrect = true;
      }
      this.answered = true;
      this.increment(isCorrect);
    },
    answerClass(index) {
      let answerClass = "";
      if (!this.answered && this.selectedIndex === index) {
        answerClass = "selected";
      } else if (this.answered && this.correctIndex === index) {
        answerClass = "correct";
      } else if (
        this.answered &&
        this.selectedIndex === index &&
        this.selectedIndex !== this.correctIndex
      ) {
        answerClass = "incorrect";
      } else {
        answerClass = "";
      }
      return answerClass;
    },
    submitted() {
      this.submit = true;
    },
    reset() {
      location.reload();
    }
  },
  computed: {
    answers: function() {
      const answer = [
        ...this.currentQuestion.incorrect_answers,
        this.currentQuestion.correct_answer
      ];
      return answer;
    }
  }
};
</script>

<style scoped>
h3 {
  text-shadow: 2px 2px 2px black;
}
.list-group-item:hover {
  cursor: pointer;
  background-color: #eee;
}

.selected {
  background-color: #428bca;
}

.selected:hover {
  background-color: #428bca;
}

.incorrect {
  background-color: #d9534f;
}

.correct {
  background-color: #5cb85c;
}

.jumbotron {
  background-color: rgba(90, 89, 89, 0.651);
}
</style>
