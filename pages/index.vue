<script setup>
import axios from "axios";
const holidays = ref([]);
const longWeekends = ref([]);
const searchValue = ref("");

const getRandomCountries = (countries, count) => {
	const shuffled = [...countries].sort(() => 0.5 - Math.random());
	return shuffled.slice(0, count);
};

const filteredCountries = computed(() => {
	if (!searchValue.value) {
		return holidays.value;
	}
	return holidays.value.filter((country) =>
		country.name.toLowerCase().includes(searchValue.value.toLowerCase())
	);
});

const fetchLongWeekendsForCountries = async (randomCountries) => {
	try {
		const promises = randomCountries.map((code) =>
			axios.get(
				`https://date.nager.at/api/v3/NextPublicHolidays/${code.countryCode}`
			)
		);
		const responses = await Promise.all(promises);
		console.log(responses);
		longWeekends.value = responses.map((response, index) => ({
			countryCode: randomCountries[index].countryCode,
			name: randomCountries[index].name,
			holidays: response.data,
		}));
	} catch (error) {
		console.error("Error fetching long weekends:", error);
	}
};

onMounted(async () => {
	try {
		const response = await axios.get(
			"https://date.nager.at/api/v3/AvailableCountries"
		);
		holidays.value = response.data;

		const randomCountries = getRandomCountries(holidays.value, 3);
		await fetchLongWeekendsForCountries(randomCountries);
	} catch (error) {
		console.error("Error fetching holidays or long weekends:", error);
	}
});
</script>

<template>
	<div class="wrapper">
		<div class="wrap_list">
			<input type="text" class="search_countries" v-model="searchValue" />
			<h1 class="title_list">
				List Countries ({{ filteredCountries.length }})
			</h1>
			<div class="list_for_countries">
				<CountryCard
					v-if="holidays.length !== 0"
					v-for="(item, key) in filteredCountries"
					:name="item.name"
					:code="item.countryCode"
					:key="key"
				></CountryCard>
			</div>
		</div>
		<div class="random_widget">
			<h1 class="title_widget">Random Country</h1>
			<RandomCountry
				v-for="(item, key) in longWeekends"
				:name="item.name"
				:code="item.countryCode"
				:holidays="item.holidays"
				:key="key"
			></RandomCountry>
		</div>
	</div>
</template>

<style scoped lang="scss">
.wrapper {
	width: 100%;
	display: flex;
	align-items: flex-start;
	justify-content: flex-start;
	padding: 4rem;
	gap: 10rem;
}
.search_countries {
	border: 2px solid #212121;
	border-radius: 10px;
	padding: 1rem;
	margin-left: 3rem;
	font-family: "Source Code Pro";
	font-weight: 500;
	font-size: 1.6rem;
	margin-bottom: 1rem;
}
.random_widget {
	display: flex;
	flex-direction: column;
	align-items: center;
	justify-content: center;
	border: 2px solid #212121;
	border-radius: 10px;
	padding: 1rem;
	min-width: 55rem;
}
.title_widget {
	font-family: "Source Code Pro";
	font-size: 2rem;
	font-weight: 500;
	margin-left: 2rem;
}
.wrap_list {
	display: flex;
	flex-direction: column;
	align-items: flex-start;
	justify-content: flex-start;
}
.list_for_countries {
	width: 100%;
	display: flex;
	flex-direction: column;
	flex-wrap: nowrap;
	align-items: center;
	justify-content: flex-start;
	max-height: 40rem;
	overflow-y: auto;
	overflow-x: hidden;
	max-width: 30rem;
}
.list_for_countries::-webkit-scrollbar {
	width: 0.7rem;
}
.list_for_countries::-webkit-scrollbar-track {
	width: 0.7rem;
}
.list_for_countries::-webkit-scrollbar-thumb {
	width: 0.7rem;
	border-radius: 0.35rem;
	border: 1px solid rgba(255, 255, 255, 0.15);
	background: var(--Stroke-medium-grey-stroke, #d5d6de);
}
.title_list {
	font-family: "Source Code Pro";
	font-size: 2rem;
	font-weight: 500;
	margin-left: 2rem;
}
</style>
