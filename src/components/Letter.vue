<template>
  <div class="letter">
    <p></p>
  </div>
</template>

<script>
export default {
  name: "Letter",
};
</script>

<style lang="scss" scoped>
.letter {
  width: 50%;
  height: 90vh;
  border: 1px solid #4484f4;
  border-radius: 5px;

  @media (max-width: 1350px) {
    width: 60%;
  }
  @media (max-width: 1150px) {
    width: 75%;
  }
  @media (max-width: 950px) {
    width: 85%;
  }
  @media (max-width: 750px) {
    width: 95%;
  }
  @media (max-width: 550px) {
    width: 100%;
  }
}
</style>