<template>
	<article class="home">
		<h1>Welcome to TicTacToe-do!</h1>
		<form @submit.prevent="submit">
			<label>
				Player X:
			</label>
			<input v-model="playerX" required />
			<label>
				Player O:
			</label>
			<input v-model="playerO" required />
			<button type="submit">Start game</button>
		</form>
	</article>
</template>

<script setup lang="ts">
import { ref } from 'vue';

const emit = defineEmits<{
	(e: 'start-game', players: { playerX: string; playerO: string }): void;
}>();

const playerX = ref('');
const playerO = ref('');
const submit = () => {
	emit('start-game', { playerX: playerX.value, playerO: playerO.value });
};
</script>

<style lang="scss" scoped>
@import '../assets/styles/variables';

.home {
	font-family: 'Shadows Into Light', cursive;
	text-align: center;
	margin-top: 50px;

	h1 {
		font-size: 3rem;
		color: $color1;
		text-shadow: 
		0 1px 0 $color4,
		0 2px 0 lighten($color4, 5%),
		0 3px 0 lighten($color4, 10%),
		0 4px 0 lighten($color4, 15%),
		0 5px 0 lighten($color4, 20%),
		0 6px 1px rgba($color1, 0.1),
		0 0 5px rgba($color1, 0.1),
		0 1px 3px rgba($color1, 0.3),
		0 3px 5px rgba($color1, 0.2), 
		0 5px 10px rgba($color1, 0.25),
		0 10px 10px rgba($color1, 0.2), 
		0 20px 20px rgba($color1, 0.15),
		2px 2px 2px rgba($color1, 0);
	}
}

form {
	display: flex;
	flex-direction: column;
	align-items: center;
	font-family: 'Roboto', sans serif;
	font-size: 1.3rem;
	color: $color1;

	label {
		text-align: left;
		margin: 4px 0;
		width: 204px;
	}
	input {
		margin-bottom: 8px;
		padding: 8px;
		font-size: 1rem;
		font-family: 'Roboto', sans serif;
		font-weight: 500;
		color: $color1;
		background-color: $color5;
		border-radius: 4px;
		transition: background-color 0.3s ease;

		&:hover {
			background-color: $color3;
		}
	}
}
</style>
