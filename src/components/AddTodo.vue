<script setup lang="ts">
import { ref } from "vue";
import { TypeTodoItem } from "../interfaces";
import { v4 as uuidv4 } from "uuid";

const input = ref("");

const emit = defineEmits<{
	(e: "todoAdded", item: TypeTodoItem): void;
}>();

function emitTodo() {
	emit("todoAdded", {
		id: uuidv4(),
		content: input.value,
		done: false,
	});
	input.value = "";
}
</script>

<template>
	<form class="space-x-2 text-xl" action="submit" @submit.prevent="emitTodo">
		<input
			class="border px-2 rounded dark:border-black dark:bg-stone-900"
			id="newInput"
			placeholder="neuen Eintrag hinzufügen"
			type="text"
			v-model="input"
		/>
		<button
			class="hover:bg-stone-300 dark:hover:bg-stone-600 transition-colors rounded"
			type="submit"
		>
			➕
		</button>
		<label class="absolute opacity-0" for="newInput">Einen neuen Eintrag hinzufügen</label>
	</form>
</template>

<style scoped></style>
