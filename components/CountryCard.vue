<script lang="ts" setup>
interface Country {
	name: string;
	code: string;
}
const props = defineProps<Country>();
</script>

<template>
	<NuxtLink class="button_country" :to="`/country/${code}`"
		>{{ name }} - {{ code }}</NuxtLink
	>
</template>

<style scoped lang="scss">
.button_country {
	background-color: darkgrey;
	color: #ffffff;
	font-size: 1.4rem;
	cursor: pointer;
	padding: 1.2rem;
	border: 2px solid #212121;
	border-radius: 8px;
	margin: 6px;
}
</style>
