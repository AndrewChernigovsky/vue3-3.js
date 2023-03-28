<script setup>

// defineProps({
// 	time: String
// })




</script>

<script>

export default {
	emits: ['start', 'stop', 'reset'],
	data() {
		return {
			seconds: 0,
			minutes: null,
			hours: null,
			isRunning: false,
			secondomers: [],
			secondomer: {
				id: 1,
				times: {
					seconds: 0,
					minutes: null,
					hours: null,
				},
			}
		}
	},
	computed: {
		getSeconds: function () { return this.secondomer.times.seconds },
		getMinutes: function () { return this.secondomer.times.minutes },
		getHours: function () { return this.secondomer.times.hours },
		getID: function () { return this.secondomer.id }
	},
	methods: {
		timerStart() {
			let seconds = this.getSeconds
			let minutes = this.getMinutes
			let hours = this.getHours

			if (this.isRunning === true) {
				seconds++

				if (seconds >= 60) {
					seconds = 0
					minutes++
				}
				if (minutes  >= 60) {
					seconds = 0
					hours++
					minutes = 0
				}

				if (hours >= 24) {
					return hours = 0
				}

			} else {
				return
			}
		},

		start(event) {
			if (event) {
				this.isRunning = true

				setInterval(() => { this.timerStart() }, 1)
			}
		},
		stop(event) {
			if (event) {
				this.isRunning = false
				clearInterval(() => this.start())
			}
		},
		add(event) {
			if (event) {
				console.log(this.secondomers)
				return this.secondomers.push(this.secondomer)
			}
		},
	},
	watch: {
		seconds() {
			this.start
		}
	},

	mounted: function () {
		this.start()
	}
}


</script>

<template>
	<div id="clock" v-cloak>
		<!-- <div>
				<span class="time" v-if="hours != null">{{ hours + ':' }}</span>
				<span class="time" v-if="minutes != null">{{ minutes + ':' }}</span>
				<span class="time">{{ seconds }}</span>
			</div>

			<div class="btn-container">
				<button type="button" class="button" @click="start">Start</button>
				<button type="button" class="button" @click="stop">Stop</button>
			</div>

			 -->

		<div v-for="secondomer in secondomers" :key="secondomer.id">
			<div>
				<span class="time" v-if="secondomer.times.hours != null">{{ secondomer.times.hours + ':' }}</span>
				<span class="time" v-if="secondomer.times.minutes != null">{{ secondomer.times.minutes + ':' }}</span>
				<span class="time">{{ secondomer.times.seconds }}</span>
			</div>
			<div class="btn-container">
				<button type="button" class="button" @click="start">Start</button>
				<button type="button" class="button" @click="stop">Stop</button>
			</div>
		</div>

		<div class="btn-add">
			<button type="button" class="button" @click="add">Add</button>
		</div>

	</div>
</template>

<style lang="sass" scoped>
	button
		&:hover
			opacity: 0.7
			transition: 0.3s ease-in-out
			cursor: pointer
		&:active
			background-color: orange
		&:focus
			border: 2px solid orange

	[v-cloak]
		display: none

	#clock
		padding: 20px
		min-width: 310px

	.time 
		color: black
		font-size: 60px
		font-weight: bold

	.btn-container
		display: flex
		justify-content: flex-start
		align-items: center

		.button
			background-color: blue
			height: 50px
			color: white
			min-width: 100px
			font-size: 20px
			font-weight: bold

			&:not(:first-of-type)
				margin-left: 20px
	.btn-add
		background-color: gray
		min-width: 310px
		min-height: 200px
		display: flex
		justify-content: center
		align-items: center

		.button
			background-color: blue
			height: 50px
			color: white
			min-width: 100px
			font-size: 20px
			font-weight: bold

</style>
