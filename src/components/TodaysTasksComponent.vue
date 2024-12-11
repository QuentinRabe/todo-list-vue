<template>
	<div class="w-full px-10 mt-5">
		<div class="w-full bg-[#322834] flex items-center px-5 py-3 rounded-lg justify-between">
			<p class="text-lg font-bold text-[#ead4f1]">Today's Tasks</p>
			<div class="w-[45px] h-[45px] relative rounded-full flex justify-center items-center">
				<svg
			class="absolute w-full h-full"
			viewBox="0 0 45 45"
			xmlns="http://www.w3.org/2000/svg"
				>
					<circle
						cx="22.5"
						cy="22.5"
						r="20"
						stroke-width="4"
						stroke="#1c0e20"
						fill="none"
					>
					</circle>
					<circle
						cx="22.5"
						cy="22.5"
						r="20"
						stroke-width="4"
						stroke="#ead4f1"
						:stroke-dasharray="2 * Math.PI * 20"
						:stroke-dashoffset="dashOffetValue"
						stroke-linecap="round"
						style="transform: rotate(-90deg); transform-origin: center;"
						fill="none"
					>
					</circle>
				</svg>
				<p class="text-[#ead4f1]">{{ props.taskAverage }}%</p>
			</div>
		</div>
	</div>
</template>

<script setup>
	import { computed } from 'vue';
	const	props = defineProps({
		taskAverage: Number,
	});
	const	dashOffetValue = computed(() => {
		return (2 * Math.PI * 20) * (1 - (props.taskAverage / 100));
	});
</script>

<style scoped>
circle {
	transition: all 0.8s ease; /* Animation fluide de stroke-dashoffset */
}
</style>
