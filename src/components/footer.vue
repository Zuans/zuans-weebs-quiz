<template>
  <div class="footer py-2">
    <h4 class="text-white">
      Made with
      <font-awesome class="heart mx-2" icon="heart" />By Zuans &copy;2020
    </h4>
  </div>
</template>

<script>
export default {
  name: "Footer"
};
</script>

<style scoped >
/* @media (max-wdith: 700px) {
  .footer {
    position: relative;
  }
} */
.footer {
  background-color: #292b2c;
  width: 100%;
  position: fixed;
  bottom: 0;
  font-family: title;
  box-sizing: content-box;
}

.heart {
  color: rgb(255, 0, 140);
}
</style>