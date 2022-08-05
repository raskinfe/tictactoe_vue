<template>
    <div class="tictactoe">
        <div class="row" v-for="(n, i) in 3" :key="n">
           <div v-for="(n, j) in 3" :key="n">
                <single-cell @click="gotoCell(i, j)" :value="board[i][j]" />
           </div> 
        </div>
        <div class="message">
            <p v-if="!displayMessage && !isDraw">Player <span>{{Number(this.swapPlayer) + 1}}</span>'s turn</p>
            <p v-else-if="displayMessage">Player <span>{{Number(this.swapPlayer) + 1}}</span>  won!!</p>
            <p v-else-if="isDraw">Draw</p>
            <button class="btn btn-reset" @click="resetBoard">Reset</button>
        </div>
    </div>
</template>

<script>
import SingleCell from './SingleCell.vue'
import Board  from '../constants/Board.js' 

export default {
  components: { SingleCell },
    name: 'TicTacToe',
    data() {
        return {
            board: new Board().cells,
            swapPlayer: false,
            displayMessage: false,
        }
    },
    computed: {
         isDraw() {
            const movesLeft = [];
            let count = 0;
            for(let i=0; i <3; i++) {
                for(let j=0; j<3; j++) {
                    console.log(i, j)
                    if(this.board[i][j] == '') 
                    {
                        ++count;
                        movesLeft.push(count);
                        
                    }
                }
            }
            return movesLeft.length === 0;
        }
    },
    methods: {
        gotoCell(a, b) {
            if(this.isGameOver()) {return;}
            if(this.board[a][b] != '') { return; }
            this.swapPlayer = !this.swapPlayer;
            const player = Number(this.swapPlayer) == 1 ? "x" :"o";
            if(player == "x") {
                 this.board[a][b] = "x";
            }else {
                 this.board[a][b] = "o";
            }
            const wininingMove = this.isAWiningMove(player);
            if(wininingMove) {
                this.displayMessage = true;
            }
        },
        resetBoard() {
            this.board = new Board().cells
            this.swapPlayer = false;
            this.displayMessage = false;
        },
        isAWiningMove(player){
           /*   Horizontal rows  */
            for(let i=0; i<3; i++) {
                if(this.board[0][i] == player && this.board[1][i] == player && this.board[2][i] == player) {return true;}
            }
            /* vertical rows */
             for(let i=0; i<3; i++) {
                if(this.board[i][0] == player && this.board[i][1] == player && this.board[i][2] == player) {return true;}
            }
            /* diagonal rows */
            if(this.board[0][0] == player && this.board[1][1] == player && this.board[2][2] == player) {return true;}
            if(this.board[2][0] == player && this.board[1][1] == player && this.board[0][2] == player) {return true;} 
            return false;
        },
        isGameOver() {
            if(this.displayMessage) {return true;}
            if(this.isDraw){return true;}
        },
    }
}
</script>
<style scoped>
.tictactoe{
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    align-content: center;
    margin-top: 100px;
    min-height: 50vh;
}
.row {
    display: flex;
    flex-direction: row;
}
.message {
    margin: 30px;
    font-size: 30px;
    display: flex;
    flex-direction: row;
    gap: 40px;
}
.btn {
      padding: 10px 35px;
    font-size: 1.4rem;
    border-radius: 10px;
    background: transparent;
    outline: none;
}
.btn-reset {
    border: 0.5px solid crimson;
    color: #fff;
}
.btn-reset:hover{
    background: crimson;
    color: #000;
    border: 1px solid #fff;
}
</style>
