<template>
  <div ref="letter" class="letter">
    <div ref="line" class="line"></div>
    <div class="hole h1"></div>
    <div class="hole h2"></div>
    <div class="hole h3"></div>
    <div class="hole h4"></div>
    <p>{{ content }}</p>
    <img class="hart" v-if="section === 1" src="@/assets/hart.png" alt="hart" />
    <img class="lazo" v-if="section === 2" src="@/assets/lazo.png" alt="lazo" />
    <img class="rama" v-if="section === 3" src="@/assets/rama.png" alt="rama" />
    <img
      class="arrowhart"
      v-if="section === 4"
      src="@/assets/arrowhart.png"
      alt="arrowhart"
    />
    <img
      class="flechalazo"
      v-if="section === 5"
      src="@/assets/flechalazo.png"
      alt="flechalazo"
    />
    <img
      class="firma"
      v-if="section === 6"
      src="@/assets/firma.png"
      alt="firma"
    />
  </div>
</template>

<script>
export default {
  name: "Letter",
  props: {
    content: {
      type: String,
      required: true,
    },
    section: {
      type: Number,
      required: true,
      default: 1,
    },
  },
  watch: {
    content() {
      this.resizeLetterElements();
    },
  },
  methods: {
    removeElementsByClass(className) {
      const elements = document.getElementsByClassName(className);
      while (elements.length > 0) {
        elements[0].parentNode.removeChild(elements[0]);
      }
    },
    resizeLetterElements() {
      this.removeElementsByClass("newHole");
      this.$nextTick(() => {
        this.$refs.line.style.height = "0px";
        const increase =
          this.$refs.letter.scrollHeight -
          this.$refs.letter.offsetHeight * 0.87;
        const numberOfHoles =
          ((increase / (this.$refs.letter.offsetHeight * 0.87)) * 100) / 25;
        for (let i = 1; i < Math.floor(numberOfHoles); i++) {
          let newHole = document.createElement("div");
          newHole.classList.add("newHole");
          let topDistance = 87 + i * 25;
          newHole.style.cssText = `
            position: absolute;
            width: 1.2em;
            height: 1.2em;
            background: #f1f0f0;
            box-shadow: inset 0 5px 5px 2px rgba(184, 177, 176, 0.5);
            border-radius: 50%;
            left: 2.5em;
            z-index: 3;
            top: ${topDistance}%;
          `;
          this.$refs.letter.appendChild(newHole);
        }

        this.$refs.line.style.height = this.$refs.letter.scrollHeight + "px";
      });
    },
  },
  mounted() {
    const increase =
      this.$refs.letter.scrollHeight - this.$refs.letter.offsetHeight * 0.87;
    const numberOfHoles =
      ((increase / (this.$refs.letter.offsetHeight * 0.87)) * 100) / 25;
    for (let i = 1; i < Math.floor(numberOfHoles); i++) {
      let newHole = document.createElement("div");
      newHole.classList.add("newHole");
      let topDistance = 87 + i * 25;
      newHole.style.cssText = `
        position: absolute;
        width: 1.2em;
        height: 1.2em;
        background: #f1f0f0;
        box-shadow: inset 0 5px 5px 2px rgba(184, 177, 176, 0.5);
        border-radius: 50%;
        left: 2.5em;
        z-index: 3;
        top: ${topDistance}%;
      `;
      this.$refs.letter.appendChild(newHole);
    }

    this.$refs.line.style.height = this.$refs.letter.scrollHeight + "px";

    window.onresize = this.resizeLetterElements;
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
  overflow-y: auto;
  overflow-x: hidden;

  &::-webkit-scrollbar-track {
    border-radius: 10px;
    background: transparent;
  }
  &::-webkit-scrollbar {
    width: 8px;
    background: transparent;
    border-radius: 10px;
  }
  &::-webkit-scrollbar-thumb {
    border-radius: 5px;
    border: 2px solid #d5dbe0;
    background-color: #d5dbe070;
  }
  &::-webkit-scrollbar-track-piece:start {
    margin-top: 12px;
  }
  &::-webkit-scrollbar-track-piece:end {
    margin-bottom: 12px;
  }

  p {
    font-family: "Yomogi", cursive;
    font-size: 1.2em;
    font-weight: 500;
    color: black;
    text-align: start;
    white-space: pre-line;
  }

  img {
    position: absolute;
    top: 0.5em;
    right: 4em;
    height: auto;
  }

  .lazo,
  .rama {
    top: 1.5em;
    width: 13em;
  }

  .arrowhart {
    top: 1.5em;
    width: 8em;
    height: auto;
  }
  .flechalazo {
    top: 1.5em;
    width: 7em;
    height: auto;
  }

  .hart {
    top: 2em;
    width: 13em;
  }

  .firma {
    position: static;
    width: 10em;
    height: auto;
  }

  .line {
    width: 2px;
    position: absolute;
    background: #dea5a4;
    left: 6em;
    top: 0;
    bottom: 0;
  }

  .hole {
    position: absolute;
    width: 1.2em;
    height: 1.2em;
    background: #f1f0f0;
    box-shadow: inset 0 5px 5px 2px rgba(184, 177, 176, 0.5);
    border-radius: 50%;
    left: 2.5em;
    z-index: 3;
  }

  .h1 {
    top: 12%;
  }
  .h2 {
    top: 37%;
  }
  .h3 {
    top: 62%;
  }
  .h4 {
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
