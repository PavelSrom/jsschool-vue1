<template>
	<div
		v-if="show"
		@click="stopTimer"
		class="w-2/4 h-96 bg-green-500 mx-auto flex justify-center items-center text-white rounded-3xl"
	>
		<p class="text-3xl font-light">Click me</p>
	</div>
</template>

<script>
export default {
	props: {
		delay: Number
	},
	data: () => ({
		show: false,
		timer: null,
		reactionTime: 0
	}),
	methods: {
		startTimer() {
			this.timer = setInterval(() => {
				this.reactionTime += 10
			}, 10);
		},
		stopTimer() {
			clearInterval(this.timer)
			this.$emit('sendResult', this.reactionTime)
		}
	},
	mounted() {
		setTimeout(() => {
			this.show = true
			this.startTimer()
		}, this.delay);
	},
}
</script>