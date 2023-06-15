<template>
	<main>
		<!-- scoreboard -->
		<ScoreBoard />

		<!-- Arena -->
		<TriangleArena />

		<!-- Rules -->
		<button type="button" class="btn--rules" @click.prevent="showModal = true">
			Rules
		</button>

		<transition name="fade" appear>
			<RulesModal v-if="showModal" @closeModal="showModal = !showModal" />
		</transition>
	</main>
</template>

<script setup>
import { ref } from "vue";
import RulesModal from "./components/RulesModal.vue";
import ScoreBoard from "./components/ScoreBoard.vue";
import TriangleArena from "./components/TriangleArena.vue";

const showModal = ref(false);
</script>

<style scoped></style>
