<style>
    .tic-tac-toe {
        display: grid;
        grid-template-rows: 1fr 1fr 1fr;
        max-width: 50%;
        margin-left: auto;
        margin-right: auto;
    }

    .row {
        display: flex;
        justify-content: center;
    }

    .square {
        width: 40px;
        height: 40px;
    }

    .player-won-alert {
        margin: auto;
        margin-top: 20px
    }

    .reset-button {
        margin: auto;
        min-width: 30%;
        margin-top: 20px
    }
</style>

<script>
    let currentPlayer = 'X'
    let board = ['-', '-', '-', '-', '-', '-', '-', '-', '-']
    let gameIsOver = false

    function handleSquareClicked(squareIndex) {
        claimSquare(squareIndex)

        if (isGameOver()) {
            handleGameOver()
            return
        }

        alternatePlayer()
    }

    function claimSquare(squareIndex) {
        if (['X', 'O'].includes(board[squareIndex])) {
            return
        }

        board[squareIndex] = currentPlayer
    }

    function resetBoard() {
        board = ['-', '-', '-', '-', '-', '-', '-', '-', '-']
    }


    function isGameOver() {
        const winningPatterns = [
            [0, 1, 2],
            [3, 4, 5],
            [6, 7, 8],
            [0, 3, 6],
            [1, 4, 7],
            [2, 5, 8],
            [0, 4, 8],
            [2, 4, 6],
        ];

        for (let i = 0; i < winningPatterns.length; i++) {
            const pattern = winningPatterns[i];

            if (!patternHasBeenSelected(pattern, board)) {
                continue;
            }

            if (
                board[pattern[0]] === board[pattern[1]] &&
                board[pattern[1]] === board[pattern[2]]
            ) {
                return true;
            }
        }

        return false;
    }

    function patternHasBeenSelected(pattern, board) {
        const result = (
            board[pattern[0]] !== "-" &&
            board[pattern[1]] !== "-" &&
            board[pattern[2]] !== "-"
        );

        return result

    }

    function handleGameOver() {
        gameIsOver = true
    }


    function alternatePlayer() {
        currentPlayer = currentPlayer === 'X' ? 'O' : currentPlayer === 'O' ? 'X' : 'X'
    }
</script>

<section class="tic-tac-toe">
    <div class='row'>
        <button class="square" on:click={()=> handleSquareClicked(0)}>{board[0]}</button>
        <button class="square" on:click={()=> handleSquareClicked(1)}>{board[1]}</button>
        <button class="square" on:click={()=> handleSquareClicked(2)}>{board[2]}</button>
    </div>
    <div class='row'>
        <button class="square" on:click={()=> handleSquareClicked(3)}>{board[3]}</button>
        <button class="square" on:click={()=> handleSquareClicked(4)}>{board[4]}</button>
        <button class="square" on:click={()=> handleSquareClicked(5)}>{board[5]}</button>
    </div>
    <div class='row'>
        <button class="square" on:click={()=> handleSquareClicked(6)}>{board[6]}</button>
        <button class="square" on:click={()=> handleSquareClicked(7)}>{board[7]}</button>
        <button class="square" on:click={()=> handleSquareClicked(8)}>{board[8]}</button>
    </div>

    {#if gameIsOver }
        <p class='player-won-alert'> player {currentPlayer} wins 🎉 </p>
    {/if}
    <button class='reset-button' on:click={resetBoard}>reset</button>
</section>