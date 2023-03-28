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
		}
	},
	methods: {
		timerStart() {
			
			if (this.isRunning === true) {
				this.seconds++

				if (this.seconds >= 60) {
					this.seconds = 0
					this.minutes++
				}
				if (this.minutes >= 60) {
					this.seconds = 0
					this.hours++
					this.minutes = 0
				}

				if (this.hours >= 24) {
					return this.hours = 0
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
				return 
			}
		},
	},
	watch: {
		seconds() {
            this.start
        }
    },
	computed: {

	},
	mounted: function(){
		this.start()
    }
}


</script>

<template>
	<div id="clock" v-cloak>
		<div>
			<span class="time" v-if="hours != null">{{ hours + ':' }}</span>
			<span class="time" v-if="minutes != null">{{ minutes + ':' }}</span>
			<span class="time">{{ seconds }}</span>
		</div>
		
		<div class="btn-container">
			<button type="button" @click="start">Start</button>
			<button type="button" @click="stop">Stop</button>
		</div>

		<div class="btn-add">
            <button type="button" @click="add">Add</button>
        </div>


	</div>
</template>

<style lang="sass" scoped>
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

		button
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

		button
			background-color: blue
			height: 50px
			color: white
			min-width: 100px
			font-size: 20px
			font-weight: bold

</style>
	// this.secundomers.secundomer.times.seconds++

				// if (this.secundomers.secundomer.times.seconds >= 60) {
				// 	this.secundomers.secundomer.times.seconds = 0
				// 	this.secundomers.secundomer.times.minutes++
				// }
				// if (this.secundomers.secundomer.times.minutes >= 60) {
				// 	this.secundomers.secundomer.times.seconds = 0
				// 	this.secundomers.secundomer.times.hours++
				// 	this.secundomers.secundomer.times.minutes = 0
				// }

				// if (this.secundomers.secundomer.times.hours >= 24) {
				// 	return this.secundomers.secundomer.times.hours = 0
				// }