<template>
	<div class="w-full h-screen px-10 mt-5 flex flex-col gap-3 pb-5">
		<div class="w-full bg-[#322834] flex flex-col gap-1 px-5 py-3 rounded-lg" v-for="task in tasks" :key="task.id">
			<div class="w-full flex justify-between items-center">
				<div class="w-[40px] h-[10px] rounded-full" :style="{backgroundColor:task.color}"></div>
				<form @submit.prevent>
					<button >
						<svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="size-6 text-[#ead4f1] w-[30pxpx] h-[30px]">
 							 <path stroke-linecap="round" stroke-linejoin="round" d="m14.74 9-.346 9m-4.788 0L9.26 9m9.968-3.21c.342.052.682.107 1.022.166m-1.022-.165L18.16 19.673a2.25 2.25 0 0 1-2.244 2.077H8.084a2.25 2.25 0 0 1-2.244-2.077L4.772 5.79m14.456 0a48.108 48.108 0 0 0-3.478-.397m-12 .562c.34-.059.68-.114 1.022-.165m0 0a48.11 48.11 0 0 1 3.478-.397m7.5 0v-.916c0-1.18-.91-2.164-2.09-2.201a51.964 51.964 0 0 0-3.32 0c-1.18.037-2.09 1.022-2.09 2.201v.916m7.5 0a48.667 48.667 0 0 0-7.5 0" />
						</svg>
					</button>
				</form>
			</div>
			<p class="text-sm text-[#ead4f1] mt-1">{{ task.name }}</p>
			<div class="w-full flex items-center">
				<p class="text-xs font-light text-[#ead4f1] italic flex-grow" v-if="task.added === formatedDate">Today</p>
				<p class="text-xs font-light text-[#ead4f1] italic flex-grow" v-else>{{ task.added }}</p>
				<form class="flex items-center" @submit.prevent>
					<input type="checkbox" :id="'done-'+task.id" class="hidden peer" v-model="task.state" @change="checkTask(task)">
					<button class="w-7 h-6 rounded-md border bg-none peer-checked:bg-green-300">
						<label :for="'done-'+task.id" class="w-full h-full flex justify-center items-center cursor-pointer"></label>
					</button>
				</form>
			</div>
		</div>
	</div>
</template>

<script setup>
import { ref } from 'vue';

	const	checked = ref(true);
	const	today = ref(new Date());
	const	todayOptions = {day: 'numeric', month: 'short', year: 'numeric'}
	const	formatedDate = ref(today.value.toLocaleDateString('en-US', todayOptions));
	const	taskColors = [
			"#ff8564",
			"#cdbd00",
			"#786ca4",
			"#ad2428",
			"#cf5250",
			"#a13fa1",
			"#e06c68",
			"#ffa658",
			"#b2b161",
			"#7b6300"
			]
	const	tasks = ref([
		{id: 1, name: "Learn React js", state:false, added: formatedDate.value, color:taskColors[1]},
		{id: 2, name: "Check mail", state:false, added: formatedDate.value, color:taskColors[2]},
		{id: 3, name: "Read books", state:false, added: formatedDate.value, color:taskColors[3]},
		{id: 4, name: "Find inspiration", state:false, added: "Dec 8, 2024", color:taskColors[4]},
	]);

	const	checkTask = (task) => {
		console.log(task.name);
		if (!task.state)
			task.state = true;
		else
			task.state = false;
		console.log(task.state);
	}
</script>
