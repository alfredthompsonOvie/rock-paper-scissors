<template>
  <section class="scoreBoard">
    <!-- <h1 class="heading--scoreBoard">
      <span>Rock</span>
      <span>Paper</span>
      <span>Scissors</span>
    </h1> -->
    <img src="@/assets/images/logo.svg" alt="logo" v-if="level === 'normal'">
    <img src="@/assets/images/logo-bonus.svg" alt="bonus logo" v-else>
    <section class="score">
      <p class="score--title">score</p>
      <p class="score--number">
        <span>{{ playerScore }}</span> : 
        <span>{{ aiScore }}</span>
      </p>
    </section>
  </section>
</template>

<script setup>
import { watch, ref } from 'vue';

const props = defineProps({
  score: {
    type: Array,
    required: true
  },
  level: {
    type: String,
    required: true
  }
});

const playerScore = ref(0);
const aiScore = ref(0);

watch(props, () => {
  // console.log(props.score);
  playerScore.value = props.score[0];
  aiScore.value = props.score[1];
})
// watchEffect(() => {
//   console.log(props);
//   console.log(props.score);
//   console.log(props.score[0]);
//   console.log(props.score[1]);
//     playerScore.value = props.score[0];
//   aiScore.value = props.score[1];
// })

// const playerScore = computed(() => props.score[0]);
// const aiScore = computed(() => props.score[1]);

// console.log(playerScore.value);

</script>

<style scoped>
.scoreBoard {
  padding: .5em;
  border: 3px solid var(--HeaderOutline);
  max-width: 500px;
  width: 100%;
  margin-inline: auto;
  border-radius: 8px;
  display: flex;
  justify-content: space-between;
  align-items: center;
  flex-wrap: wrap;
  gap: 1em;
  position: relative;
  z-index: 10;
}
.heading--scoreBoard {
  color: #fff;
  display: inline-block;
  line-height: 0.8;
  text-transform: uppercase;
}
.heading--scoreBoard span {
  display: block;
}

.score {
  background-color: #fff;
  padding: 1em 2em;
  border-radius: 8px;
  text-align: center;
}
.score--title {
  font-size: .9rem;
  color: var(--ScoreText);
  font-weight: var(--fw-medium);
}
.score--number {
  font-size: 2.4rem;
  font-weight: var(--fw-bold);
  color: var(--DarkText);
  display: flex;
  align-items: center;
}
</style>