<template>
	<div class="w-full px-10 mt-5">
		<form class="w-full flex" @submit.prevent>
			<input type="text" placeholder="Add task" class="text-sm font-semibold opacity-60 bg-[#322834] px-3 py-2 text-slate-200 outline-none w-[80%] flex-grow rounded-e-none rounded-lg" v-model="taskText">
			<button class="bg-[#e6606b] rounded-lg rounded-s-none px-2 py-2 transition-transform transform active:scale-95" @click="addTask">
				<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="currentColor" class="size-6 text-slate-200">
					<path fill-rule="evenodd" d="M12 3.75a.75.75 0 0 1 .75.75v6.75h6.75a.75.75 0 0 1 0 1.5h-6.75v6.75a.75.75 0 0 1-1.5 0v-6.75H4.5a.75.75 0 0 1 0-1.5h6.75V4.5a.75.75 0 0 1 .75-.75Z" clip-rule="evenodd" />
				</svg>
			</button>
		</form>
	</div>
</template>

<script setup>
import { ref, watch } from 'vue';

	const emit = defineEmits(['addTaskEmit']);
	const	taskText = ref("");
	const	output = ref("");

	const	addTask = () => {
		let	newValue;
		if (taskText.value.length)
		{
			output.value = taskText.value;
			newValue = taskText.value;
			taskText.value = "";
		}
		emit('addTaskEmit', newValue);
	}
</script>
