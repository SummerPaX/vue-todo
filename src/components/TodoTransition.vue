<script setup lang="ts">
import { ref } from "vue";
import AddTodo from "./AddTodo.vue";
import TodoItem from "./TodoItem.vue";
import { TypeTodoItem } from "../interfaces";

const todoItems = ref<TypeTodoItem[]>([]);
</script>

<template>
	<div
		class="w-screen flex flex-col items-center p-12 gap-4"
	>
		<h1 class="text-4xl">📝 Todo Liste mit TransitionGroup</h1>
		<div class="p-4 space-y-2">
			<AddTodo @todoAdded="(todoItem) => todoItems.unshift(todoItem)"></AddTodo>
			<TransitionGroup class="block relative space-y-1" name="list" tag="div">
				<TodoItem
					v-for="todoItem in todoItems"
					:key="todoItem.id"
					:todo="todoItem"
					@delete="todoItems = todoItems.filter((item) => item.id !== todoItem.id)"
					@toggledone="
						() => {
							todoItem.done = !todoItem.done;
							todoItems.splice(todoItems.indexOf(todoItem), 1);
							todoItem.done ? todoItems.push(todoItem) : todoItems.unshift(todoItem);
						}
					"
				></TodoItem>
			</TransitionGroup>
		</div>
	</div>
</template>

<style scoped>
.list-move, /* apply transition to moving elements */
.list-enter-active,
.list-leave-active {
	transition: all 0.5s ease;
}

.list-enter-from,
.list-leave-to {
	opacity: 0;
	transform: translateX(30px);
}
.list-leave-active {
	position: absolute;
}
</style>
