<template>
  <div class="letter">
    <div class="hole1"></div>
    <div class="hole2"></div>
    <div class="hole3"></div>
    <div class="hole4"></div>
    <p>{{ content }}</p>
  </div>
</template>

<script>
export default {
  name: "Letter",
  data() {
    return {
      content:
        "Hi Joanna,\n\n Sorry it has taken so long for me to write back.\
        I kind of wanted to make it up to you so I designed and coded this website.\
        Don't judge me too harsh, I'm pretty bad designer and writter",
    };
  },
};
</script>

<style lang="scss" scoped>
.letter {
  width: 50%;
  height: 90vh;
  background-color: #fdfeff;
  background-image: url("https://www.transparenttextures.com/patterns/lined-paper-2.png");
  border-radius: 5px;
  box-shadow: 0px 0px 5px rgba($color: #b8b1b0, $alpha: 0.4);
  position: relative;
  padding: 4rem 3rem 3rem 8rem;

  &:after {
    content: "";
    height: 2px;
    position: absolute;
    left: 0;
    right: 0;
    clip-path: polygon(
      0% 0%,
      5% 100%,
      10% 0%,
      15% 100%,
      20% 0%,
      25% 100%,
      30% 0%,
      35% 100%,
      40% 0%,
      45% 100%,
      50% 0%,
      55% 100%,
      60% 0%,
      65% 100%,
      70% 0%,
      75% 100%,
      80% 0%,
      85% 100%,
      90% 0%,
      95% 100%,
      100% 0%
    );
  }
  &:after {
    background-color: #fdfeff;
    bottom: -2px;
  }

  p {
    font-family: "Yomogi", cursive;
    font-size: 1.2em;
    font-weight: 500;
    color: black;
    text-align: start;
    white-space: pre-line;
  }

  &::before {
    content: "";
    height: inherit;
    width: 2px;
    position: absolute;
    background: #dea5a4;
    left: 6em;
    top: 0;
  }

  .hole1,
  .hole2,
  .hole3,
  .hole4 {
    position: absolute;
    width: 1.2em;
    height: 1.2em;
    background: #fcf4f2;
    box-shadow: inset 0 5px 5px 2px rgba(184, 177, 176, 0.5);
    border-radius: 50%;
    left: 2.5em;
    z-index: 3;
  }

  .hole1 {
    top: 12%;
  }
  .hole2 {
    top: 37%;
  }
  .hole3 {
    top: 62%;
  }
  .hole4 {
    top: 87%;
  }

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
