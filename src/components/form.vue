<template>
  <div>
    <form>
      <label class="mt-4" for="exampleFormControlSelect1">
        <h5 class="text-white">Amount Question</h5>
      </label>
      <select class="form-control" v-model="numQuest" id="exampleFormControlSelect1">
        <option>5</option>
        <option>10</option>
        <option>15</option>
        <option>20</option>
        <option>25</option>
      </select>
      <label class="mt-4" for="exampleFormControlSelect1">
        <h5 class="text-white">Level of Difficult</h5>
      </label>
      <select class="form-control" v-model="difficult" id="exampleFormControlSelect1">
        <option>Easy</option>
        <option>Medium</option>
        <option>Hard</option>
      </select>
      <button @click="submitValue" class="btn mt-5 btn-primary">Submit</button>
    </form>
  </div>
</template>

<script>
export default {
  name: "Form",
  props: {
    changeValue: Function,
    submitted: Function
  },
  data() {
    return {
      numQuest: 15,
      difficult: "Easy"
    };
  },
  methods: {
    submitValue() {
      const lowDiff = this.difficult.toLowerCase();
      this.submitted();
      this.changeValue(lowDiff, this.numQuest);
    }
  },
  computed: {}
};
</script>

<style>
</style>