<template>
	<section>
		<div class="chooseYourWeapon" v-if="!playerChoice">
			<button 
			class="btn btn--paper"
			@click.prevent="declareWinner('paper')"
			ref="paper"
			>
				<span class="btn--imgContainer">
					<img src="@/assets/images/icon-paper.svg" alt="paper" class="weapon"/>
				</span>
			</button>

			<button 
			class="btn btn--scissors"
			@click.prevent="declareWinner('scissors')"
			ref="scissors"
			>
				<span class="btn--imgContainer">
					<img src="@/assets/images/icon-scissors.svg" alt="paper" class="weapon"/>
				</span>
			</button>

			<button 
			class="btn btn--rock"
			@click.prevent="declareWinner('rock')"
			ref="rock"
			>
				<span class="btn--imgContainer">
					<img src="@/assets/images/icon-rock.svg" alt="paper" class="weapon"/>
				</span>
			</button>
		</div>
		<div class="yourDestiny" v-else>
			<!-- display flex jcc gap3em -->
			<section class="player">
				<button 
				class="btn"
				:class="`btn--${playerChoice}`"
				@click.prevent="declareWinner('paper')"
				ref="paper"
				>
					<span class="btn--imgContainer">
						<img :src="`${getImage(playerChoice)}`" alt="paper" class="weapon"/>
					</span>
				</button>
				<p class="player--choice">You Picked</p>
			</section>

			<section class="results">
				<p class="resultDeclaration">you {{ result }}</p>
				<button
				type="button"
				@click.prevent=""
				class="btn--reset"
				>play again</button>
			</section>

			<section class="Ai">
				<button 
				class="btn"
				:class="`btn--${computerChoice}`"
				@click.prevent="declareWinner('scissors')"
				ref="scissors"
				>
					<span class="btn--imgContainer">
						<img :src="`${getImage(computerChoice)}`" alt="paper" class="weapon"/>
					</span>
				</button>
				<p class="Ai--choice">The House Picked</p>
			</section>


		</div>
	</section>
</template>

<script setup>
import { ref } from 'vue';

// const emits = defineEmits(['selected']);
const playerChoice = ref('');
const computerChoice = ref('');
const result = ref('');
const isWeaponSelected = ref(false);


// rules
/*
paper beats rock
rock beats scissors
scissors beats paper
*/
const rules = {
	paper: [{rock: 'wins'}, {scissors: 'lose'}, {paper:'draw'}],
	rock: [{ scissors: 'wins' }, {paper: 'lose'}, {rock:'draw'}],
	scissors: [{ paper: 'wins' }, {rock: 'lose'}, {scissors:'draw'}],
}

// options
const options = ['paper', 'scissors', 'rock'];

const paper = ref(null);
const scissors = ref(null);
const rock = ref(null);

const getComputerChoice = () => {
	const idx = Math.floor(Math.random() * 3)
	return options[idx];
}


const declareWinner = (weapon) => {
	// playerChoice.value = weapon;

	playerChoice.value = weapon;
	computerChoice.value = getComputerChoice();
	let w = rules[playerChoice.value];
	let y = w.filter(e => e).filter(e => e[computerChoice.value])[0]
	let r = y[computerChoice.value]
	console.log("pc", playerChoice.value);
	console.log("cc", computerChoice.value);
	console.log("w", w);
	console.log("y", y);
	console.log("r", r);
	result.value = r
}
function getImage(name) {
	return new URL(`/src/assets/images/icon-${name}.svg`, import.meta.url).href
}
</script>

<style scoped></style>
