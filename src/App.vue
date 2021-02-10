<template>
  <div class="flex flex-col items-center space-y-10">
    <h1 class="mt-10 text-5xl text-center">Pavel's reaction timer</h1>
    <button class="rounded-md shadow" :disabled="isPlaying" @click="startTimer">
      <p
        class="w-full flex items-center justify-center px-8 py-3 border border-transparent text-base font-medium rounded-md text-white bg-yellow-600 hover:bg-yellow-700 md:py-4 md:text-lg md:px-10"
      >
        Get started
      </p>
    </button>

		<div class="flex items-center">
      <p class="text-2xl font-semibold mr-8">Latest 5 scores:</p>

      <div class="flex space-x-4">
				<p v-for="score in scores" :key="score">{{ score }} ms</p>
			</div>
    </div>

    <Canvas v-if="isPlaying" :delay="delay" @sendResult="sendResult" />
  </div>
</template>

<script>
import { generateRandomValue } from "./utils/funcs";
import Canvas from "./components/Canvas";

export default {
  name: "App",
  components: {
    Canvas,
  },
  data: () => ({
    isPlaying: false,
    delay: null,
    scores: [],
  }),
  methods: {
    startTimer() {
      this.isPlaying = true;
      this.delay = generateRandomValue(1000, 5000);
    },
    sendResult(finalTime) {
      this.isPlaying = false;
      this.scores = [finalTime, ...this.scores.slice(0, 4)];
    },
  },
};
</script>

<style>
	body {
		background: #f1f1f1;
	}
</style>