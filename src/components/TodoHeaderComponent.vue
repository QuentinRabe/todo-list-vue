<template>
	<div class="w-full flex px-10 pt-5 justify-between items-center">
		<div class="flex flex-col gap-3 flex-shrink">
			<p class="text-xl text-[#ead4f1] font-bold">Hey, Quentin</p>
			<div class="flex space-x-5">
				<p class="text-xs text-[#ead4f1] ">{{ formatedDate }}</p>
				<p class="text-xs text-[#ead4f1] ">{{ formatedTime }}</p>
			</div>
		</div>
		<div class="w-[60px] h-[60px] rounded-full bg-center bg-cover" :style="{ backgroundImage: `url(${avatar})` }"></div>
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
