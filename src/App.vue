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
    <button
      @click="sectionClicked('g')"
      :class="{ 'g-clicked': isGoodBye, addTransition: isAnimFinish }"
    >
      Good Bye <span></span>
    </button>
  </div>
  <transition name="moveup" mode="out-in">
    <Letter
      :key="key"
      v-if="isIconClick"
      :section="sectionNum"
      :content="letterContent"
    />
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
      isGoodBye: false,
      isAnimFinish: false,
      key: 0,
      sectionNum: 1,
      letterContent: "",
      IntroLetterContent:
        "Hi Joanna,\n" +
        "\n" +
        "Sorry, it has taken so long for me to write back. I kind of wanted to make it up to you, so I designed and coded this website. Don't judge me too harshly. I'm a pretty bad English writer and, also I'm not good at picking colors.\n" +
        "\n" +
        "Well, I think I have a lot to tell you, so I divided the letter into sections: Studies, Work, Health and Love. Spoiler alert, my love life is almost non-existent ☹. But apart from that, my life is going great.\n" +
        "\n" +
        "My family is doing great! Jorge is graduating possibly next year he is studying Computer Engineering like me (we are both a couple of nerds). But what's most important is that he loves it as much as I do.\n" +
        "My Mom is still working at school and, my Dad is still working in the same place at the position of the economic corporate executive. I'm so proud of my family! They talk pretty often about you and your family. They say the USA and you was the best experience I ever had in my life (and I agree).\n" +
        "\n" +
        "My group of friends went through a bad situation plus covid didn't help. But now we are more united than ever. I will tell you that story at another time.\n" +
        "\n" +
        "Even though this year had lots of ups and downs because of covid, I think it was good to have more time for myself. ",
      StudiesLetterContent:
        "December 2020, I finally finished my career in Software Engineering. I should have finished a year ago, but I couldn't, I wasn't feeling good, I did not have the strength because of depression (I talk more about this in the Health section).\n" +
        "Anyway, the bad time lasted a year, and then things got better I finish all the subjects with good grades and the last thing I had to do was my Final Degree Project (which is like a thesis). The project was about User Experience and Micro-Interactions on the Web. Actually, you are seeing lots of animations and micro-interaction on this web, especially when you opened the envelope at the beginning (If you want to check all the animations again, just refresh the page).\n" +
        "\n" +
        "The project took me five months to complete and I put all the effort in the world into this project. Finally, I delivered the project and presented it to a university jury. They liked it so much that they rated my project with a 9 out of 10. I was so happy and fulfilled! But I also had a bittersweet feeling because I had just finished my degree and did not know what my life would be like now.\n" +
        "So next five months I hanged out a lot with my friends and family. As well I felt like I wanted to keep improving as a web developer, so I signed up for a couple of courses (those courses were great). \n" +
        "\n" +
        "Two months after getting my actual job, I received an email from my university saying that they loved my thesis and they wanted me to give a lesson to the student and program some examples of micro-interactions. That was more exciting for me than even when I got my job.☺",
      WorkLetterContent:
        "So I finished school and I started doing courses about web development and expanding my portfolio. At the same time, I started not only coding but designing web pages. I made a couple of websites for my portfolio, my favorite it's about the Solar System:\n" +
        "https://solar-system-d831d.web.app/\n" +
        "\n" +
        "Collete used this website for teaching his students (I think that was lovely).\n" +
        "\n" +
        "So the hard part was getting a job but my Dad kinda helped. My Dad put me in contact with one of the companies of the group of companies where my father works. They liked my resume and portfolio so they got me.\n" +
        "\n" +
        "I've been working now for 5 months as a software developer and I'm so happy with my experience so far and I think they can say the same about me. The company is called Fundación ONCE and it helps disabled people to get a job and make things accessible for them.\n" +
        "\n" +
        "I worked on a few projects but the one I felt was the most important and I had more participation was in building a website for cognitively disabled people. On this project, I was able to demonstrate everything that I had practiced about web development.\n" +
        "\n" +
        "So it seems they like me at work cause last week they told me I'll be on two \"business trips\" soon. One it's to the Camino de Santiago to test an app with blind people and this September I'll be going for a week to an accessibility Bootcamp in Malaga. I'm so grateful they are giving me this opportunity.",
      LoveLetterContent:
        "Non-existent ☹\n" +
        "\n" +
        "I will be quite brief.\n" +
        "During my first year of college, I had a girlfriend and things didn't go well so we broke up. Then in my third year of college, I fell in love with another girl and I think she did too. We hung out a lot and but we never took the step (I will always regret that). So once I thought I was ready to tell her I got sick and I isolated myself from everyone, even my friends.\n" +
        "\n" +
        "About a year later I recovered, my friends were still there but she wasn't. Then I wasn't confident enough to start another relation plus I was busy with college and covid happened. \n" +
        "\n" +
        "Although I don't have a girlfriend right now I don't feel lonely I feel more supported than ever. I love my family and friends I would not change them for anything.",
      HealthLetterContent:
        "When I was in my third year of university, my friends and I went on a trip to Galicia (north of Spain). As you know here in Spain we get our driver's license when we are 18 or older. I was the only one of my friends who got his driver's license at 18 and another of my friends had just got it a few months ago.\n" +
        "\n" +
        "The weather was very bad, so the trip from Madrid to Galicia took us 10 hours. At the beginning of the trip, everything was okay, but then, the weather, my inexperienced friend driving my parent's car, and how tired I was, caused me a lot of stress.\n" +
        "\n" +
        "Then we partied for a few days in Galicia and that wasn't healthy neither plus then the trip back to Madrid... After all that I was not feeling well. I thought I'd recover soon but I didn't. Eventually, I was depressed, I didn't enjoy a movie or a tv show, I didn't enjoy food, I didn't want to hang out, I didn't enjoy my life... But somehow I never gave up.\n" +
        "\n" +
        "I went to lots of doctors and took different medications till I got in contact with one of the best doctors in Madrid and she got the medication right. It took me a while to recover but since now I have been fully recovered for a year. And now I finished college, I got a job and what's more important, now I appreciate my family and friends much more and I am grateful to them since they have been with me all the way through.",
      GoodByeLetterContent:
        "I'm sorry that the letter was so long. I have skipped some parts of the story so as not to make it excessively long but I will tell you the rest in person cause I will probably visit soon.\n" +
        "\n" +
        "You can show this website to whoever you think should see this (just copy the URL).\n" +
        "\n" +
        "I have felt very identified with your letters and way of writing. I feel that our personal experiences have made us change and matured a lot but I know that whatever happens, we will always have each other in our hearts.\n" +
        "\n" +
        "I think a lot about you, Joe, Josh, Rachel, Jonh, and Collete (and Bella of course) ♡.\n" +
        "\n" +
        "Lost of Love,\n" +
        "Miggy",
    };
  },
  methods: {
    sectionClicked(section) {
      this.key++;
      this.isIntro =
        this.isStudies =
        this.isWork =
        this.isLove =
        this.isHealth =
        this.isGoodBye =
          false;
      switch (section) {
        case "i":
          this.isIntro = true;
          this.letterContent = this.IntroLetterContent;
          this.sectionNum = 1;
          break;
        case "s":
          this.isStudies = true;
          this.letterContent = this.StudiesLetterContent;
          this.sectionNum = 2;
          break;
        case "w":
          this.isWork = true;
          this.letterContent = this.WorkLetterContent;
          this.sectionNum = 3;
          break;
        case "l":
          this.isLove = true;
          this.letterContent = this.LoveLetterContent;
          this.sectionNum = 4;
          break;
        case "h":
          this.isHealth = true;
          this.letterContent = this.HealthLetterContent;
          this.sectionNum = 5;
          break;
        default:
          this.isGoodBye = true;
          this.letterContent = this.GoodByeLetterContent;
          this.sectionNum = 6;
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
      }, 7300);
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
    this.letterContent = this.IntroLetterContent;
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
      background: #f1f0f0;
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
    &:nth-child(6) {
      background: transparent;
      box-shadow: 0px 0px 3px rgba($color: #b8b1b0, $alpha: 0.8);
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
.g-clicked {
  // border: 2px solid rgba(174, 73, 214, 1) !important;
  transform: translate(30px) !important;
}

.addTransition {
  transition: transform 0.5s ease, border 0.5s ease;
}

.moveup-enter-active {
  transition: 0.8s;
}
.moveup-leave-active {
  transition: 0.5s;
}
.moveup-enter-from/* .fade-leave-active below version 2.1.8 */ {
  transform: translate(0, 100%);
  opacity: 0;
}
.moveup-leave-to/* .fade-leave-active below version 2.1.8 */ {
  transform: translate(0, -100%);
  opacity: 0;
}
</style>
