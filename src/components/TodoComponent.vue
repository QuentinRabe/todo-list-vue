<template>
	<div class="w-1/3 h-[600px] bg-[#3f3241] shadow-lg shadow-black rounded-md flex flex-col items-center overflow-y-scroll">
		<TodoHeaderComponent/>
		<AddTodoComponent/>
		<TodaysTasksComponent/>
		<TaskComponent/>
	</div>
</template>

<script setup>
	import TodoHeaderComponent from './TodoHeaderComponent.vue';
	import AddTodoComponent from './AddTodoComponent.vue';
	import TodaysTasksComponent from './TodaysTasksComponent.vue';
	import TaskComponent from './TaskComponent.vue';
</script>
