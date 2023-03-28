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

				if (this.seconds >= 20) {
					this.seconds = 0
					this.minutes++
				}
				if (this.minutes >= 20) {
					this.seconds = 0
					this.hours++
					this.minutes = 0
					console.log(123123)
				}
			} else {
				return
			}
		},

		start(event) {
			if (event) {
				this.isRunning = true
				setInterval(() => { this.timerStart() }, 50)
			}
		},
		stop(event) {
			if (event) {
				this.isRunning = false
				clearInterval(() => this.start())
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
			<button type="button" @click="reset">Reset</button>
		</div>	
	</div>
</template>

<style lang="sass" scoped>
	[v-cloak]
		display: none

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

</style>
