<template>
  <LetterIcon @clicked="showLetter" />
  <div class="sections">
    <button>Intro</button>
    <button>Studies</button>
    <button>Work</button>
    <button>Love</button>
    <button>Health</button>
  </div>
  <transition name="moveup">
    <Letter v-if="isIconClick" />
  </transition>
</template>

<script>
import LetterIcon from "./components/LetterIcon.vue";
import Letter from "./components/Letter.vue";
import gsap from "gsap";
export default {
  name: "App",
  components: {
    LetterIcon,
    Letter,
  },
  data() {
    return {
      isIconClick: false,
      tl: null,
    };
  },
  methods: {
    showLetter() {
      setTimeout(() => {
        this.isIconClick = true;
      }, 4000);
      setTimeout(() => {
        this.tl.resume();
      }, 4800);
    },
  },
  mounted() {
    let tl = gsap.timeline();
    tl.from(".sections button", {
      x: -80,
      opacity: 0,
      stagger: 0.2,
      duration: 1,
      ease: "back",
    });
    tl.pause();
    this.tl = tl;

  },
};
</script>

<style lang="scss">
@import url("https://fonts.googleapis.com/css2?family=Yomogi&display=swap");

*,
*::before,
*::after {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  overflow-x: hidden;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  width: 100vw;
  display: flex;
  justify-content: center;
  padding-right: 3em;
  padding-left: 11em;
  padding-top: 2.5em;
}

.sections {
  position: absolute;
  left: 2.5em;
  top: 13em;
  display: flex;
  flex-direction: column;
  gap: 2em;
  button {
    border-radius: 2rem;
    padding: 0.5em 2em;
    border: 1px solid #4484f4;
    background: white;
    font-family: "Yomogi", cursive;
    font-size: 1em;
    font-weight: 500;
    color: black;
    cursor: pointer;

    &:nth-child(2) {
      border: 1px solid #7ed448;
    }
    &:nth-child(3) {
      border: 1px solid #f1ad3e;
    }
    &:nth-child(4) {
      border: 1px solid #e962ac;
    }
    &:nth-child(5) {
      border: 1px solid #ae49d6;
    }
  }
}

.moveup-enter-active {
  transition: 0.8s;
}
.moveup-enter-from/* .fade-leave-active below version 2.1.8 */ {
  transform: translate(0, 100%);
  opacity: 0;
}
</style>
