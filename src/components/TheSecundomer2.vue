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
			secondomers: [],
			secondomer: {
				isRunning: false,
				start: false,
				times: {
					seconds: 0,
					minutes: null,
					hours: null,
				},
			}
		}
	},
	computed: {
	},
	methods: {
		timerStart(index) {
			if (this.secondomers[index].isRunning === true) {

				this.secondomers[index].times.seconds++

				if (this.secondomers[index].times.seconds >= 60) {
					this.secondomers[index].times.seconds = 0
					this.secondomers[index].times.minutes++
				}

				if (this.secondomers[index].times.minutes >= 60) {
					this.secondomers[index].times.seconds = 0
					this.secondomers[index].times.hours++
					this.secondomers[index].times.minutes = 0
				}

				if (this.secondomers[index].times.hours >= 24) {
					return this.secondomers[index].times.hours = 0
				}

			} else {
				return
			}

		},

		start(event, index) {
			if (event) {
				this.secondomers[index].isRunning  = true
				setInterval(() => { this.timerStart(index) }, 1)
				console.log(index, "Running")
			}
		},
		stop(event, index) {
			if (event) {
				this.secondomers[index].isRunning  = false
				clearInterval(() => { this.start(index) })
			}
		},
		reset(event, index) {
			if (event) {
				
				return this.secondomers[index] = {
					times: {
						seconds: 0,
						minutes: null,
						hours: null,
					}
				}
			}
		},
		add(event) {
			if (event) {
				
				return this.secondomers.push(this.secondomer)
			}
		},
		remove(event) {
			if (event) {
				
				return this.secondomers.pop(this.secondomer)
			}
		},
	},
	// watch: {
	// 	seconds() {
	// 		this.start
	// 	}
	// },

	mounted: function () {
		this.start()
		// this.secondomers.push(this.secondomer)
		this.secondomer = {
			isRunning: false,
			start: false,
			times: {
				seconds: 0,
				minutes: null,
				hours: null,
			},
		}
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
			</div> -->



		<div v-for="(secondomer, index) in secondomers" :key="secondomer">
			<div>
				<span class="time" v-if="secondomer.times.hours != null">{{ secondomer.times.hours + ':' }}</span>
				<span class="time" v-if="secondomer.times.minutes != null">{{ secondomer.times.minutes + ':' }}</span>
				<span class="time">{{ secondomer.times.seconds }}</span>
			</div>
			<div class="btn-container">
				<button type="button" class="button" @click="start($event, index)">Start</button>
				<button type="button" class="button" @click="stop($event, index)">Stop</button>
				<button type="button" class="button" @click="reset($event, index)">Reset</button>
			</div>
		</div>

		<div class="btn-actions">
			<button type="button" class="button" @click="add($event)">Add</button>
			<button type="button" class="button" @click="remove($event)">Remove</button>
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
	.btn-actions
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

			&:not(:first-child)
				margin-left: 20px

</style>
