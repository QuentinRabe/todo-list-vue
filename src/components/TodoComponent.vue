<template>
	<div class=" w-[90%] lg:w-1/3 sm:w-1/2  h-[85%] bg-[#3f3241] shadow-lg shadow-black rounded-md flex flex-col items-center overflow-y-scroll
		scrollbar-thin scrollbar-track-[#322834] scrollbar-thumb-[#e6606b]">
		<TodoHeaderComponent @updateTime="handleTimeUpdate"/>
		<AddTodoComponent @addTaskEmit="handleAddTaskUpdate"/>
		<TodaysTasksComponent :taskAverage="checkedTask"/>
		<TaskComponent @updateCheckedTask="handleCheckTaskUpdate" :tasks="tasks" @removeTask="handleRemoveTask"/>
	</div>
</template>

<script setup>
	import TodoHeaderComponent from './TodoHeaderComponent.vue';
	import AddTodoComponent from './AddTodoComponent.vue';
	import TodaysTasksComponent from './TodaysTasksComponent.vue';
	import TaskComponent from './TaskComponent.vue';
	import { ref } from 'vue';

	const	checkedTask = ref(0);
	const tasks = ref([]);
	const taskColors = [
	"#ff8564", // orange clair
	"#ff6347", // rouge tomate
	"#ff4500", // orange foncé
	"#cdbd00", // jaune moutarde
	"#ffa500", // orange
	"#f5c71a", // jaune doré
	"#c2d9d3", // bleu-vert clair
	"#64b3f4", // bleu clair
	"#4682b4", // bleu acier
	"#6a5acd", // bleu violet
	"#3b0a45", // violet foncé
	"#8a2be2", // bleu violet
	"#ad2428", // rouge bordeaux
	"#f72585", // rose vif
	"#cf5250", // rose saumon
	"#a13fa1", // violet lavande
	"#ff1493", // rose profond
	"#e06c68", // rouge-orangée
	"#ffa658", // pêche
	"#b2b161"  // vert mousse
		];
	const	today = ref(new Date());
	const	todayOptions = {day: 'numeric', month: 'short', year: 'numeric'};
	const	formatedDate = ref(today.value.toLocaleDateString('en-US', todayOptions));
	let		actualTime;

	const	handleTimeUpdate = (value) => {
		actualTime = value;
	}
	const	handleCheckTaskUpdate = (value) => {
		checkedTask.value = value;
	}
	const shuffleArray = (array) => {
		for (let i = array.length - 1; i > 0; i--) {
			const j = Math.floor(Math.random() * (i + 1));
			[array[i], array[j]] = [array[j], array[i]];
		}
	};
	const	handleAddTaskUpdate = (value) => {
		if (!value)
			return ;
		shuffleArray(taskColors);
		const	newTask = {
			id: Date.now(),
			name: value,
			state: false,
			added: formatedDate.value,
			color: taskColors[0],
			addedTime: actualTime,
		};
		tasks.value.push({...newTask});
		console.log(`Added`);
		console.log('newTask :>> ', newTask);
	}
	const	handleRemoveTask = (newArray) => {
		tasks.value = newArray;
	}
</script>
