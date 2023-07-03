<template>
	<section class="triangleArena">
		<transition name="fade" mode="out-in">
			<div class="chooseYourWeapon" v-if="!playerChoice">
				<button
					class="btn btn--paper"
					@click.prevent="declareWinner('paper')"
					ref="paper"
				>
					<span class="btn--imgContainer">
						<img
							src="@/assets/images/icon-paper.svg"
							alt="paper"
							class="weaponImg"
						/>
					</span>
				</button>

				<button
					class="btn btn--scissors"
					@click.prevent="declareWinner('scissors')"
					ref="scissors"
				>
					<span class="btn--imgContainer">
						<img
							src="@/assets/images/icon-scissors.svg"
							alt="paper"
							class="weaponImg"
						/>
					</span>
				</button>

				<button
					class="btn btn--rock"
					@click.prevent="declareWinner('rock')"
					ref="rock"
				>
					<span class="btn--imgContainer">
						<img
							src="@/assets/images/icon-rock.svg"
							alt="paper"
							class="weaponImg"
						/>
					</span>
				</button>
			</div>
			<div class="yourDestiny" v-else>
				<transition-group name="fade__group" appear mode="in-out">
					<section class="player selectedWeapon" key="1">
						<div
							class="selectedWeapon--btn__container"
							:class="{ winner: result === 'win' }"
						>
							<button
								class="btn btn--selectedWeapon"
								:class="`btn--${playerChoice}`"
								disabled
							>
								<span class="btn--imgContainer">
									<img
										:src="`${getImage(playerChoice)}`"
										alt="paper"
										class="weaponImg"
									/>
								</span>
							</button>
							<!-- <div class="circle__container">
								<div class="circle circle--sm"></div>
								<div class="circle circle--md"></div>
								<div class="circle circle--lg"></div>
							</div> -->

							<div class="pulse">
								<span style="--i: 0"></span>
								<span style="--i: 1"></span>
								<span style="--i: 2"></span>
								<span style="--i: 3"></span>
							</div>
						</div>
						<p class="player--choice">You Picked</p>
					</section>

					<section
						class="results"
						:class="{ showResults: isResultsReady }"
						key="2"
						v-if="isResultsReady"
					>
						<p class="resultDeclaration">
							{{
								result === "win"
									? "you win"
									: result === "lose"
									? "you lose"
									: "draw"
							}}
						</p>
						<button type="button" @click.prevent="playAgain" class="btn--reset">
							play again
						</button>
					</section>

					<section class="Ai selectedWeapon" key="3">
						<transition name="fade" mode="out-in">
							<div class="selection__base" v-if="!isAiWeaponSelected">
								<div class="selection__base__circle"></div>
							</div>

							<div
								class="selectedWeapon--btn__container"
								:class="{ winner: result === 'lose' }"
								v-else
							>
								<button class="btn" :class="`btn--${computerChoice}`" disabled>
									<span class="btn--imgContainer">
										<img
											:src="`${getImage(computerChoice)}`"
											alt="paper"
											class="weaponImg"
										/>
									</span>
								</button>

								<!-- <div class="circle__container">
									<div class="circle circle--sm"></div>
									<div class="circle circle--md"></div>
									<div class="circle circle--lg"></div>
								</div> -->
								<div class="pulse">
									<span style="--i: 0"></span>
									<span style="--i: 1"></span>
									<span style="--i: 2"></span>
									<span style="--i: 3"></span>
								</div>
							</div>
						</transition>

						<p class="Ai--choice">The House Picked</p>
					</section>
				</transition-group>
			</div>
		</transition>
	</section>
</template>

<script setup>
import { ref } from "vue";

const emits = defineEmits(["score"]);
const playerChoice = ref("");
const computerChoice = ref("");
const result = ref("");
const isWeaponSelected = ref(false);
const playerScore = ref(0);
const aiScore = ref(0);

// const classArr = ref([`btn--${computerChoice.value}`, `${isAiWeaponSelected.value ? '': 'btnAi--bg'}`])

// rules
/*
paper beats rock
rock beats scissors
scissors beats paper
*/
const rules = {
	paper: [{ rock: "win" }, { scissors: "lose" }, { paper: "draw" }],
	rock: [{ scissors: "win" }, { paper: "lose" }, { rock: "draw" }],
	scissors: [{ paper: "win" }, { rock: "lose" }, { scissors: "draw" }],
};

// options
const options = ["paper", "scissors", "rock"];

const paper = ref(null);
const scissors = ref(null);
const rock = ref(null);

const getComputerChoice = () => {
	const idx = Math.floor(Math.random() * 3);
	return options[idx];
};

const isAiWeaponSelected = ref(null);
const isResultsReady = ref(null);

const declareWinner = (weapon) => {
	isAiWeaponSelected.value = false;

	playerChoice.value = weapon;
	setTimeout(() => {
		computerChoice.value = getComputerChoice();
		let w = rules[playerChoice.value];
		let y = w.filter((e) => e).filter((e) => e[computerChoice.value])[0];
		let r = y[computerChoice.value];
		// console.log("pc", playerChoice.value);
		// console.log("cc", computerChoice.value);
		// console.log("w", w);
		// console.log("y", y);
		// console.log("r", r);
		r === "win" ? playerScore.value++ : r === "lose" ? aiScore.value++ : "";
		emits("score", [playerScore.value, aiScore.value]);
		result.value = r;
		// console.log(r);

		isAiWeaponSelected.value = true;
		showResults();
	}, 1500);
};
function getImage(name) {
	return new URL(`/src/assets/images/icon-${name}.svg`, import.meta.url).href;
}
const showResults = () => {
	setTimeout(() => {
		isResultsReady.value = true;
	}, 1000);
};
const playAgain = () => {
	isWeaponSelected.value = false;
	isResultsReady.value = false;
	playerChoice.value = "";
	computerChoice.value = "";
};
</script>

<style scoped></style>
