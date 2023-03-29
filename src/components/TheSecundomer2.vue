<script setup>
</script>

<script>

export default {
	data() {
		return {
			secondomers: [],

		}
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
				this.secondomers[index].isRunning = true
				this.secondomers[index].on = true
				setInterval(() => { this.timerStart(index) }, 1000)
			}
		},
		stop(event, index) {
			if (event) {
				this.secondomers[index].isRunning = false
				this.secondomers[index].on = false
				clearInterval(() => { this.start(index) })
			}
		},
		reset(event, index) {
			if (event) {
				this.secondomers[index].on = false
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
				this.secondomer = {
					isRunning: false,
					start: false,
					on: false,
					times: {
						seconds: 0,
						minutes: null,
						hours: null,
					},
				}
				return this.secondomers.push(this.secondomer)
			}
		},
		remove(event) {
			if (event) {

				return this.secondomers.pop(this.secondomer)
			}
		},
	},

	mounted: function () {
		this.start()
	}
}


</script>

<template>
	<div id="clock" v-cloak>
		<div class="clock-wrapper">
			<div v-for="(secondomer, index) in secondomers" :key="secondomer" class="secondomer">
				<div class="secondomer-wrapper" :class="{ 'on': secondomer.on }">
					<div class="time-wrapper">
						<span class="time" v-if="secondomer.times.hours != null">{{ secondomer.times.hours + ':' }}</span>
						<span class="time" v-if="secondomer.times.minutes != null">{{ secondomer.times.minutes + ':'
						}}</span>
						<span class="time">{{ secondomer.times.seconds }}</span>
					</div>
					<div class="btn-container">
						<button type="button" class="button" @click="start($event, index)"
							v-if="!this.secondomers[index].isRunning">
							<svg width="20" height="20" viewBox="0 0 20 20" xmlns="http://www.w3.org/2000/svg">
								<path d="M0 20V0L17 10L0 20Z" fill="#9E9E9E" />
							</svg>
						</button>
						<button type="button" class="button" @click="stop($event, index)"
							v-if="this.secondomers[index].isRunning">
							<svg width="20" height="20" viewBox="0 0 20 20" xmlns="http://www.w3.org/2000/svg">
								<rect x="7" width="3" height="20" fill="#9E9E9E" />
								<rect width="3" height="20" fill="#9E9E9E" />
							</svg>

						</button>
						<button type="button" class="button" @click="stop($event, index)">
							<svg width="20" height="20" viewBox="0 0 20 20" fill="none" xmlns="http://www.w3.org/2000/svg">
								<rect width="20" height="20" fill="#9E9E9E" />
							</svg>

						</button>
						<!-- <button type="button" class="button" @click="reset($event, index)">Reset</button> -->
					</div>
				</div>

			</div>
			<div class="btn-actions">
				<button type="button" class="button" @click="add($event)">
					<svg width="20" height="20" viewBox="0 0 20 20" xmlns="http://www.w3.org/2000/svg">
						<rect x="8.5" width="3" height="20" fill="#9E9E9E" />
						<rect y="11.5" width="3" height="20" transform="rotate(-90 0 11.5)" fill="#9E9E9E" />
					</svg>
				</button>
				<!-- <button type="button" class="button" @click="remove($event)">Remove</button> -->
			</div>
		</div>
	</div>
</template>

<style lang="sass" scoped>
	@import '../assets/styles/variables.sass'
	[v-cloak]
		display: none
	.clock-wrapper
		padding: 20px
		display: grid
		grid-template-columns: 1fr
		gap: 20px

		@media  screen and (min-width: 768px)
			grid-template-columns: 1fr 1fr
		

		@media  screen and (min-width: 1024px)
			grid-template-columns: 1fr 1fr 1fr
		
	.secondomer
		background-color: $lightGrey
		margin-bottom: 20px
		padding: 20px
		min-height: 120px
		min-width: 100%

	
	.secondomer-wrapper
		&.on
			.time-wrapper 
				border-bottom: 1px solid white
			.time 
				color: white
			svg *
				fill: white

	button
		&:hover
			opacity: 0.7
			transition: 0.3s ease-in-out
			cursor: pointer
		&:active
			background-color: orange
		&:focus
			border: 2px solid orange


	.time-wrapper 
		text-align: center
		padding-bottom: 10px
		border-bottom: 1px solid $lightGrey1
		margin-bottom: 10px
	.time 
		color: $lightGrey1
		font-size: 22px
		text-align: center
	
	.time.on
		color: white
	.btn-container
		display: flex
		justify-content: center
		align-items: center

		.button
			background: transparent
			border: none
			outline: none
			height: 50px
			color: white
			min-width: 100px
			font-size: 20px
			font-weight: bold

			&:not(:first-of-type)
				margin-left: 20px
	.btn-actions
		background-color: gray
		min-width: 260px
		max-width: 50%
		min-height: 120px
		display: flex
		justify-content: center
		align-items: center
		padding: 13px
		margin-bottom: 20px

		.button
			background: transparent
			border: none
			outline: none
			min-height: inherit
			color: white
			min-width: 100%
			font-size: 20px
			font-weight: bold

			&:not(:first-child)
				margin-left: 20px

</style>
