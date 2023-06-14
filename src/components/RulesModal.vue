<template>
	<section class="modal">
		<section class="modal__contents">
      <h1 class="heading--modal">Rules</h1>

			<img src="@/assets/images/image-rules.svg" alt="rules" class="rules__img"/>

      <button type="button" @click.prevent="closeModal">
        <img src="@/assets/images/icon-close.svg" alt="close modal" />
      </button>
		</section>
	</section>
</template>

<script setup>
const emits = defineEmits(['closeModal'])

const closeModal = () => {
  emits('closeModal');
}
</script>

<style scoped>
.modal {
	position: fixed;
	top: 0;
	left: 0;
	width: 100vw;
	height: 100vh;
	background-color: rgba(0, 0, 0, 0.4);
}
.modal__contents {
	width: 100%;
  height: 100vh;
	background-color: white;
	padding: 4em 1.5em;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: space-between;
}
.heading--modal {
	font-size: clamp(1.2rem, 8vw, 1.6rem);
  text-transform: uppercase;
	color: var(--DarkText);
	font-weight: var(--fw-bold);
}

@media (min-width: 768px) {
	.modal {
		display: grid;
		place-items: center;
		padding: 1em;
	}
	.modal__contents {
		max-width: 350px;
		width: 100%;
		padding: 1.5em;
		border-radius: 8px;

    height: initial;
    display: grid;
    grid-template-columns: repeat(2, 1fr);
    grid-template-rows: repeat(2, auto);
    gap: 1em;
	}
	.heading--modal {
    grid-column: 1;
    grid-row: 1;
    justify-self: start;
	}
	button {
    grid-column: 2;
    grid-row: 1;
    justify-self: end;
	}
  .rules__img {
    grid-row: 2;
    grid-column: 1/-1;
  }
}
</style>
