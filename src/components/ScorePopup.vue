<template>
    <div class="popup">
      <div class="popup-content">
        <Score :scores="scores" />
        <button @click="close">Close</button>
      </div>
    </div>
  </template>
  
  <script setup lang="ts">
  import Score from './Score.vue';
  
  const props = defineProps<{
    scores: { [key: string]: number };
  }>();
  
  const emit = defineEmits<{
    (e: 'close'): void;
  }>();

  const close = () => {
    emit('close');
  }
  </script>
  
  <style lang="scss" scoped>
  </style>