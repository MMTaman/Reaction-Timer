<template>
      <div class="options">
            <button class="button-20" @click="startGame" :disabled="isPlaying">
                  Play
            </button>
            <div class="howto" v-show="howto">
                  How to Play: press anywhere on the screen below the play
                  button
            </div>
            <resultBox v-show="showTime">
                  <div v-show="showScore">Your Speed: {{ yourTime }}ms</div>
                  <div failed v-show="jumped">You Jump Started !</div>
            </resultBox>
      </div>
      <lightsRace
            @click="endGame"
            :playClicked="isPlaying"
            :waitingTimeChild="waitingTime"
            :delaychild="delay"
            @jumpStart="stopGame"
      />
</template>
<script>
import resultBox from "./components/result-box.vue";
import lightsRace from "./components/lights-race.vue";
export default {
      name: "App",
      components: {
            resultBox,
            lightsRace,
      },
      data() {
            return {
                  isPlaying: false,
                  howto: true,
                  showTime: false,
                  showScore: false,
                  jumped: false,
                  showTextInsideLights: false,
                  delay: 0,
                  yourTime: 0,
                  startingTimeInterval: null,
                  waitingTime: 0,
                  waitingTimeChild: 0,
                  waitingInterval: null,
                  startingTimeout: null,
            };
      },
      methods: {
            beforeStart() {
                  this.waitingInterval = setInterval(() => {
                        if (this.waitingTimeChild >= this.delay) {
                              clearInterval(this.waitingInterval);
                        }
                        this.waitingTimeChild += 10;
                        console.log(this.waitingTimeChild);
                  }, 10);
            },
            stopGame() {
                  if (this.isPlaying) {
                        clearInterval(this.waitingInterval);
                        clearInterval(this.startingTimeInterval);
                        clearTimeout(this.startingTimeout);
                        (this.isPlaying = false),
                              (this.playClicked = this.isPlaying);
                        (this.howto = !this.isPlaying), (this.delay = 0);
                        this.delaychild = this.delay;
                        this.showTime = true;
                        this.showScore = false;
                        this.jumped = true;
                  }
            },
            startGame() {
                  this.beforeStart();
                  this.waitinTimeChild = 0;
                  this.isPlaying = true;
                  (this.howto = !this.isPlaying),
                        (this.playClicked = this.isPlaying);
                  this.yourTime = 0;
                  this.showTime = false;
                  this.delay = 6000 + Math.ceil(Math.random() * 3000);
                  this.delaychild = this.delay;
                  console.log(this.delay);
                  this.startingTimeout = setTimeout(() => {
                        this.startingTimeInterval = setInterval(() => {
                              this.yourTime += 10;
                        }, 10);
                        this.showTextInsideLights = true;
                        this.showScore = true;
                  }, this.delay);
            },
            endGame() {
                  if (this.yourTime != 0) {
                        this.isPlaying = false;
                        (this.howto = !this.isPlaying),
                              (this.playClicked = this.isPlaying);
                        this.showTime = true;
                        this.showTextInsideLights = false;
                        this.showScore = true;
                        this.jumped = false;
                        clearInterval(this.startingTimeInterval);
                  }
            },
      },
};
</script>

<style lang="scss">
$bgColor: #8898ac;
$textColor: #dc0000;
$fancy: #00d2be;
$LightsColor: #ff1801;

body {
      background: $bgColor;
}

#app {
      padding-top: 100px;
      font-family: "Inter Tight", sans-serif;
      text-align: center;
      // background: red;
      height: 480px;
      overflow-y: hidden;

      .options {
            display: flex;
            flex-direction: column;
            justify-content: space-between;
            align-items: center;
            width: 100%;
      }

      .button-20 {
            appearance: button;
            width: fit-content;
            color: $textColor;
            background-color: $fancy;
            background-image: linear-gradient(
                  180deg,
                  rgba(255, 255, 255, 0.15),
                  rgba(255, 255, 255, 0)
            );
            border: 1px solid $fancy;
            border-radius: 1rem;
            box-shadow: rgba(255, 255, 255, 0.15) 0 1px 0 inset,
                  rgba(46, 54, 80, 0.075) 0 1px 1px;
            box-sizing: border-box;
            cursor: pointer;
            display: inline-block;
            font-family: Inter, sans-serif;
            font-size: 1rem;
            font-weight: 500;
            line-height: 1.5;
            margin: 10px;
            padding: 0.5rem 1rem;
            text-align: center;
            text-transform: none;
            transition: color 0.15s ease-in-out,
                  background-color 0.15s ease-in-out,
                  border-color 0.15s ease-in-out, box-shadow 0.15s ease-in-out;
            user-select: none;
            -webkit-user-select: none;
            touch-action: manipulation;
            vertical-align: middle;
      }

      .button-20:focus:not(:focus-visible),
      .button-20:focus {
            outline: 0;
      }

      .button-20:hover {
            background-color: $LightsColor;
            border-color: $LightsColor;
      }

      .button-20:active:focus {
            box-shadow: rgba(46, 54, 80, 0.125) 0 3px 5px inset,
                  rgba(104, 101, 235, 0.5) 0 0 0 0.2rem;
      }

      .button-20:disabled {
            background-image: none;
            box-shadow: none;
            opacity: 0.65;
            cursor: not-allowed;
      }
      .howto {
            font-size: 20px;
            color: $fancy;
            padding: 10px;
            @media (max-width: 750px) {
                  font-size: 20px;
            }
      }
}
</style>
