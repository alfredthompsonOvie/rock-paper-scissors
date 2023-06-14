<template>
  <section class="scoreBoard">
    <h1 class="heading--scoreBoard">
      <span>Rock</span>
      <span>Paper</span>
      <span>Scissors</span>
    </h1>
    <section class="score">
      <p class="score--title">score</p>
      <p class="score--number">12</p>
    </section>
  </section>
</template>

<script setup>

</script>

<style scoped>
.scoreBoard {
  padding: 1em;
  border: 3px solid var(--HeaderOutline);
  max-width: 700px;
  width: 100%;
  margin-inline: auto;
  border-radius: 8px;
  display: flex;
  justify-content: space-between;
  align-items: center;
  flex-wrap: wrap;
  gap: 1em;
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
}
</style>