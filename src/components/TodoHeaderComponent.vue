<template>
	<div class="w-full flex flex-col px-10 pt-5">
		<div class="w-full flex justify-between">
			<p class="text-xl text-[#ead4f1] font-bold">Hey, Quentin</p>
			<div class="w-[40px] h-[40px] rounded-full bg-center bg-cover" :style="{ backgroundImage: `url(${avatar})` }"></div>
		</div>
		<div class="flex space-x-5">
			<p class="text-xs text-[#ead4f1] ">{{ formatedDate }}</p>
			<p class="text-xs text-[#ead4f1] ">{{ formatedTime }}</p>
		</div>
	</div>
</template>

<script setup>
	import { onMounted, ref } from 'vue';
	import avatar from '../assets/avatar.jpg'

	const	today = ref(new Date());
	const	hour = ref(new Date());

	const	todayOptions = {day: 'numeric', month: 'short', year: 'numeric'}
	const	formatedDate = ref(today.value.toLocaleDateString('en-US', todayOptions));
	const	hourOptions = {hour: 'numeric', minute: '2-digit', hour12: true};
	const	formatedTime = ref("")

	let 	interval;
	onMounted(() => {
		interval = setInterval(() => {
			hour.value = new Date();
			formatedTime.value = hour.value.toLocaleTimeString('en-US', hourOptions);
		}, 1000);
	})
</script>
