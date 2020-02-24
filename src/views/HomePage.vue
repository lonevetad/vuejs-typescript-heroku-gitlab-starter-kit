<template>
	<div>
		<strong>Computed: {{computedInfo}}</strong>
		<br />
		<strong>value from Vuex: {{example.currentExampleValue}}</strong>
		<br />
		<button @click="showAlert()">Click Me!</button>
		<br />
		<button @click="triggerIncrement()">INCREMENT!</button>
		<br />
		<button @click="goTo('about')">Go to About!</button>
		<br />
		<label>
			<button @click="goTo('todos')">Go to Todos page</button> (Testing storing arrays on vuex and dialog within components)
		</label>
		<br />
		<button @click="goTo('matrix')">Go to Matrix!</button>
		<br />
	</div>
</template>
<script lang="ts">
import { Vue, Component } from "vue-class-decorator";

import { example } from "@/vuex";

@Component({})
export default class HomePage extends Vue {
	example = example;

	mounted(): void {
		console.log("mounted");
	}

	get computedInfo(): string {
		return "Computed" + " " + "example";
	}

	showAlert(): void {
		alert("Well done");
	}


	triggerIncrement(): void {
		this.example.bicrement();
	}
	goTo(where: string): void {
		this.$router.push({
			name: where
		});
	}
}
</script>
<style lang="scss" scoped>
</style>