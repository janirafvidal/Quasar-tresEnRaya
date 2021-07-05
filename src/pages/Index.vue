<template>
  <q-page padding>
    <div class="row justify-center">
      <div class="col-12 col-md-8">
        <q-card>
          <q-card-section class="bg-dark text-white">
            <div class="text-h4">TRES EN RAYA</div>
          </q-card-section>

          <q-card-section class="bg-grey-4">
            <div class="row q-col-gutter-xl">
              <div class="col-4" v-for="(btn, index) in buttons" :key="index">
                <q-btn
                  class="full-width text-h6"
                  @click="btnAction(index)"
                  :disable="clickCounter === 9"
                  :color="checkColor(buttons[index])"
                >
                  {{ btn }}
                </q-btn>
              </div>
            </div>
            <q-btn
              class="q-col-gutter-xs text-h6 q-mt-xl full-width"
              color="blue"
              padding="2px"
              align="center"
              @click="reset"
            >
              PLAY AGAIN
            </q-btn>
            <pre>{{ whosPlaying }}</pre>
          </q-card-section>
        </q-card>
      </div>
    </div>
  </q-page>
</template>

<script>
export default {
  data() {
    return {
      buttons: ["", "", "", "", "", "", "", "", ""],
      clickCounter: 0,
      whosPlaying: "",
    };
  },
  methods: {
    btnAction(valor) {
      this.clickCounter++;
      if (this.clickCounter <= 9) {
        console.log(this.buttons, valor);
        if (this.clickCounter % 2 === 0 && this.buttons[valor] === "") {
          this.buttons[valor] = "X";
          this.whosPlaying = "Now playing: Blue Team";
          console.log(this.clickCounter, this.buttons[valor]);
        } else if (this.clickCounter % 2 !== 0 && this.buttons[valor] === "") {
          this.buttons[valor] = "O";
          this.whosPlaying = "Now playing: Red Team";
          console.log(this.clickCounter, this.buttons[valor]);
        }
        this.checkWin();
      }
    },
    reset() {
      (this.buttons = ["", "", "", "", "", "", "", "", ""]),
        (this.clickCounter = 0),
        (this.whosPlaying = "");
    },
    checkWin() {
      if (
        (this.buttons[0] === this.buttons[1] &&
          this.buttons[1] === this.buttons[2] &&
          this.buttons[1] !== "") ||
        (this.buttons[3] === this.buttons[4] &&
          this.buttons[4] === this.buttons[5] &&
          this.buttons[4] !== "") ||
        (this.buttons[6] === this.buttons[7] &&
          this.buttons[7] === this.buttons[8] &&
          this.buttons[7] !== "") ||
        (this.buttons[0] === this.buttons[3] &&
          this.buttons[3] === this.buttons[6] &&
          this.buttons[3] !== "") ||
        (this.buttons[1] === this.buttons[4] &&
          this.buttons[4] === this.buttons[7] &&
          this.buttons[4] !== "") ||
        (this.buttons[2] === this.buttons[5] &&
          this.buttons[5] === this.buttons[8] &&
          this.buttons[5] !== "") ||
        (this.buttons[0] === this.buttons[4] &&
          this.buttons[4] === this.buttons[8] &&
          this.buttons[4] !== "") ||
        (this.buttons[2] === this.buttons[4] &&
          this.buttons[4] === this.buttons[6] &&
          this.buttons[4] !== "")
      ) {
        this.clickCounter = 9;
        this.whosPlaying = "Congratulations! You win!";
        return true;
      }
      return false;
    },
    checkColor(valor) {
      if (valor === "X") {
        return "blue";
      } else if (valor === "O") {
        return "red";
      } else {
        return "white";
      }
    },
  },
};
</script>
