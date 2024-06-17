<template>
	<div class="score">
		<h2>Scores</h2>
		<p>Player X: {{ scores.X || 0 }}</p>
		<p>Player O: {{ scores.O || 0 }}</p>
	</div>
</template>

<script setup lang="ts">
const props = defineProps<{
	scores: { [key: string]: number };
}>();
</script>

<style lang="scss" scoped>
@import '../assets/styles/variables';
.score {
	text-align: center;
	margin-top: 20px;

}
</style>
