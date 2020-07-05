<template>
  <div id="app">
    <Header :numCorrect="numCorrect" :numTotal="numTotal" />
    <b-container class="bv-example-row mt-5">
      <b-row>
        <b-col sm="6" class="mx-auto" offset="0">
          <!-- apakah sudah menyelesaikan quiz -->
          <div v-if="!done">
            <QuizBox
              :changeValue="changeValue"
              v-if="questions.length"
              :increment="increment"
              :next="next"
              :currentQuestion="questions[index]"
            />
          </div>
          <!-- Jika sudah -->
          <div v-else-if="done">
            <doneQuiz :mode="mode" :rank="rank" />
          </div>
        </b-col>
      </b-row>
    </b-container>
    <Footer />
  </div>
</template>

<script>
import axios from "axios";
import Header from "./components/Header";
import QuizBox from "./components/QuizBox";
import doneQuiz from "./components/doneQuiz";
import Footer from "./components/footer";
export default {
  name: "App",
  components: {
    Header,
    QuizBox,
    doneQuiz,
    Footer
  },
  data() {
    return {
      questions: [],
      index: 0,
      numCorrect: 0,
      numTotal: 0,
      done: false,
      rank: null,
      mode: null
    };
  },
  beforeCreate() {
    document.body.className = "bg-img";
  },
  async mounted() {
    try {
      const data = axios.get(
        "https://opentdb.com/api.php?amount=5&category=31&difficulty=easy&type=multiple"
      );
      const responses = await data;
      this.questions = responses.data.results;
    } catch (error) {
      console.error(error);
    }
  },
  methods: {
    next() {
      this.index++;
      if (this.index == this.numTotal) {
        const score = this.getScore(this.numCorrect, this.numTotal);
        this.getRank(score);
        this.done = true;
      }
    },
    getScore: function(correct, total) {
      const score = 10 * (correct / total);
      return score;
    },
    getRank(score) {
      if (score >= 8) {
        return (this.rank = "A");
      } else if (score >= 5.5) {
        return (this.rank = "B");
      } else {
        return (this.rank = "C");
      }
    },
    increment(isCorrect) {
      if (isCorrect) {
        this.numCorrect++;
      }
    },
    async changeValue(diff, num) {
      try {
        const data = axios.get(
          `https://opentdb.com/api.php?amount=${num}&category=31&difficulty=${diff}&type=multiple`
        );
        const responses = await data;
        this.questions = responses.data.results;
        this.index = 0;
        this.mode = diff;
        (this.numCorrect = 0), (this.numTotal = num);
      } catch (error) {
        console.error(error);
      }
    }
  }
};
</script>

<style>
@font-face {
  font-family: title;
  src: url("./assets/Bangers-Regular.ttf");
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

.bg-img {
  background: url("./assets/background.png");
  background-size: 100vw;
  background-repeat: no-repeat;
  background-attachment: fixed;
}

@media (max-width: 700px) {
  .bg-img {
    background: url("./assets/bg-mobile.png");
    background-size: 100vw;
    background-repeat: no-repeat;
    background-attachment: fixed;
  }
}
</style>
