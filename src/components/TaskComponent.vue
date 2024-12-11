<template>
	<div class="w-full h-screen px-10 mt-5 flex flex-col gap-3 pb-5">
		<TransitionGroup name="task-transition">
			<div class="w-full bg-[#322834] flex flex-col gap-1 px-5 py-3 rounded-lg card" v-for="task in sortTasks" :key="task.id">
				<div class="w-full flex justify-between items-center">
					<div class="w-[40px] h-[10px] rounded-full" :style="{backgroundColor:task.color}"></div>
						<button @click="removeTask(task)">
							<svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="size-6 text-red-400 w-[30pxpx] h-[30px]">
									<path stroke-linecap="round" stroke-linejoin="round" d="m14.74 9-.346 9m-4.788 0L9.26 9m9.968-3.21c.342.052.682.107 1.022.166m-1.022-.165L18.16 19.673a2.25 2.25 0 0 1-2.244 2.077H8.084a2.25 2.25 0 0 1-2.244-2.077L4.772 5.79m14.456 0a48.108 48.108 0 0 0-3.478-.397m-12 .562c.34-.059.68-.114 1.022-.165m0 0a48.11 48.11 0 0 1 3.478-.397m7.5 0v-.916c0-1.18-.91-2.164-2.09-2.201a51.964 51.964 0 0 0-3.32 0c-1.18.037-2.09 1.022-2.09 2.201v.916m7.5 0a48.667 48.667 0 0 0-7.5 0" />
							</svg>
						</button>
				</div>
				<p class="text-sm text-[#ead4f1] mt-1">{{ task.name }}</p>
				<div class="w-full flex items-center">
					<p class="text-xs font-light text-[#ead4f1] italic flex-grow" v-if="task.added === formatedDate">Today</p>
					<p class="text-xs font-light text-[#ead4f1] italic flex-grow" v-else>{{ task.added }}</p>
					<input type="checkbox" :id="'done-'+task.id" class="hidden peer" :checked="task.state" @click="checkTask(task)">
					<button class="w-7 h-6 rounded-md border bg-none peer-checked:bg-green-300" >
						<label :for="'done-'+task.id" class="w-full h-full flex justify-center items-center cursor-pointer"></label>
					</button>
				</div>
			</div>
		</TransitionGroup>
	</div>
</template>

<script setup>
	import { computed, ref, watch, defineEmits } from 'vue';

	const	emit = defineEmits(['updateCheckedTask', 'removeTask']);
	const	props = defineProps({ tasks: Array, });
	const	today = ref(new Date());
	const	todayOptions = {day: 'numeric', month: 'short', year: 'numeric'}
	const	formatedDate = ref(today.value.toLocaleDateString('en-US', todayOptions));

	const checkTask = (task) => {
		task.state = !task.state;
	};
	const	sortTasks = computed(() => {
		return (props.tasks.sort((a, b) => {
			if (a.state === b.state)
				return (0);
			return (a.state ? 1 : -1);
		}))
	});
	const checkedTask = computed(() => {
		if (props.tasks.length === 0)
			return (0);
		return (Math.round(([...props.tasks].filter((task) => task.state).length / props.tasks.length) * 100));
	});
	const	removeTask = (remove) => {
		const	newArray = [];
		for(let i = 0; i < props.tasks.length; i++){
			if (remove.id != props.tasks[i].id)
				newArray.push(props.tasks[i]);
		}
		emit('removeTask', newArray);
	}
	watch(checkedTask, (newValue) => {
		emit('updateCheckedTask', newValue);
	});
</script>

<style scoped>
.task-transition-enter-active, .task-transition-leave-active {
	transition: all .5s ease-in-out;
}
.task-transition-enter-from {
	opacity: 0;
	transform: translateY(-20px);
}
.task-transition-enter-to {
	opacity: 1;
	transform: translateY(0);
}
.task-transition-leave-from {
  opacity: 1;
  transform: translateY(0);
}
.task-transition-leave-to {
  opacity: 0;
  transform: translateY(-20px);
}
</style>
