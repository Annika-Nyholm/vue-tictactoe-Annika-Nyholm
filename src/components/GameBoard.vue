<template>
	<article class="gameboard">
		<h2>TicTacToe-do!</h2>
		<h3>{{ currentPlayerName }}´s turn - {{ currentPlayer }}</h3>
		<div class="board">
			<Cell
				v-for="(value, index) in board"
				:key="index"
				:value="value"
				:index="index"
				@cell-click="makeMove"
			/>
		</div>
		<div class="buttons">
			<button @click="toggleScorePopup" v-if="gameStarted">
				Show score
			</button>
			<button @click="$emit('reset-game')" v-if="gameStarted">
				Play again
			</button>
			<button @click="newGame" v-if="gameStarted">New game</button>
		</div>
	</article>
</template>

<script setup lang="ts">
import { ref, onMounted, defineExpose, computed } from 'vue';
import Cell from './Cell.vue';

const props = defineProps<{
	playerX: string;
	playerO: string;
	gameStarted: boolean;
}>();

const emit = defineEmits<{
	(e: 'update-score', winner: string): void;
	(e: 'game-won', winner: string): void;
	(e: 'toggle-score-popup'): void;
	(e: 'new-game'): void;
	(e: 'reset-game'): void;
}>();

const board = ref<(string | null)[]>(Array(9).fill(null));
const winner = ref<string | null>(null);
const currentPlayer = ref('X');
const currentPlayerName = computed(() =>
	currentPlayer.value === 'X' ? props.playerX : props.playerO
);


onMounted(() => {
	const savedBoard = localStorage.getItem('board');
	const savedCurrentPlayer = localStorage.getItem('currentPlayer');

	if (savedBoard && savedCurrentPlayer) {
		board.value = JSON.parse(savedBoard);
		currentPlayer.value = savedCurrentPlayer;
	}
});

const makeMove = (index: number) => {
	if (!board.value[index] && !winner.value) {
		board.value[index] = currentPlayer.value;
		winner.value = checkWinner();
		if (!winner.value) {
			currentPlayer.value = currentPlayer.value === 'X' ? 'O' : 'X';
		} else {
			emit('update-score', winner.value);
			emit('game-won', winner.value);
		}
		localStorage.setItem('board', JSON.stringify(board.value));
		localStorage.setItem('currentPlayer', currentPlayer.value);
	}
};

const checkWinner = () => {
	const winningCombo = [
		[0, 1, 2],
		[3, 4, 5],
		[6, 7, 8],
		[0, 3, 6],
		[1, 4, 7],
		[2, 5, 8],
		[0, 4, 8],
		[2, 4, 6],
	];

	for (const combo of winningCombo) {
		const [a, b, c] = combo;
		if (
			board.value[a] &&
			board.value[a] === board.value[b] &&
			board.value[a] === board.value[c]
		) {
			return board.value[a];
		}
	}

	return board.value.every((cell) => cell) ? 'Draw' : null;
};

const toggleScorePopup = () => {
	emit('toggle-score-popup');
};

const newGame = () => {
	emit('new-game');
};

const resetBoard = () => {
	board.value = Array(9).fill(null);
	currentPlayer.value = 'X';
	winner.value = null;
	localStorage.removeItem('board');
	localStorage.removeItem('currentPlayer');
};

defineExpose({ resetBoard });
// const gameboard = ref({ resetBoard });
</script>

<style lang="scss" scoped>
@import '../assets/styles/variables';

.gameboard {
	font-family: 'Shadows Into Light', cursive;
	text-align: center;
	margin-top: 50px;
	display: flex;
	flex-direction: column;
	align-items: center;
	color: $color1;

	h2 {
		font-size: 2.5rem;
	}
}

.board {
	display: grid;
	grid-template-columns: repeat(3, 1fr);
	margin-bottom: 20px;
	border: 4px solid;
	box-shadow: $box-shadow-button;
}

.buttons {
	display: flex;
	flex-direction: column;
}
button {
	margin: 6px;
}
</style>
