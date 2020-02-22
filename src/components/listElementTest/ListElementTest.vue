<template>
	<div>
		<button @click="toggleListCancellability">Toggle list cancellability</button>
		<p>Your items</p>
		<ul v-if="isListShowing">
			<li class="m-2" v-for="(e, i) in this.todos.allTodos" v-bind:key="i">
				<span class="horizContainer m-2">
					<i>{{i}} :</i>
					<b>{{e.id}}</b>
					<h4>{{e.text}}</h4>
					<button @click="removeAt(i)">Delete me</button>
				</span>
			</li>
		</ul>
	</div>
</template>


<script lang="ts">
import { Vue, Component, Prop } from "vue-class-decorator";
import { todos } from "@/vuex";
import { Todo } from "@/store/todos"
import EventBusGolbal from "@/eventBus";

@Component({})
export default class ListElementTest extends Vue {
	@Prop({}) todos = todos;
	private isListShowing: boolean = true;

	mounted(): void {
		EventBusGolbal.$on("toggleListVisualization", this.toggleListVisualizationHandler);
	}

	removeAt(i: number): void {
		this.todos.removeAt(i);
	}

	todosCount(): number {
		return this.todos.todosAmount;
	}

	/**Event handler */
	toggleListVisualizationHandler(msg: any): void {
		console.log(JSON.stringify(msg));
		this.isListShowing = !this.isListShowing;
	}

	/**Communicate to add-remove list component to toggle the ability to remove items from the list*/
	toggleListCancellability(): void {
		EventBusGolbal.$emit('toggleListCancellability', "Toggle the list cancellability");
	}
}
</script>




<style lang="scss" scoped>
h4 {
	margin: 0px;
}
li {
	list-style-type: none;
}
.horizContainer {
	display: flex;
	flex-direction: row;
	flex-wrap: nowrap;
	justify-content: flex-start;
	align-items: flex-start;
}
.horizContainer > * {
	margin: 2px;
}
.m-2 {
	margin: 1vh;
}
</style>