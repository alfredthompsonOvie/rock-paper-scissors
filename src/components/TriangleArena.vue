<template>
	<section>
		<div class="chooseYourWeapon">
			<button 
			class="btn btn--paper"
			@click.prevent="playerSelected">
				<span class="btn--imgContainer">
					<img src="@/assets/images/icon-paper.svg" alt="paper" class="weapon"/>
				</span>
			</button>

			<button 
			class="btn btn--scissors"
			@click.prevent="playerSelected">
				<span class="btn--imgContainer">
					<img src="@/assets/images/icon-scissors.svg" alt="paper" class="weapon"/>
				</span>
			</button>

			<button 
			class="btn btn--rock"
			@click.prevent="playerSelected">
				<span class="btn--imgContainer">
					<img src="@/assets/images/icon-rock.svg" alt="paper" class="weapon"/>
				</span>
			</button>
		</div>
		<div class="yourDestiny">
			<!-- display flex jcc gap3em -->
		</div>
	</section>
</template>

<script setup>

const emits = defineEmits(['selected'])

const playerSelected = (e) => {
	console.log(e);
	// 387 274
}
</script>

<style scoped></style>
