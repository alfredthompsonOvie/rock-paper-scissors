<template>
	<main>
		<!-- select game level -->
		<section class="cover" v-if="showCover">
			<section class="cover__content">
				<!-- <h1>Rock Paper Scissors</h1> -->
				<img src="@/assets/images/logo.svg" alt="logo">
				<p>Choose Your Destiny</p>
				<section>
					<button 
					type="button"
					@click.prevent="setGameMode('normal')"
					class="gameModeBtn gameModeBtn--normal"
					>
					Earth
				</button>
					<button 
					type="button"
					@click.prevent="setGameMode('hard')"
					class="gameModeBtn  gameModeBtn--hard"
					>
					Mars
				</button>
				</section>
			</section>
			<!-- attribution -->
		</section>
		<!-- game starts -->
		<!-- scoreboard -->
		<ScoreBoard :score="score" :level="gameMode"/>
		<template v-if="gameMode === 'normal'">
	
			<!-- Arena -->
			<TriangleArena @score="(s)=> score = [...s]" @gameMode="changeDifficulty"/>
	
			<!-- Rules -->
			<button type="button" class="btn--rules" @click.prevent="showModal = true">
				Rules
			</button>
	
			<transition name="slide" appear>
				<RulesModal v-if="showModal" @closeModal="showModal = !showModal" />
			</transition>
		</template>
		<template v-if="gameMode=== 'hard'">
			<div>
				hard
			</div>
		</template>
	</main>
</template>

<script setup>
import { onMounted, ref,} from "vue";
import RulesModal from "./components/RulesModal.vue";
import ScoreBoard from "./components/ScoreBoard.vue";
import TriangleArena from "./components/TriangleArena.vue";

const showModal = ref(false);
const score = ref([]);

const gameMode = ref(null);
const showCover = ref(null);

// const updateScore = (s) => {
// 	score.value = [...s];
// }

onMounted(() => {
	gameMode.value = false;
	showCover.value = true;
})

const setGameMode = (mode) => {
	gameMode.value = mode;
	showCover.value = false; 
	// console.log(gameMode.value);
}
const changeDifficulty = () => {
	showCover.value = true; 
	gameMode.value = false;
}

</script>

<style scoped></style>
