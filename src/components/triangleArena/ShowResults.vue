<template>
	<section>
		<!-- display flex jcc gap3em -->
		<section class="player selectedOption">
			<button
				class="btn"
				:class="`btn--${playerChoice}`"
				@click.prevent="declareWinner('paper')"
				ref="paper"
			>
				<span class="btn--imgContainer">
					<img :src="`${getImage(playerChoice)}`" alt="paper" class="weapon" />
				</span>
			</button>
			<p class="player--choice">You Picked</p>
		</section>

		<section class="results">
			<p class="resultDeclaration">you {{ result }}</p>
			<button 
      type="button" 
      @click.prevent="playAgain" 
      class="btn--reset"
      >
				play again
			</button>
		</section>

		<section class="Ai selectedOption">
			<button
				class="btn"
				:class="`btn--${computerChoice}`"
				@click.prevent="declareWinner('scissors')"
				ref="scissors"
			>
				<span class="btn--imgContainer">
					<img
						:src="`${getImage(computerChoice)}`"
						alt="paper"
						class="weapon"
					/>
				</span>
			</button>
			<p class="Ai--choice">The House Picked</p>
		</section>
	</section>
</template>

<script setup>

const playAgain = () => {
  
}
</script>

<style scoped></style>
