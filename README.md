<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Tic-Tac-Toe Game</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: url("/tic_tac_toe/tic\ tac\ toe\ image.jpg");
            background-size: cover;
            background-position: center;
            background-repeat: no-repeat;
            min-height: 100vh;
            display: flex;
            align-items: center;
            justify-content: center;
            padding: 20px;
        }

        .game-container {
            background: rgba(255, 255, 255, 0.95);
            border-radius: 20px;
            padding: 2rem;
            box-shadow: 0 20px 40px rgba(0, 0, 0, 0.1);
            text-align: center;
            max-width: 500px;
            width: 90%;
            backdrop-filter: blur(10px);
        }

        h1 {
            color: #4a5568;
            margin-bottom: 1rem;
            font-size: 2.5rem;
            text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.1);
        }

        .game-modes {
            margin-bottom: 2rem;
            display: flex;
            gap: 1rem;
            justify-content: center;
            flex-wrap: wrap;
        }

        .mode-btn {
            padding: 0.8rem 1.5rem;
            border: none;
            border-radius: 25px;
            font-size: 1rem;
            font-weight: bold;
            cursor: pointer;
            transition: all 0.3s ease;
            background: linear-gradient(45deg, #667eea, #764ba2);
            color: white;
            box-shadow: 0 4px 15px rgba(102, 126, 234, 0.3);
        }

        .mode-btn:hover {
            transform: translateY(-2px);
            box-shadow: 0 6px 20px rgba(102, 126, 234, 0.4);
        }

        .mode-btn.active {
            background: linear-gradient(45deg, #48bb78, #38a169);
            box-shadow: 0 4px 15px rgba(72, 187, 120, 0.3);
        }

        .game-info {
            margin-bottom: 2rem;
            display: flex;
            justify-content: space-between;
            align-items: center;
            flex-wrap: wrap;
            gap: 1rem;
        }

        .current-player, .score {
            font-size: 1.2rem;
            font-weight: bold;
            color: #4a5568;
        }

        .player-x { color: #e53e3e; }
        .player-o { color: #3182ce; }

        .board {
            display: grid;
            grid-template-columns: repeat(3, 1fr);
            gap: 8px;
            margin: 2rem auto;
            max-width: 300px;
            background: #4a5568;
            padding: 8px;
            border-radius: 15px;
            box-shadow: inset 0 4px 8px rgba(0, 0, 0, 0.2);
        }

        .cell {
            width: 90px;
            height: 90px;
            background: white;
            border: none;
            border-radius: 10px;
            font-size: 2rem;
            font-weight: bold;
            cursor: pointer;
            transition: all 0.3s ease;
            display: flex;
            align-items: center;
            justify-content: center;
            box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
        }

        .cell:hover {
            background: #f7fafc;
            transform: scale(1.05);
            box-shadow: 0 4px 10px rgba(0, 0, 0, 0.15);
        }

        .cell.x {
            color: #e53e3e;
            animation: popIn 0.3s ease;
        }

        .cell.o {
            color: #3182ce;
            animation: popIn 0.3s ease;
        }

        .cell.winning {
            background: linear-gradient(45deg, #48bb78, #38a169);
            color: white;
            animation: pulse 0.6s ease-in-out;
        }

        @keyframes popIn {
            0% { transform: scale(0); }
            80% { transform: scale(1.1); }
            100% { transform: scale(1); }
        }

        @keyframes pulse {
            0%, 100% { transform: scale(1); }
            50% { transform: scale(1.1); }
        }

        .controls {
            margin-top: 2rem;
            display: flex;
            gap: 1rem;
            justify-content: center;
            flex-wrap: wrap;
        }

        .btn {
            padding: 0.8rem 1.5rem;
            border: none;
            border-radius: 25px;
            font-size: 1rem;
            font-weight: bold;
            cursor: pointer;
            transition: all 0.3s ease;
        }

        .reset-btn {
            background: linear-gradient(45deg, #ed8936, #dd6b20);
            color: white;
            box-shadow: 0 4px 15px rgba(237, 137, 54, 0.3);
        }

        .reset-btn:hover {
            transform: translateY(-2px);
            box-shadow: 0 6px 20px rgba(237, 137, 54, 0.4);
        }

        .status {
            margin: 1rem 0;
            font-size: 1.3rem;
            font-weight: bold;
            min-height: 2rem;
            display: flex;
            align-items: center;
            justify-content: center;
        }

        .winner {
            color: #48bb78;
            animation: celebration 0.8s ease-in-out;
        }

        .draw {
            color: #ed8936;
        }

        @keyframes celebration {
            0%, 100% { transform: scale(1); }
            25% { transform: scale(1.1) rotate(-2deg); }
            75% { transform: scale(1.1) rotate(2deg); }
        }

        .difficulty {
            margin: 1rem 0;
            display: flex;
            gap: 0.5rem;
            justify-content: center;
            flex-wrap: wrap;
        }

        .difficulty-btn {
            padding: 0.5rem 1rem;
            border: 2px solid #667eea;
            background: transparent;
            color: #667eea;
            border-radius: 20px;
            cursor: pointer;
            transition: all 0.3s ease;
            font-weight: bold;
        }

        .difficulty-btn.active {
            background: #667eea;
            color: white;
        }

        .difficulty-btn:hover {
            background: #667eea;
            color: white;
            transform: translateY(-1px);
        }

        @media (max-width: 480px) {
            .game-container {
                padding: 1rem;
            }
            
            .board {
                max-width: 270px;
            }
            
            .cell {
                width: 80px;
                height: 80px;
                font-size: 1.8rem;
            }
            
            h1 {
                font-size: 2rem;
            }
        }
    </style>
</head>
<body>
    <div class="game-container">
        <h1>🎮 Tic-Tac-Toe</h1>
        
        <div class="game-modes">
            <button class="mode-btn active" onclick="setGameMode('pvp')">Player vs Player</button>
            <button class="mode-btn" onclick="setGameMode('pve')">Player vs AI</button>
        </div>

        <div id="difficulty-section" class="difficulty" style="display: none;">
            <button class="difficulty-btn active" onclick="setDifficulty('easy')">Easy</button>
            <button class="difficulty-btn" onclick="setDifficulty('medium')">Medium</button>
            <button class="difficulty-btn" onclick="setDifficulty('hard')">Hard</button>
        </div>

        <div class="game-info">
            <div class="current-player">
                Current Player: <span id="current-player" class="player-x">X</span>
            </div>
            <div class="score">
                <span class="player-x">X: <span id="score-x">0</span></span> - 
                <span class="player-o">O: <span id="score-o">0</span></span>
            </div>
        </div>

        <div class="status" id="status">Click a cell to start playing!</div>

        <div class="board" id="board">
            <button class="cell" onclick="makeMove(0)"></button>
            <button class="cell" onclick="makeMove(1)"></button>
            <button class="cell" onclick="makeMove(2)"></button>
            <button class="cell" onclick="makeMove(3)"></button>
            <button class="cell" onclick="makeMove(4)"></button>
            <button class="cell" onclick="makeMove(5)"></button>
            <button class="cell" onclick="makeMove(6)"></button>
            <button class="cell" onclick="makeMove(7)"></button>
            <button class="cell" onclick="makeMove(8)"></button>
        </div>

        <div class="controls">
            <button class="btn reset-btn" onclick="resetGame()">Reset Game</button>
        </div>
    </div>

    <script>
        let board = Array(9).fill('');
        let currentPlayer = 'X';
        let gameMode = 'pvp';
        let difficulty = 'medium';
        let gameActive = true;
        let scores = { X: 0, O: 0 };

        const winningCombinations = [
            [0, 1, 2], [3, 4, 5], [6, 7, 8],
            [0, 3, 6], [1, 4, 7], [2, 5, 8],
            [0, 4, 8], [2, 4, 6]
        ];

        function init() {
            updateDisplay();
            updateStatus('Click a cell to start playing!');
        }

        function setGameMode(mode) {
            gameMode = mode;
            resetGame();
            
            document.querySelectorAll('.mode-btn').forEach(btn => btn.classList.remove('active'));
            event.target.classList.add('active');
            
            const difficultySection = document.getElementById('difficulty-section');
            difficultySection.style.display = mode === 'pve' ? 'flex' : 'none';
        }

        function setDifficulty(level) {
            difficulty = level;
            document.querySelectorAll('.difficulty-btn').forEach(btn => btn.classList.remove('active'));
            event.target.classList.add('active');
        }

        function makeMove(index) {
            if (!gameActive || board[index] !== '') return;

            board[index] = currentPlayer;
            updateCell(index, currentPlayer);

            if (checkWinner()) {
                endGame(`Player ${currentPlayer} wins!`, 'winner');
                scores[currentPlayer]++;
                updateScores();
                return;
            }

            if (board.every(cell => cell !== '')) {
                endGame("It's a draw!", 'draw');
                return;
            }

            currentPlayer = currentPlayer === 'X' ? 'O' : 'X';
            updateCurrentPlayer();

            if (gameMode === 'pve' && currentPlayer === 'O' && gameActive) {
                setTimeout(() => {
                    makeAIMove();
                }, 500);
            }
        }

        function makeAIMove() {
            let move = -1;

            switch (difficulty) {
                case 'easy':
                    move = getRandomMove();
                    break;
                case 'medium':
                    move = Math.random() < 0.7 ? getBestMove() : getRandomMove();
                    break;
                case 'hard':
                    move = getBestMove();
                    break;
            }

            if (move !== -1) {
                makeMove(move);
            }
        }

        function getRandomMove() {
            const availableMoves = board.map((cell, index) => cell === '' ? index : null).filter(index => index !== null);
            return availableMoves.length > 0 ? availableMoves[Math.floor(Math.random() * availableMoves.length)] : -1;
        }

        function getBestMove() {
            let bestScore = -Infinity;
            let bestMove = -1;

            for (let i = 0; i < 9; i++) {
                if (board[i] === '') {
                    board[i] = 'O';
                    let score = minimax(board, 0, false);
                    board[i] = '';
                    
                    if (score > bestScore) {
                        bestScore = score;
                        bestMove = i;
                    }
                }
            }

            return bestMove;
        }

        function minimax(board, depth, isMaximizing) {
            const winner = checkWinnerForMinimax();
            
            if (winner === 'O') return 10 - depth;
            if (winner === 'X') return depth - 10;
            if (board.every(cell => cell !== '')) return 0;

            if (isMaximizing) {
                let bestScore = -Infinity;
                for (let i = 0; i < 9; i++) {
                    if (board[i] === '') {
                        board[i] = 'O';
                        let score = minimax(board, depth + 1, false);
                        board[i] = '';
                        bestScore = Math.max(score, bestScore);
                    }
                }
                return bestScore;
            } else {
                let bestScore = Infinity;
                for (let i = 0; i < 9; i++) {
                    if (board[i] === '') {
                        board[i] = 'X';
                        let score = minimax(board, depth + 1, true);
                        board[i] = '';
                        bestScore = Math.min(score, bestScore);
                    }
                }
                return bestScore;
            }
        }

        function checkWinnerForMinimax() {
            for (let combination of winningCombinations) {
                const [a, b, c] = combination;
                if (board[a] && board[a] === board[b] && board[a] === board[c]) {
                    return board[a];
                }
            }
            return null;
        }

        function checkWinner() {
            for (let combination of winningCombinations) {
                const [a, b, c] = combination;
                if (board[a] && board[a] === board[b] && board[a] === board[c]) {
                    highlightWinningCells(combination);
                    return true;
                }
            }
            return false;
        }

        function highlightWinningCells(combination) {
            combination.forEach(index => {
                document.querySelectorAll('.cell')[index].classList.add('winning');
            });
        }

        function updateCell(index, player) {
            const cell = document.querySelectorAll('.cell')[index];
            cell.textContent = player;
            cell.classList.add(player.toLowerCase());
        }

        function updateCurrentPlayer() {
            const playerElement = document.getElementById('current-player');
            playerElement.textContent = currentPlayer;
            playerElement.className = currentPlayer === 'X' ? 'player-x' : 'player-o';
        }

        function updateStatus(message) {
            document.getElementById('status').textContent = message;
        }

        function endGame(message, type) {
            gameActive = false;
            const statusElement = document.getElementById('status');
            statusElement.textContent = message;
            statusElement.className = `status ${type}`;
        }

        function updateScores() {
            document.getElementById('score-x').textContent = scores.X;
            document.getElementById('score-o').textContent = scores.O;
        }

        function resetGame() {
            board = Array(9).fill('');
            currentPlayer = 'X';
            gameActive = true;
            
            document.querySelectorAll('.cell').forEach(cell => {
                cell.textContent = '';
                cell.className = 'cell';
            });
            
            updateCurrentPlayer();
            updateStatus('Click a cell to start playing!');
            document.getElementById('status').className = 'status';
        }

        function updateDisplay() {
            updateCurrentPlayer();
            updateScores();
        }

        init();
    </script>
</body>
</html># Tic-Tac-Toe
