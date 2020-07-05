<template>
  <section id="rank">
    <div v-if=" rank == 'A'">
      <div class="jumbotron">
        <h3 class="text-white">Terimkasih telah mampir</h3>
        <img class="img-score" src="../assets/awesome.jpg" alt />
        <p class="mt-3 lead text-white">Yeay.. Quiz nya sudah selesai</p>
        <hr class="my-4" />
        <h1 class="mt-2 text-white">Awesome</h1>
        <h5 class="text-white mt-2">
          RANK:
          <h4 class="d-inline">{{ rank }}</h4>
        </h5>
        <h5 class="text-white mt-2">
          MODE:
          <h4 class="d-inline">{{ capitalize }}</h4>
        </h5>
        <p class="text-white mt-2">Kamu sangat hebat menjadi wibu pertahankan teruss yaaa....</p>
        <button class="btn btn-success" @click="back">Back</button>
      </div>
    </div>
    <div v-else-if=" rank == 'B'">
      <div class="jumbotron">
        <h3 class="text-white">Terimkasih telah mampir</h3>
        <img class="img-score" src="../assets/nice.jpg" alt />
        <p class="mt-3 lead text-white">Yeay.. Quiz nya sudah selesai</p>
        <hr class="my-4" />
        <h1 class="mt-2 text-white">Good</h1>
        <h5 class="text-white mt-2">
          RANK:
          <h4 class="d-inline">{{ rank }}</h4>
        </h5>
        <h5 class="text-white mt-2">
          MODE:
          <h4 class="d-inline">{{ capitalize }}</h4>
        </h5>
        <p class="text-white mt-2">Good job tingkat kan terus ilmu kewibuan kamu</p>
        <button class="btn btn-success" @click="back">Back</button>
      </div>
    </div>
    <div v-if=" rank == 'C'">
      <div class="jumbotron">
        <h3 class="text-white">Terimkasih telah mampir</h3>
        <img class="img-score" src="../assets/angry.jpg" alt />
        <p class="mt-3 lead text-white">Yeay.. Quiz nya sudah selesai</p>
        <hr class="my-4" />
        <h4 class="mt-2 text-white">Too Bad...</h4>
        <h5 class="text-white mt-2">
          RANK:
          <h4 class="d-inline">{{ rank }}</h4>
        </h5>
        <h5 class="text-white mt-2">
          MODE:
          <h4 class="d-inline">{{ capitalize }}</h4>
        </h5>

        <p
          class="mt-2 text-white"
        >Kamu belum menjadi wibu sejati perkuat lah jiwa nolep mu jangan sampai kamu dimarahin emillia-tan lagi</p>
        <button class="btn btn-success" @click="back">Back</button>
      </div>
    </div>
  </section>
</template>

<script>
export default {
  name: "doneQuiz",
  props: {
    rank: String,
    mode: String
  },
  methods: {
    back() {
      location.reload();
    }
  },
  computed: {
    capitalize: function() {
      let string = this.mode.toUpperCase();
      return string;
    }
  }
};
</script>

<style scoped >
.jumbotron {
  background-color: rgba(90, 89, 89, 0.651);
}
.img-score {
  width: 55%;
  border-radius: 10px;
  margin-top: 1.5rem;
  box-shadow: 2px 2px 10px rgb(77, 74, 74);
}
</style>