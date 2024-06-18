<template>
	<section>
		<Home v-if="!gameStarted" @start-game="startGame" />
		<GameBoard
			v-else
			:playerX="playerX"
			:playerO="playerO"
			:gameStarted="gameStarted"
			@update-score="updateScore"
			@toggle-score-popup="toggleScorePopup"
			@new-game="newGame"
			@reset-game="resetGame"
			@game-won="setWinner"
			ref="gameboard"
		/>
		<ScorePopup
			v-if="showScorePopup"
			:scores="scores"
			@close="toggleScorePopup"
		/>
		<WinPopup v-if="winner" :winner="winner" @close="resetGame" />
	</section>
</template>

<script setup lang="ts">
import { ref, onMounted } from 'vue';
import Home from './components/Home.vue';
import GameBoard from './components/GameBoard.vue';
import ScorePopup from './components/ScorePopup.vue';
import WinPopup from './components/WinPopup.vue';

const playerX = ref(localStorage.getItem('playerX') || '');
const playerO = ref(localStorage.getItem('playerO') || '');
const gameStarted = ref(playerX.value && playerO.value ? true : false);
const showScorePopup = ref(false);
const scores = ref(JSON.parse(localStorage.getItem('scores') || '{}'));
const winner = ref<string | null>(null);
const gameboard = ref<InstanceType<typeof GameBoard> | null>(null);

onMounted(() => {
	const savedPlayerX = localStorage.getItem('playerX');
	const savedPlayerO = localStorage.getItem('playerO');
	const savedBoard = localStorage.getItem('board');

	if (savedPlayerX && savedPlayerO && savedBoard) {
		playerX.value = savedPlayerX;
		playerO.value = savedPlayerO;
		gameStarted.value = true;
	}
});

const startGame = (players: { playerX: string; playerO: string }) => {
	playerX.value = players.playerX;
	playerO.value = players.playerO;
	localStorage.setItem('playerX', playerX.value);
	localStorage.setItem('playerO', playerO.value);
	gameStarted.value = true;
};

const updateScore = (winner: string) => {
	if (!scores.value[winner]) {
		scores.value[winner] = 0;
	}
	scores.value[winner]++;
	localStorage.setItem('scores', JSON.stringify(scores.value));
};

const setWinner = (winnerValue: string) => {
	winner.value =
		winnerValue === 'X'
			? playerX.value
			: winnerValue === 'O'
			? playerO.value
			: 'Draw';
};

const toggleScorePopup = () => {
	showScorePopup.value = !showScorePopup.value;
};

const resetGame = () => {
	gameboard.value?.resetBoard();
	winner.value = null;
};

const newGame = () => {
	localStorage.clear();
	gameStarted.value = false;
	playerX.value = '';
	playerO.value = '';
	scores.value = {};
	winner.value = null;
};
</script>

<style lang="scss" scoped></style>
