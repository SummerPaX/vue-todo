<script setup lang="ts">
import { ref } from "vue";
import AddTodo from "./AddTodo.vue";
import TodoItem from "./TodoItem.vue";
import { TypeTodoItem } from "../interfaces";
import draggable from "vuedraggable";

const todoItems = ref<TypeTodoItem[]>([]);

const toggleDone = (todoItem: TypeTodoItem) => {
	const index = todoItems.value.indexOf(todoItem);
	todoItems.value[index].done = !todoItems.value[index].done;
	todoItems.value.splice(index, 1);
	todoItem.done ? todoItems.value.push(todoItem) : todoItems.value.unshift(todoItem);
};
</script>

<template>
	<div class="w-screen flex flex-col items-center p-12 gap-4">
		<h1 class="text-4xl">📝 Todo Liste mit Draggable</h1>
		<div class="p-4 space-y-2">
			<AddTodo @todoAdded="(todoItem) => todoItems.unshift(todoItem)"></AddTodo>
			<draggable :list="todoItems" item-key="id" animation="200" ghostClass="ghost">
				<template #item="{ element: todoItem }">
					<TodoItem
						:key="todoItem.id"
						:todo="todoItem"
						@delete="todoItems = todoItems.filter((item) => item.id !== todoItem.id)"
						@toggledone="toggleDone(todoItem)"
					></TodoItem>
				</template>
			</draggable>
		</div>
	</div>
</template>

<style scoped>
.ghost {
	opacity: 50%;
}
</style>
