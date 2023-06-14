<template>
  <main>
    <!-- Welcome -->
    <ScoreBoard />

    <RulesModal v-if="showModal" @closeModal="showModal = !showModal"/>
  </main>
</template>

<script setup>
import { ref } from 'vue';
import RulesModal from './components/RulesModal.vue';
import ScoreBoard from './components/ScoreBoard.vue';

const showModal = ref(false);
</script>

<style  scoped>

</style>