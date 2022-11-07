<template>
      <div class="box" ref="stopSpace" @click="jumpStart">
            <div class="l1">
                  <span></span>
                  <span></span>
                  <span ref="upperLight1"></span>
                  <span ref="lowerLight1"></span>
            </div>
            <div class="l2">
                  <span></span>
                  <span></span>
                  <span ref="upperLight2"></span>
                  <span ref="lowerLight2"></span>
            </div>
            <div class="l3">
                  <span></span>
                  <span></span>
                  <span ref="upperLight3"></span>
                  <span ref="lowerLight3"></span>
            </div>
            <div class="l4">
                  <span></span>
                  <span></span>
                  <span ref="upperLight4"></span>
                  <span ref="lowerLight4"></span>
            </div>
            <div class="l5">
                  <span></span>
                  <span></span>
                  <span ref="upperLight5"></span>
                  <span ref="lowerLight5"></span>
            </div>
      </div>
</template>

<script>
export default {
      data() {
            return {
                  // waitingTimechild: 0,
                  timeout1: null,
                  timeout2: null,
                  timeout3: null,
                  timeout4: null,
                  timeout5: null,
                  timeout6: null,
            };
      },
      props: ["playClicked", "delaychild", "waitingTimeChild"],
      updated() {
            if (this.playClicked) {
                  this.startRaceLight();
            }
      },
      methods: {
            startRaceLight() {
                  this.$refs.upperLight1.style.background = "#290000";
                  this.$refs.lowerLight1.style.background = "#290000";
                  this.$refs.upperLight2.style.background = "#290000";
                  this.$refs.lowerLight2.style.background = "#290000";
                  this.$refs.upperLight3.style.background = "#290000";
                  this.$refs.lowerLight3.style.background = "#290000";
                  this.$refs.upperLight4.style.background = "#290000";
                  this.$refs.lowerLight4.style.background = "#290000";
                  this.$refs.upperLight5.style.background = "#290000";
                  this.$refs.lowerLight5.style.background = "#290000";
                  let F1 = new Audio(require("../assets/F1.mp3"));
                  this.timeout1 = setTimeout(() => {
                        F1.play();
                        this.$refs.upperLight1.style.background = "#FF1801";
                        this.$refs.lowerLight1.style.background = "#FF1801";
                  }, 1000);
                  this.timeout2 = setTimeout(() => {
                        F1.play();
                        this.$refs.upperLight2.style.background = "#FF1801";
                        this.$refs.lowerLight2.style.background = "#FF1801";
                  }, 2000);
                  this.timeout3 = setTimeout(() => {
                        F1.play();
                        this.$refs.upperLight3.style.background = "#FF1801";
                        this.$refs.lowerLight3.style.background = "#FF1801";
                  }, 3000);
                  this.timeout4 = setTimeout(() => {
                        F1.play();
                        this.$refs.upperLight4.style.background = "#FF1801";
                        this.$refs.lowerLight4.style.background = "#FF1801";
                  }, 4000);
                  this.timeout5 = setTimeout(() => {
                        F1.play();
                        this.$refs.upperLight5.style.background = "#FF1801";
                        this.$refs.lowerLight5.style.background = "#FF1801";
                  }, 5000);
                  this.timeout6 = setTimeout(() => {
                        this.$refs.upperLight1.style.background = "#290000";
                        this.$refs.lowerLight1.style.background = "#290000";
                        this.$refs.upperLight2.style.background = "#290000";
                        this.$refs.lowerLight2.style.background = "#290000";
                        this.$refs.upperLight3.style.background = "#290000";
                        this.$refs.lowerLight3.style.background = "#290000";
                        this.$refs.upperLight4.style.background = "#290000";
                        this.$refs.lowerLight4.style.background = "#290000";
                        this.$refs.upperLight5.style.background = "#290000";
                        this.$refs.lowerLight5.style.background = "#290000";
                  }, this.delaychild);
            },
            jumpStart() {
                  if (
                        this.waitingTimeChild <= this.delaychild &&
                        this.playClicked
                  ) {
                        clearTimeout(this.timeout1);
                        clearTimeout(this.timeout2);
                        clearTimeout(this.timeout3);
                        clearTimeout(this.timeout4);
                        clearTimeout(this.timeout5);
                        clearTimeout(this.timeout6);
                  }
                  this.$emit("jumpStart");
            },
      },
};
</script>

<style lang="scss" scoped>
.box {
      display: flex;
      justify-content: center;
      margin: 20px;
      height: 100%;
}

@for $numofLights from 1 through 5 {
      .l#{$numofLights} {
            background-color: black;
            pointer-events: none;
            width: 50px;
            height: 250px;
            display: flex;
            flex-direction: column;
            justify-content: space-between;
            align-items: center;
            padding: 10px 5px;
            border-radius: 10px;
            margin: 5px;

            span {
                  width: 45px;
                  height: 45px;
                  border-radius: 100%;
                  background-color: #290000;
            }
      }
      @media (max-width: 750px) {
            @for $numofLights from 1 through 5 {
                  .l#{$numofLights} {
                        width: 40px;
                        height: 150px;
                        span {
                              width: 30px;
                              height: 30px;
                              border-radius: 100%;
                              background-color: #290000;
                        }
                  }
            }
      }
}
</style>
