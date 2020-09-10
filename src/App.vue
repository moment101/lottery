<template>
	<div id="app">
		<lottie :options="defaultOptions" :width="150" :height="150" v-on:animCreated="handleAnimation" />
		<Greeting />
		<div class="container operate">
			<div class="row">
				<div class="col-6 text-left">
					<label>需要抽出幾位：</label> <input type="text" class="number-elected" v-model="needSelectedNumber">
				</div>
				<div class="col-4"></div>
				<div class="col-2 text-right">
					<button type="button" class="btn btn-primary" v-on:click="start">Go</button>
				</div>
			</div>
		</div>

		<div class="container">
			<div class="row">
				<div class="col-8">
					<Candidate :updateItems="updateItems" />
				</div>
				<div class="col-4">
					<Elected :selectedItems_str="selectedItems_str" />
				</div>
			</div>
		</div>
	</div>

</template>

<script>
	import _ from 'lodash'
	import lottie from 'vue-lottie'
	import Anim from "./assets/23054-search.json"
	import Greeting from './components/Greeting.vue'
	import Candidate from './components/Candidate.vue'
	import Elected from './components/Elected.vue'

	export default {
		name: 'App',
		data() {
			return {
				rawText: "",
				items: [],
				needSelectedNumber: 1,
				shuffledItems: [],
				selectedItems: [],
				selectedItems_str: "",
				defaultOptions: {
					animationData: Anim,
					loop: true,
					autoplay: true
				},
				defaultAnim: ''
			}
		},
		components: {
			Greeting,
			Candidate,
			Elected,
			'lottie': lottie
		},
		methods: {
			start() {
				if (this.needSelectedNumber > this.items.length) {
					alert("抽出的數量不正確")
				} else {
					console.log("start")
					this.shuffleAnswers()
					this.select()
				}
			},
			updateItems(items) {
				this.rawText = items
				this.items = this.rawText.split('\n')
				console.log(this.items.length)
				console.log(this.rawText)
			},
			shuffleAnswers() {
				let raw_items = _.shuffle(this.items)
				this.shuffledItems = []
				for (let i = 0; i < raw_items.length; i++) {
					if (raw_items[i] !== "") {
						this.shuffledItems.push(raw_items[i])
					}
				}
				console.log(this.shuffledItems)
			},
			select() {
				this.selectedItems = []
				for (let i = 0; i < this.needSelectedNumber; i++) {
					this.selectedItems.push(this.shuffledItems[i])
				}
				console.log(this.selectedItems)
				this.selectedItems_str = this.selectedItems.join('\n')
			},
			handleAnimation(anim) {
				this.defaultAnim = anim;
			}
		}
	}
</script>

<style>
	#app {
		font-family: Avenir, Helvetica, Arial, sans-serif;
		-webkit-font-smoothing: antialiased;
		-moz-osx-font-smoothing: grayscale;
		text-align: center;
		color: #2c3e50;
		margin-top: 60px;
	}

	.operate {
		margin-bottom: 10px;
	}

	.number-elected {
		border-color: aliceblue;
		background-color: lightblue;
	}
</style>
