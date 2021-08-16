<template>
  <MatrizGame
    :mat="mat"
    @leftPress="leftPress"
    @rightPress="rightPress"
    @downPress="downPress"
    @upPress="upPress"
    @startGame="startGame"
  />
</template>

<script>
import MatrizGame from "./components/MatrizGame.vue";
export default {
  name: "App",
  components: { MatrizGame },
  data() {
    return {
      mat: [
        [null, null, null, null],
        [null, null, null, null],
        [null, null, null, null],
        [null, null, null, null],
      ],
      maxNumber: 2,
      gameOver: false,
    };
  },
  methods: {
    leftPress() {
      // Remove os espaços nulos
      for (let r = 0; r < 4; r++) {
        for (let c = 0; c < 4; c++) {
          if (c != 0) {
            if (this.mat[r][c] != null) {
              let value = this.mat[r][c];
              for (let i = c - 1; i >= 0; i--) {
                if (this.mat[r][i] == null) {
                  this.mat[r][i] = value;
                  this.mat[r][i + 1] = null;
                }
              }
            }
          }
        }
      }
      // Soma os valores
      for (let r = 0; r < 4; r++) {
        for (let c = 0; c < 4; c++) {
          if (c != 3) {
            if (this.mat[r][c] != null) {
              if (this.mat[r][c] == this.mat[r][c + 1]) {
                this.mat[r][c] += this.mat[r][c];
                this.maxNumber <= this.mat[r][c]
                  ? (this.maxNumber = this.mat[r][c])
                  : null;
                for (let i = c + 1; i < 4; i++) {
                  this.mat[r][i] = this.mat[r][i + 1];
                }
              }
            }
          }
        }
      }
      this.addNumber();
    },
    rightPress() {
      // Remove os espaços nulos
      for (let r = 0; r < 4; r++) {
        for (let c = 3; c >= 0; c--) {
          if (c != 3) {
            if (this.mat[r][c] != null) {
              let value = this.mat[r][c];
              for (let i = c; i < 4; i++) {
                if (this.mat[r][i] == null) {
                  this.mat[r][i] = value;
                  this.mat[r][i - 1] = null;
                }
              }
            }
          }
        }
      }
      // Soma os valores
      for (let r = 0; r < 4; r++) {
        for (let c = 3; c >= 0; c--) {
          if (c != 0) {
            if (this.mat[r][c] != null) {
              if (this.mat[r][c] == this.mat[r][c - 1]) {
                this.mat[r][c] += this.mat[r][c];
                this.maxNumber <= this.mat[r][c]
                  ? (this.maxNumber = this.mat[r][c])
                  : null;
                for (let i = c - 1; i >= 0; i--) {
                  this.mat[r][i] = this.mat[r][i - 1];
                }
              }
            }
          }
        }
      }
      this.addNumber();
    },
    downPress() {
      // Remove os espaços nulos
      for (let c = 0; c < 4; c++) {
        for (let r = 3; r >= 0; r--) {
          if (r != 3) {
            if (this.mat[r][c] != null) {
              let value = this.mat[r][c];
              for (let i = r + 1; i < 4; i++) {
                if (this.mat[i][c] == null) {
                  this.mat[i][c] = value;
                  this.mat[i - 1][c] = null;
                }
              }
            }
          }
        }
      }
      // Soma os valores
      for (let c = 0; c < 4; c++) {
        for (let r = 3; r >= 0; r--) {
          if (r != 0) {
            if (this.mat[r][c] != null) {
              if (this.mat[r][c] == this.mat[r - 1][c]) {
                this.mat[r][c] += this.mat[r][c];
                this.maxNumber <= this.mat[r][c]
                  ? (this.maxNumber = this.mat[r][c])
                  : null;
                for (let i = r - 1; i >= 0; i--) {
                  i > 0
                    ? (this.mat[i][c] = this.mat[i - 1][c])
                    : (this.mat[i][c] = null);
                }
              }
            }
          }
        }
      }
      this.addNumber();
    },
    upPress() {
      // Remove os espaços nulos
      for (let c = 0; c < 4; c++) {
        for (let r = 0; r < 4; r++) {
          if (r != 0) {
            if (this.mat[r][c] != null) {
              let value = this.mat[r][c];
              for (let i = r - 1; i >= 0; i--) {
                if (this.mat[i][c] == null) {
                  this.mat[i][c] = value;
                  this.mat[i + 1][c] = null;
                }
              }
            }
          }
        }
      }
      // Soma os valores
      for (let c = 0; c < 4; c++) {
        for (let r = 0; r < 4; r++) {
          if (r != 3) {
            if (this.mat[r][c] != null) {
              if (this.mat[r][c] == this.mat[r + 1][c]) {
                this.mat[r][c] += this.mat[r][c];
                this.maxNumber <= this.mat[r][c]
                  ? (this.maxNumber = this.mat[r][c])
                  : null;
                for (let i = r + 1; i < 4; i++) {
                  i < 3
                    ? (this.mat[i][c] = this.mat[i + 1][c])
                    : (this.mat[i][c] = null);
                }
              }
            }
          }
        }
      }
      this.addNumber();
    },
    addNumber() {
      let arrayNull = [];
      let count = 0;
      let idx = 0;
      for (let r = 0; r < 4; r++) {
        for (let c = 0; c < 4; c++) {
          count++;
          this.mat[r][c] == null ? arrayNull.push(count) : null;
        }
      }

      if (arrayNull.length > 0) {
        idx = arrayNull[Math.floor(Math.random() * arrayNull.length)];

        count = 0;
        for (let r = 0; r < 4; r++) {
          for (let c = 0; c < 4; c++) {
            count++;
            idx == count ? (this.mat[r][c] = this.generateNumber()) : null;
          }
        }
      } else {
        this.gameOver = true;
      }
    },
    startGame() {
      this.maxNumber = 2;
      this.gameOver = false;
      this.addNumber();
      this.addNumber();
    },
    generateNumber() {
      console.log("teste");
      let divisor = 0;
      let count = 0;
      let countAnt = 0;
      let arrayFibonacci = [];
      divisor = this.maxNumber;
      do {
        if (divisor == this.maxNumber) {
          count = 1;
        } else {
          count += countAnt;
        }
        for (let i = countAnt; i < count; i++) {
          arrayFibonacci.push(divisor)  
          console.log(arrayFibonacci)
        }
        countAnt = count
        divisor = divisor / 2;
      } while (divisor != 1);
      return arrayFibonacci[Math.floor(Math.random() * arrayFibonacci.length)];
    },
  },
};
</script>

