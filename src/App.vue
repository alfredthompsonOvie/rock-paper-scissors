<template>
	<main>
		<!-- scoreboard -->
		<ScoreBoard />

		<!-- interaction -->
		<section>
			<div class="chooseYourWeapon">
				<button class="btn btn--paper">
					<span class="btn--imgContainer">
						<img src="@/assets/images/icon-paper.svg" alt="paper" />
					</span>
				</button>

				<button class="btn btn--scissors">
					<span class="btn--imgContainer">
						<img src="@/assets/images/icon-scissors.svg" alt="paper" />
					</span>
				</button>

				<button class="btn btn--rock">
					<span class="btn--imgContainer">
						<img src="@/assets/images/icon-rock.svg" alt="paper" />
					</span>
				</button>
			</div>
		</section>

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

const showModal = ref(false);
</script>

<style scoped></style>
