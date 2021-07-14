<template>
  <LetterIcon @clicked="showLetter" />
  <div class="sections">
    <button
      @click="sectionClicked('i')"
      :class="{ 'i-clicked': isIntro, addTransition: isAnimFinish }"
    >
      Intro <span></span>
    </button>
    <button
      @click="sectionClicked('s')"
      :class="{ 's-clicked': isStudies, addTransition: isAnimFinish }"
    >
      Studies <span></span>
    </button>
    <button
      @click="sectionClicked('w')"
      :class="{ 'w-clicked': isWork, addTransition: isAnimFinish }"
    >
      Work <span></span>
    </button>
    <button
      @click="sectionClicked('l')"
      :class="{ 'l-clicked': isLove, addTransition: isAnimFinish }"
    >
      Love <span></span>
    </button>
    <button
      @click="sectionClicked('h')"
      :class="{ 'h-clicked': isHealth, addTransition: isAnimFinish }"
    >
      Health <span></span>
    </button>
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
      isIntro: false,
      isStudies: false,
      isWork: false,
      isLove: false,
      isHealth: false,
      isAnimFinish: false,
    };
  },
  methods: {
    sectionClicked(section) {
      this.isIntro =
        this.isStudies =
        this.isWork =
        this.isLove =
        this.isHealth =
          false;
      switch (section) {
        case "i":
          this.isIntro = true;
          break;
        case "s":
          this.isStudies = true;
          break;
        case "w":
          this.isWork = true;
          break;
        case "l":
          this.isLove = true;
          break;
        default:
          this.isHealth = true;
          break;
      }

      console.log(this.isIntro);
    },
    showLetter() {
      setTimeout(() => {
        this.isIconClick = true;
      }, 4000);
      setTimeout(() => {
        this.tl.resume();
        this.$nextTick(() => {
          this.isIntro = true;
        });
      }, 5000);
      setTimeout(() => {
        this.isAnimFinish = true;
      }, 7000);
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
  background-color: #fcf4f2;
  background-image: url("https://www.transparenttextures.com/patterns/polaroid.png");
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
    border-radius: 2px;
    padding: 0.5em 2em;
    // border: 2px solid #fcf4f2;
    border: none;
    font-family: "Yomogi", cursive;
    font-size: 1em;
    font-weight: 500;
    color: black;
    cursor: pointer;
    display: block;
    position: relative;

    &::before {
      content: "";
      position: absolute;
      left: 0.35rem;
      top: 0.7rem;
      width: 0.6rem;
      height: 0.6rem;
      border-radius: 50%;
      background: #F1F0F0;
      box-shadow: inset 0 2px 2px 1px rgba(184, 177, 176, 0.5);
    }

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

    span {
      position: absolute;
      height: 100%;
      width: 1.2px;
      position: absolute;
      background: #dea5a4;
      left: 1.3em;
      top: 0;
    }

    &:nth-child(1) {
      background: #b5ceff;
      background-image: url("https://www.transparenttextures.com/patterns/lined-paper-2.png");
      &:after {
        background-color: #b0c5ee;
        bottom: -2px;
      }
    }

    &:nth-child(2) {
      background: #c9e7ae;
      background-image: url("https://www.transparenttextures.com/patterns/lined-paper-2.png");
      &:after {
        background-color: #c9e7ae;
        bottom: -2px;
      }
    }
    &:nth-child(3) {
      background: #f7d7aa;
      background-image: url("https://www.transparenttextures.com/patterns/lined-paper-2.png");
      &:after {
        background-color: #f7d7aa;
        bottom: -2px;
      }
    }
    &:nth-child(4) {
      background: #f4b9d6;
      background-image: url("https://www.transparenttextures.com/patterns/lined-paper-2.png");
      &:after {
        background-color: #f4b9d6;
        bottom: -2px;
      }
    }
    &:nth-child(5) {
      background: #ddafe7;
      background-image: url("https://www.transparenttextures.com/patterns/lined-paper-2.png");
      &:after {
        background-color: #ddafe7;
        bottom: -2px;
      }
    }
  }
}

.i-clicked {
  // border: 2px solid rgba(68, 132, 244, 1) !important;
  transform: translate(30px) !important;
}
.s-clicked {
  // border: 2px solid rgba(126, 212, 72, 1) !important;
  transform: translate(30px) !important;
}
.w-clicked {
  // border: 2px solid rgba(241, 173, 62, 1) !important ;
  transform: translate(30px) !important;
}
.l-clicked {
  // border: 2px solid rgba(233, 98, 172, 1) !important ;
  transform: translate(30px) !important;
}
.h-clicked {
  // border: 2px solid rgba(174, 73, 214, 1) !important;
  transform: translate(30px) !important;
}

.addTransition {
  transition: transform 0.5s ease, border 0.5s ease;
}

.moveup-enter-active {
  transition: 0.8s;
}
.moveup-enter-from/* .fade-leave-active below version 2.1.8 */ {
  transform: translate(0, 100%);
  opacity: 0;
}
</style>
