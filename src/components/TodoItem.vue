<script setup lang="ts">
import { ref } from "vue";
import { TypeTodoItem } from "../interfaces";

const props = defineProps<{
	todo: TypeTodoItem;
}>();

const emit = defineEmits<{
	(e: "delete"): void;
	(e: "toggledone"): void;
}>();

const done = ref(props.todo.done);

console.log({ ...props.todo });
</script>

<template>
	<li
		:class="{ 'opacity-50': done }"
		class="flex gap-4 rounded w-full transition-all bg-stone-100 dark:bg-stone-900 ring-1 ring-stone-800 px-2"
	>
		<input
			class="cursor-pointer"
			type="checkbox"
			name="Mark as Done"
			v-model="done"
			@click="emit('toggledone')"
		/>
		<span :class="{ 'line-through': done }" class="flex-grow">{{ props.todo.content }}</span>
		<button @click="emit('delete')">❌</button>
	</li>
</template>

<style scoped></style>
