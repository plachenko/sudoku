<template> 
  <div id="container">
    <!--
    <div>
      <label for="difficulty">Difficulty ({{difficultyTxt[difficulty]}}):</label>
      <input name="difficulty" v-model="difficulty" @input="setaNumbers" min="0" max="6" type="range">
    </div>
    -->
    <div>
      <div v-for="a in 9" :key="a" class="numInp">{{a}}</div>
    </div>
    <div id="game">
      <div class="block" v-for="a in aNumbers.length" :key="a">
        <div class="block" v-for="b in aNumbers[a - 1].length" :key="b">
          <span v-if="Math.floor(Math.random()*11) >= difficulty">{{ aNumbers[a - 1][b - 1] }}</span>
        </div>
      </div>
    </div>
  </div>
</template>

<script>

export default {
  name: 'App',
  components: {
  },
  data: function() {
    return{
      aNumbers: [[]],
      difficulty: 0,
      difficultyTxt: [
        'number mode',
        'sunday driving',
        'easy',
        'medium',
        'hard',
        'extreme'
      ]
    }
  },
  beforeMount(){
    this.setaNumbers();
  },
  mounted(){
    // Sudoku Comitted
  },
  methods: {
    setaNumbers(){
      const aNumbers = this.aNumbers || []
      let a = 0

      while(a < 3){
        aNumbers[a] = aNumbers[a - 1] || []

        let b = 0
        while(b < 9){
          let arr = []

          if(!a){
            arr[b] = (b || 9)
            // aNumbers[a] = this.shuffle(aNumbers[a])
          }else{
            // aNumbers[a][b] = arr[(b*1)%9]
            /*
            switch(b){
              case 6:
                aNumbers[a] = this.shuffle(aNumbers[a])
                break;
              case 8:
                aNumbers[a] = [...aNumbers[a].slice(0, 3), ...this.shuffle(aNumbers[a].slice(3, 9))]
                break;
            }
            */
          //  aNumbers[a][b] = aNumbers[a]
          }

          aNumbers[a] = arr
          console.log(arr)

          /*- increment b -*/
          b++
        }


        /*- increment a -*/
        a++

        /*

        if(!a){
          aNumbers[a] = this.shuffle(aNumbers[a])
        }else{
          let arr 
          let c

          if(a%3 == 0){
            arr = aNumbers[a-3]
            c = 1
          }else{
            arr = aNumbers[a-1]
            c = 3
          }

          while(b < 9){
            b++
          }
        }
        */
      }
      // let shuffled;

      // for(let a = 0; a < 2; a++){
        // aNumbers[a] = []

          // this.aNumbers[a] = this.aNumbers[a]);
          /*
          let top = this.aNumbers[a-1].slice(3, 9)
          let mid = [...this.aNumbers[a-1].slice(0,3), ...this.aNumbers[a-1].slice(6,9)]
          let bot = this.aNumbers[a-1].slice(0, 6)
          */

          // console.log(top, mid, bot)
          /*
        for(let b = 0; b < 9; b++){
          aNumbers[a][b] = a ? this.shuffle(aNumbers[a-1].slice(0,6))[b] : (b || 9)
        }
        aNumbers[a] = a ? aNumbers[a] : this.shuffle(aNumbers[a])
        */
        /*
          shuffled = this.shuffle(this.aNumbers[a-1]);
          for(let b = 0; b < 9; b++){
            if(this.aNumbers[a-1][b])
          }
         console.log(this.aNumbers[a-1][b])
        }else{
          shuffled = this.shuffle(this.aNumbers[a]);
        }

        this.aNumbers[a] = shuffled
          */
      // }
    },
    shuffle(array, mode=2){
      /* Sorting */
      switch(mode){
        case 0:
          /* -- No sort */
          return
        case 1:
          /* -- Simple sort */
          return array.sort(() => 0.5 - Math.random())
        case 2:
          /* -- Fischer-Gate algorithm */
          for (let a = array.length - 1; a > 0; a--){
            const b = Math.floor(Math.random() * (a + 1))
            const temp = array[a]
            array[a] = array[b]
            array[b] = temp
          }
          return array
      }
    },
  }
}
</script>

<style>
html, body {
  height: 100%;
  margin: 0px;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  height: 100%;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 200%;
}

.numInp{
  float: left;
  border: 1px solid;
  padding: 6px;
  margin: 2px;
  cursor: pointer;
  user-select: none;
}
.numInp:hover{
  background-color: #CCC;
}

#game{
  width: 399px;
  height: 399px;
  /* border: 3px solid; */
}

#container{
  height: 90%;
  width: 90%;
  max-width: 460px;
  max-height: 500px;
  display: flex;
  align-items: center;
  justify-content: center;
  flex-wrap: wrap;
}

.block{
  box-sizing: border-box;
  width: 33.33%;
  height: 33.33%;
  flex: 1 1 auto;
  display: flex;
  border: 1px solid;
  float: left;
  display: flex;
  align-items: flex-start;
  justify-content: center;
  flex-wrap: wrap;
  cursor: pointer;
  user-select: none;
  }
</style>
