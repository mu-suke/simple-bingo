<template>
  <div class="Bingo">
    <h2>{{msg}}</h2>
    <div v-if="!StartButtonState">
      <button v-if="!StartButtonState" @click="setNumber">Click Here!</button>
    </div>

    <div v-if="StartButtonState">
      <p class="display-number">{{SelectedNum}}</p>
      <button v-if="StartButtonState" @click="checkNum">generateNum</button>
      <button v-else @click="ChangeStartButtonState">reset</button>
      <ul class="bingo-hole">
        <li class="bingo-hole-num" v-for="(num, index) in HistoryNumberList" :key="index" :class="{isHit: num.isHit}" >{{num.id}}</li>
      </ul>
    </div>

  </div>
</template>


<script>
// import { log } from 'util';

export default {
  name: 'Bingo',
  components: {
    // CButton
  },
  data: () => ({
    msg: "Welcome my-Bingo Page!",
    HistoryNumberList: [],
    AlwaysTrue: true,
    StartButtonState: false,
    MaxHoleNum: 5,
    SelectedNum: 0,
  }),
  methods: {
    setNumber: function() {
      this.StartButtonState = !this.StartButtonState;
      // それぞれの番号に状態を付与
      for (let i = 0; i < this.MaxHoleNum; i++) {
        this.HistoryNumberList.push({
          id: Number([i]) + 1,
          isHit: false
        });
      }
    },
    ChangeStartButtonState: function() {
      this.StartButtonState = !this.StartButtonState;
    },
    generateNum: function() {
      return 1 + Math.round( Math.random () * (this.MaxHoleNum - 1) );
    },
    checkNum: function() {
      this.SelectedNum = this.generateNum();
      for (let i = 0 ; i < this.HistoryNumberList.length; i++) {
        if (this.HistoryNumberList[i].id === this.SelectedNum) {
          if (this.HistoryNumberList[i].isHit) {
            this.checkNum();
            console.log("true")
          }else {
            this.HistoryNumberList[i].isHit = true;
            console.log("false")
          }
          break;
        }
        else if (i === this.HistoryNumberList.length) {
          this.resetBingo();
        }
      }
    },
    resetBingo: function() {
      this.msg = "FINISH!";
      this.StartButtonState = false;
    }
  }
}
</script>


<style lang="scss">
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
.display-number {
  font-size: 24px;
}
.bingo-hole {
  display: flex;
  flex-wrap: wrap;
  list-style: none;
  margin: 30px auto;
  width: 75%;
  &-num {
    align-items: center;
    background-color: #ffffff;
    border: solid 1px #111111;
    color: #111111;
    display: flex;
    font-size: 16px;
    height: 30px;
    justify-content: center;
    text-align: center;
    width: 30px;
  }
}

.isHit {
  background-color: #111111;
  color: #ffffff;
}

</style>

// kebab-case