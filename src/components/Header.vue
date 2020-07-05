<template>
  <div>
    <div>
      <b-navbar toggleable="lg" type="dark" class="navbar" variant="info">
        <b-navbar-brand href="#">Weaboo Quiz Score: {{ numCorrect }}/{{ numTotal }}</b-navbar-brand>
      </b-navbar>
    </div>
  </div>
</template>

<script>
export default {
  name: "Header",
  props: ["numCorrect", "numTotal"]
};
</script>

<style scoped>
.navbar {
  margin-top: -4rem;
  position: fixed;
  width: 100%;
  z-index: 999;
}
</style>
