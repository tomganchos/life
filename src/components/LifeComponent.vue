<template>
  <div>
    <div class="logo">
      <div v-for="(row, indexOuter) in massLogo" :key="indexOuter + 'logo'" class="row">
        <div v-for="(cell, indexInner) in row" :key="indexOuter + indexInner + 'logo'" class="cell">
          <div v-if="cell" class="cell-live"/>
          <div v-else class="cell-dead"/>
        </div>
      </div>
    </div>
    <br>
    <div v-for="(row, indexOuter) in mass" :key="indexOuter" class="row">
      <div v-for="(cell, indexInner) in row" :key="indexOuter + indexInner" class="cell" @click="setLife(indexOuter, indexInner)">
        <div v-if="cell" class="cell-live"/>
        <div v-else class="cell-dead"/>
      </div>
    </div>
  </div>
</template>

<script>
  export default {
    name: "LifeComponent",
    data () {
      return {
        mass: [
          [false, false, false, false, false, false, false, false, false, false, false, false, false, false, false, false, false, false, false, false, false, false, false, false, false, false, false, false, false, false, false, false, false, false, false, false, false, false],
          [false, false, false, false, false, false, false, false, false, false, false, false, false, false, false, false, false, false, false, false, false, false, false, false, false, true,  false, false, false, false, false, false, false, false, false, false, false, false],
          [false, false, false, false, false, false, false, false, false, false, false, false, false, false, false, false, false, false, false, false, false, false, false, true,  false, true,  false, false, false, false, false, false, false, false, false, false, false, false],
          [false, false, false, false, false, false, false, false, false, false, false, false, false, true,  true,  false, false, false, false, false, false, true,  true,  false, false, false, false, false, false, false, false, false, false, false, false, true,  true,  false],
          [false, false, false, false, false, false, false, false, false, false, false, false, true,  false, false, false, true,  false, false, false, false, true,  true,  false, false, false, false, false, false, false, false, false, false, false, false, true,  true,  false],
          [false, true,  true,  false, false, false, false, false, false, false, false, true,  false, false, false, false, false, true,  false, false, false, true,  true,  false, false, false, false, false, false, false, false, false, false, false, false, false, false, false],
          [false, true,  true,  false, false, false, false, false, false, false, false, true,  false, false, false, true,  false, true,  true,  false, false, false, false, true,  false, true,  false, false, false, false, false, false, false, false, false, false, false, false],
          [false, false, false, false, false, false, false, false, false, false, false, true,  false, false, false, false, false, true,  false, false, false, false, false, false, false, true,  false, false, false, false, false, false, false, false, false, false, false, false],
          [false, false, false, false, false, false, false, false, false, false, false, false, true,  false, false, false, true,  false, false, false, false, false, false, false, false, false, false, false, false, false, false, false, false, false, false, false, false, false],
          [false, false, false, false, false, false, false, false, false, false, false, false, false, true,  true,  false, false, false, false, false, false, false, false, false, false, false, false, false, false, false, false, false, false, false, false, false, false, false],
          [false, false, false, false, false, false, false, false, false, false, false, false, false, false, false, false, false, false, false, false, false, false, false, false, false, false, false, false, false, false, false, false, false, false, false, false, false, false]
        ],
        massLogo: [
          [true, false, false, true, false, true, true, false, true, true],
          [true, false, false, false, false, true, false, false, true, false],
          [true, false, false, true, false, true, true, false, true, true],
          [true, false, false, true, false, true, false, false, true, false],
          [true, true, false, true, false, true, false, false, true, true]
        ],
        interval: 1
      }
    },
    mounted() {
      this.nextStep()
    },
    methods: {
      nextStep: function () {
        setInterval(() => {
          let newMass = []
          this.mass.forEach((row, indexOuter) => {
            let newRow = []
            row.forEach((cell, indexInner) => {
              let neighborhood = 0
              if (this.mass[indexOuter - 1] && this.mass[indexOuter - 1][indexInner - 1]) {
                neighborhood++
              }
              if (this.mass[indexOuter - 1] && this.mass[indexOuter - 1][indexInner]) {
                neighborhood++
              }
              if (this.mass[indexOuter - 1] && this.mass[indexOuter - 1][indexInner + 1]) {
                neighborhood++
              }
              if (this.mass[indexOuter][indexInner - 1]) {
                neighborhood++
              }
              if (this.mass[indexOuter][indexInner + 1]) {
                neighborhood++
              }
              if (this.mass[indexOuter + 1] && this.mass[indexOuter + 1][indexInner - 1]) {
                neighborhood++
              }
              if (this.mass[indexOuter + 1] && this.mass[indexOuter + 1][indexInner]) {
                neighborhood++
              }
              if (this.mass[indexOuter + 1] && this.mass[indexOuter + 1][indexInner + 1]) {
                neighborhood++
              }
              if (!this.mass[indexOuter][indexInner] && neighborhood === 3) {
                newRow[indexInner] = true
              } else if (this.mass[indexOuter][indexInner] && (neighborhood === 2 || neighborhood === 3)) {
                newRow[indexInner] = true
              } else if (this.mass[indexOuter][indexInner] && (neighborhood < 2 || neighborhood > 3)) {
                newRow[indexInner] = false
              } else {
                newRow[indexInner] = false
              }
            })
            newMass.push(newRow)
          })
          this.mass = newMass
        }, 100)
      },
      setLife: function (indexOuter, indexInner) {
        if (this.mass[indexOuter][indexInner]) {
          this.$set(this.mass[indexOuter], indexInner, false)
        } else {
          this.$set(this.mass[indexOuter], indexInner, true)
        }
      }
    }
  }
</script>

<style scoped>
  .logo {
    display: inline-block;
  }
  .row {
    display: flex;
  }
  .cell {
    padding: 5px;
  }
 .cell .cell-live, .cell .cell-dead {
   width: 20px;
   height: 20px;
 }
  .cell-live {
    background-color: #2c3e50;
  }
  .cell-dead {
    background-color: aliceblue;
  }
</style>
