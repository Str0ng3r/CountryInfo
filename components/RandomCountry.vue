<script lang="ts" setup>
interface Holiday {
	date: string;
	localName: string;
	name: string;
}
interface Country {
	name: string;
	code: string;
	holidays: Array<[Holiday]>;
}
const props = defineProps<Country>();
</script>

<template>
	<NuxtLink class="button_country" :to="`/country/${code}`">
		{{ name }} - {{ code }}
		<span>{{ holidays[0].localName }} - {{ holidays[0].name }} </span>
		<span> ({{ holidays[0].date }})</span>
	</NuxtLink>
</template>

<style scoped lang="scss">
.button_country {
	color: #212121;
	font-size: 1.4rem;
	cursor: pointer;
	padding: 1rem;
	border: 2px solid #212121;
	border-radius: 8px;
	margin: 6px;
	display: flex;
	width: 100%;
	flex-direction: column;
}
</style>
