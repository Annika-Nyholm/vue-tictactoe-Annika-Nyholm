<template>
	<div class="popup">
		<div class="popup-content">
			<h2>{{ winner === 'Draw' ? 'Draw' : `${winner} wins!` }}</h2>
			<button @click="close">Close</button>
		</div>
	</div>
</template>

<script setup lang="ts">
const props = defineProps<{
	winner: string;
}>();

const emit = defineEmits<{
	(e: 'close'): void;
}>();

const close = () => {
	emit('close');
};
</script>

<style lang="scss" scoped>

</style>
