<template>
  <main class="pt-8 text-center">
    <h1 class="mb-8 text-3xl font-bold uppercase">Tic Tac Toe</h1>

    <h3 class="text-xl mb-4">Player {{ player }}'s turn</h3>

    <div class="flex flex-col items-center mb-8">
      <div 
        v-for="(row, x) in board" 
        :key="x"
        class="flex">
        <div 
          v-for="(cell, y) in row" 
          :key="y" 
          @click="MakeMove(x, y)" 
          :class="`border border-white w-24 h-24 hover:bg-gray-700 flex items-center justify-center material-icons-outlined text-4xl cursor-pointer ${cell === 'X' ? 'text-pink-500' : 'text-blue-400'}`">
          {{ cell === 'X' ? 'x' : cell === 'O' ? 'o' : '' }}
        </div>
      </div>
    </div>

    <div class="text-center">
      <h2 v-if="CalculateWinner(board.flat())" class="text-6xl font-bold mb-8">Player '{{ CalculateWinner(board.flat()) }}' wins!</h2>
      <button @click="resetGame" class="px-4 py-2 bg-pink-500 rounded uppercase font-bold hover:bg-pink-600 duration-300">Reset</button>
    </div>
  </main>
</template>

<script>
  export default {
    data() {
      return {
        player: "X",
        board: [
          ["", "", ""],
          ["", "", ""],
          ["", "", ""]
        ],
        lines: [[0, 1, 2],
                [3, 4, 5],
                [6, 7, 8],
                [0, 3, 6],
                [1, 4, 7],
                [2, 5, 8],
                [0, 4, 8],
                [2, 4, 6]]
      }
    },
    methods: {
      CalculateWinner(board) {
        for (let i = 0; i < this.lines.length; i++) {
          const [a, b, c] = this.lines[i]
          if (board[a] && board[a] === board[b] && board[a] === board[c]) {
            return board[a]
          }
        }
        return null
      },
      MakeMove(x, y) {
        if (this.winner) return
        if (this.board[x][y]) return
        this.board[x][y] = this.player
        this.player = this.player === 'X' ? 'O' : 'X'
      },
      resetGame() {
        this.board = [
          ['', '', ''],
          ['', '', ''],
          ['', '', '']
        ]
        this.player = 'X'
      }
    },
    computed: {
      winner() {
        return this.CalculateWinner(this.board.flat())
      }
    }
  }
</script>


<style>
body {
  @apply bg-gray-800 text-white mt-12;
}
</style>