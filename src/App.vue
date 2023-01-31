<script setup lang="ts">
import { ref } from "vue";
import TodoDraggable from "./components/TodoDraggable.vue";
import TodoTransition from "./components/TodoTransition.vue";

const showDraggable = ref(true);
</script>

<template>
	<button
		:class="[showDraggable ? 'bg-cyan-200 dark:bg-cyan-700' : 'bg-emerald-200 dark:bg-emerald-700']"
		class="absolute top-2 left-2 right-0 z-50 dark:text-white w-fit transition-colors p-2 rounded"
		@click="showDraggable = !showDraggable"
	>
		Switch Mode to {{ showDraggable ? "Transition" : "Draggable" }}
	</button>

	<transition name="fade">
		<TodoDraggable v-show="showDraggable" class="absolute top-0" />
	</transition>
	<transition name="fade">
		<TodoTransition v-show="!showDraggable" class="absolute top-0" />
	</transition>
</template>

<style>
.fade-enter-active,
.fade-leave-active {
	transition: all 0.5s ease-in-out;
}
.fade-enter-from,
.fade-leave-to {
	opacity: 0;
}
</style>
