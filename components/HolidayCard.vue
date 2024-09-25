<script setup>
// Определяем пропсы
const props = defineProps({
	name: {
		type: String,
		required: true,
	},
	date: {
		type: String,
		required: true,
	},
	englishName: {
		type: String,
		required: true,
	},
});
</script>

<template>
	<div class="holiday-card">
		<h2>{{ name }}</h2>
		<p><strong>Date:</strong> {{ date }}</p>
		<p><strong>English Name:</strong> {{ englishName }}</p>
	</div>
</template>

<style scoped>
.holiday-card {
	border: 1px solid #212121;
	border-radius: 8px;
	padding: 16px;
	margin: 10px;
	background-color: #f9f9f9;
	width: 100%;
	max-width: 400px;
}

.holiday-card h2 {
	font-size: 1.5rem;
	color: #333;
}

.holiday-card p {
	font-size: 1rem;
	color: #555;
	margin: 5px 0;
}
</style>
