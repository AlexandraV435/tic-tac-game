<template>
  <div class="container">
    <div class="play-ground">
      <div class="players">
        <table>
          <tbody>
            <tr>
              <td>
                <div :class="{'activePlayer' : activePlayer == 'x'}">
                  <i>x</i>
                  <span ></span>
                </div>
              </td>
              <td>
                <div :class="{'activePlayer' : activePlayer == 'o'}">
                  <i>o</i>
                  <span ></span>
                </div>
              </td>
            </tr>
          </tbody>
        </table>
      </div>
      <p>
        It is <span>{{activePlayer}}</span> turn!
      </p>
      <div class="play">
 
        <table>
          <tbody>
            <tr>
              <td @click ="fillInCell(0)" id="cell_0"></td>
              <td @click ="fillInCell(1)" id="cell_1"></td>
              <td @click ="fillInCell(2)" id="cell_2"></td>
            </tr>
            <tr>
              <td @click ="fillInCell(3)" id="cell_3"></td>
              <td @click = "fillInCell(4)" id="cell_4"></td>
              <td @click ="fillInCell(5)" id="cell_5"></td>
            </tr>
            <tr>
              <td @click ="fillInCell(6)" id="cell_6"></td>
              <td @click ="fillInCell(7)" id="cell_7"></td>
              <td @click ="fillInCell(8)" id="cell_8"></td>
            </tr>
          </tbody>
        </table>
      </div>
      <div>
        <button  @click="replay()">REPLAY</button>
      </div>
    </div>
  </div>
  <div class="result-overlay" id="result-overlay">
      <button @click="replay()">REPLAY</button>
      <p id="p-overlay">
        <span class="winner">
          <i v-if="winner == ''">No one</i>
          <i v-if="winner == 'x'">x</i>
          <i v-if="winner == 'o'">o</i>
        </span>
          WON
      </p>
  
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  props: {
    msg: String,

  },
  data() {
    return {
      activePlayer: 'x',
      cells: [
        null,
        null,
        null,
        null,
        null,
        null,
        null,
        null,
        null,
      ],
      countClicks: 0,
      winnigConductions: [
        [0, 1, 2],
        [3, 4, 5],
        [6, 7, 8],
        [0, 3, 6],
        [1, 4, 7],
        [2, 5, 8],
        [0, 4, 8],
        [7, 4, 6],
      ],
      winner: ''
    }
  },
  methods: {
    fillInCell(id) {
      let cellName = "cell_" + id;
      let cell = document.getElementById(cellName);
      if (this.cells[id] == null) {
        this.countClicks += 1;
        if (this.activePlayer == 'x') {
          cell.innerHTML = "<i'>x</i>";
        } else {
          cell.innerHTML = "<i style='color:#f2ebd3'>o</i>";
        }
        this.cells[id] = this.activePlayer;
        this.activePlayer = this.activePlayer == "x" ? "o" : "x";

        if(this.countClicks >= 5) {
          this.checkGame();
        }
      }
    },
    checkGame() {
      for (let i = 0; i <= 7; i++) {
        let winnigConduction = this.winnigConductions[i];
        let a = this.cells[winnigConduction[0]];
        let b = this.cells[winnigConduction[1]];
        let c = this.cells[winnigConduction[2]];
        console.log(winnigConduction)


        if (a == null || b == null || c == null) {
          continue
        }
        if (a == b && b == c) {
          this.winner = a;
        }
      }

      if (this.winner) {
        document.getElementById("result-overlay").style.display = "block";
      }
      else {
        if (this.countClicks == 9) {
          document.getElementById("result-overlay").style.display = "block";
        }
      }
    },

    replay() {
      location.reload();
    }
  }
}
</script>

<style scoped>

  body {
    background: black;
  }

  #cell_2, #cell_5, #cell_8 {
    border-right: 0;
  }

  #cell_0, #cell_1, #cell_2 {
    border-top: 0;
  }

  #cell_0, #cell_3, #cell_6 {
    border-left: 0;
  }
  
  #cell_6, #cell_7, #cell_8 {
    border-bottom: 0;
  }

  .result-overlay button {
    position: relative;
    top: 350px;
    margin: 10px; 

  }
  .circle {
    color: #f2ebd3
  }

  button {
    padding: 0;
    border: none;
    font: inherit;
    color: inherit;
    background-color: transparent;
    cursor: pointer;
    font-weight: 500;
    font-size: 20px;
    border: 1px solid;
    border-radius: 10px;
    padding: 5px;
    margin: 5px;
  }
  .activePlayer
    {
      border-bottom:3px solid #14bdac !important;
      box-shadow: 0 4px 5px rgba(0,0,0,.16) !important;
    }
   .players div {
      width: 200px;
      border-bottom: 3px solid transparent;
      color: rgba(0,0,0,.54);
      font-size: 24px;
      margin: 0;
      transition: all 0.25s;
      -webkit-transition: all 0.25s;
      border-radius: 8px;
      box-shadow: 0 1px 1px rgba(0,0,0,.16);
      line-height: 16px;
      text-transform: uppercase;
      padding: 10px 8px;
      overflow: hidden;
    }
    .players div i {
      font-size: 20px;
      font-weight: 100;
    }
    .players table {
      margin: auto;
    }
    .play tr td {
      height: 110px;
      padding: 8px;
      position: relative;
      width: 100px;
      text-align: center;
      
    }
    .play tr td i {
      width: 50px;
      height: 50px;
      font-size: 50px;
      font-weight: 100;
    }
    .play {
      background-color: #14bdac;
      padding: 20px 0px;
      position: relative;

    }
    .play td {
      border: 5px solid #0da192;
    }
    .play table {
      width: 370px;
      height: 300px;
      margin: auto;
    }
    .play-ground {
      margin: 50px 0px;
      padding: 20px 0px;
      border: 1px solid #dfe1e5;
      border-radius: 8px;
    }
    .result-overlay {
      position: absolute;
      background: #15bdacb8;
      width: 100%;
      height: 100%;
      top: 0;
      z-index: 10;
      display: none;
    }
    .result-overlay > p {
      font-size: 50px;
      font-weight: 100;
      text-align: center;
      color: rgb(84, 84, 84);
      vertical-align: middle;
      height: 100%;
      justify-content: center;
      align-items: center;
      display: flex;
      font-weight: bold;
      margin: 20px;
    }
    .result-overlay > p > span {
      color: #f2ebd3;
      font-size: 100px;
      margin-right: 20px;
    }
    .result-overlay > p > span > i {
      font-weight: 100;
    }
</style>
