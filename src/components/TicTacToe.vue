<template>

  <div id="tic-tac-toe">
    <Player :playerData="players[0]"></Player>
    <player :player-data="players[1]"></player>
    <table>
      <tr v-for="(row, ri) in table" :key="ri">
        <td v-for="(column, ci) in row" :key="ci" @click="updateSquare(ri, ci)">
          <Square :who-play="game.whoPlay" :value="column"></Square>
        </td>
      </tr>
    </table>
  </div>

</template>

<script>
import Player from './Player.vue';
import Square from './Square.vue';

const createTable = () => [
  [-1, -1, -1],
  [-1, -1, -1],
  [-1, -1, -1],
];

const checkRows = (table, row) => {
  if (table[row][0] === 0 && table[row][1] === 0 && table[row][2] === 0) return 0;
  if (table[row][0] === 1 && table[row][1] === 1 && table[row][2] === 1) return 1;
  return -1;
};

const checkCols = (table, col) => {
  if (table[0][col] === 0 && table[1][col] === 0 && table[2][col] === 0) return 0;
  if (table[0][col] === 1 && table[1][col] === 1 && table[2][col] === 1) return 1;
  return -1;
};

const checkDiagonals = (table) => {
  if ((table[0][0] === 0 && table[1][1] === 0 && table[2][2] === 0)
    || (table[2][0] === 0 && table[1][1] === 0 && table[0][2] === 0)) return 0;
  if ((table[0][0] === 1 && table[1][1] === 1 && table[2][2] === 1)
    || (table[2][0] === 1 && table[1][1] === 1 && table[0][2] === 1)) return 1;
  return -1;
};

const checkTable = (table) => {
  for (let i = 0; i < table.length; i += 1) {
    const rowResult = checkRows(table, i);

    if (rowResult !== -1) {
      return rowResult;
    }

    const colCheck = checkCols(table, i);
    if (colCheck !== -1) {
      return colCheck;
    }
  }

  const diagonalCheck = checkDiagonals(table);
  if (diagonalCheck !== -1) {
    return diagonalCheck;
  }

  return -1;
};

const tableIsFull = (table) => {
  let result = true;

  for (let x = 0; x < table.length; x += 1) {
    for (let y = 0; y < table[x].length; y += 1) {
      if (table[x][y] === -1) result = false;
    }
  }

  return result;
};

export default {
  name: 'TicTacToe',
  components: { Square, Player },
  data() {
    return {
      game: {
        whoPlay: 0,
      },
      players: [{
        img: 'https://randomuser.me/api/portraits/men/11.jpg',
        name: 'Michel',
        score: 0,
      }, {
        img: 'https://randomuser.me/api/portraits/women/57.jpg',
        name: 'Micheline',
        score: 0,
      }],
      table: createTable(),
    };
  },
  methods: {
    updateSquare(r, c) {
      if (this.table[r][c] !== -1) return;
      const editRow = this.table[r];
      editRow[c] = this.game.whoPlay;
      this.$set(this.table, r, editRow);

      const winner = checkTable(this.table);
      if (winner !== -1) this.players[winner].score += 1;
      if (tableIsFull(this.table) || winner !== -1) this.table = createTable();

      this.game.whoPlay = this.game.whoPlay === 0 ? 1 : 0;
    },
  },
};
</script>

<style lang="scss" scoped>

  #tic-tac-toe {
    text-align: center;

    table {
      margin: auto;
      border-collapse: collapse;

      tr {
        &:first-child {
          td {
            border-top: 0;
          }
        }

        &:last-child {
          td {
            border-bottom: 0;
          }
        }

        td {
          position: relative;
          width: 100px;
          height: 100px;
          font-size: 70px;
          /*background: #ffffff;*/

          border: 4px solid #ffffff;
          color: #ffffff;

          &:first-child {
            border-left: 0;
          }

          &:last-child {
            border-right: 0;
          }
        }
      }
    }
  }

</style>
