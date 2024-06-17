<template>
	<div class="cell" @click="handleClick">
		{{ value }}
	</div>
</template>

<script setup lang="ts">
const props = defineProps<{
	value: string | null;
	index: number;
}>();

const emit = defineEmits<{
	(e: 'cell-click', index: number): void;
}>();

const handleClick = () => {
  if (props.value === null) {
    emit('cell-click', props.index);
  }
};
</script>

<style lang="scss" scoped>
@import '../assets/styles/variables';

.cell {
	width: 120px;
	height: 120px;
	display: flex;
	justify-content: center;
	align-items: center;
	border: 2px solid $color1;
	font-family: 'Shadows Into Light', cursive;
	font-size: 4rem;
	color: $color1;
	background-color: $color5;
	cursor: pointer;
	transition: background-color 0.2s ease;

	&:hover {
		background-color: $color4;
	}
}
</style>
