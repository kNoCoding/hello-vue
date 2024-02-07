<template>
  <header>
    <p>im the header</p>
  </header>

  <main>
    <ShowTime />
    <CountDown v-bind:myProps="`this is a prop`" v-bind:targetTime="Date.now() + 1000 * 11" @due="handleDueEvent" />
  </main>

  <footer>
    <p>im the footer</p>
  </footer>
</template>

<script setup>
import ShowTime from './components/ShowTime.vue'
import CountDown from './components/CountDown.vue'

function handleDueEvent() {
  console.log('Countdown is due!')
}

</script>

<style scoped></style>
