<script lang="ts" setup>
import { useRoute } from "vue-router";
import axios from "axios";
const route = useRoute();
const countryCode = route.params.countryCode;
const countryData = ref(null);
const countryInfo = ref(null);
const currentYear = ref(2024);
const yearsButtons = [
	2020, 2021, 2022, 2023, 2024, 2025, 2026, 2027, 2028, 2029, 2030,
];

const fetchCountryData = async () => {
	try {
		const response = await axios.get(
			`https://date.nager.at/api/v3/PublicHolidays/${currentYear.value}/${countryCode}`
		);
		countryData.value = response.data;
		console.log(response.data);
	} catch (error) {
		console.error("Error fetching country data:", error);
	}
};
const newYear = (year: number) => {
	currentYear.value = year;
};
const fetchCountryInfo = async () => {
	try {
		const response = await axios.get(
			`https://date.nager.at/api/v3/CountryInfo/${countryCode}`
		);
		countryInfo.value = response.data;
		console.log(response.data);
	} catch {
		console.log("Error");
	}
};
onMounted(() => {
	fetchCountryData();
	fetchCountryInfo();
});
watch(currentYear, () => {
	fetchCountryData();
});
</script>

<template>
	<div class="wrapper_country_info">
		<h1 class="title_country" v-if="countryInfo !== null">
			{{ countryInfo.officialName }} - {{ countryInfo.region }}
		</h1>
		<h1 class="title_country__desc" v-if="countryInfo !== null">
			{{ countryInfo.countryCode }}
		</h1>
		<h1 class="title_country__year" v-if="countryInfo !== null">
			{{ currentYear }}
		</h1>
		<div class="list_holidays">
			<HolidayCard
				v-for="(item, key) in countryData"
				:key="key"
				:name="item.localName"
				:english-name="item.name"
				:date="item.date"
			></HolidayCard>
		</div>
		<div class="list_years_buttons">
			<button
				class="list_years_buttons__button type1"
				v-for="(item, key) in yearsButtons"
				:key="key"
				@click="newYear(item)"
			>
				<span class="btn-txt">{{ item }}</span>
			</button>
		</div>
	</div>
</template>

<style scoped lang="scss">
.wrapper_country_info {
	display: flex;
	width: 100%;
	align-items: center;
	justify-content: center;
	padding: 2rem;
	flex-direction: column;
}
.list_years_buttons__button {
	height: 50px;
	width: 150px;
	position: relative;
	background-color: transparent;
	cursor: pointer;
	border: 2px solid #252525;
	overflow: hidden;
	color: #333;
	transition: all 0.5s ease-in-out;
}

.btn-txt {
	z-index: 1;
	font-weight: 800;
	letter-spacing: 1px;
}

.type1::after {
	content: "";
	position: absolute;
	left: 0;
	top: 0;
	transition: all 0.5s ease-in-out;
	background-color: #333;
	border-radius: 30px;
	visibility: hidden;
	height: 10px;
	width: 10px;
	z-index: -1;
}

.list_years_buttons__button:hover {
	box-shadow: 1px 1px 200px #252525;
	color: #fff;
	border: none;
}

.type1:hover::after {
	visibility: visible;
	transform: scale(100) translateX(2px);
}
.list_years_buttons {
	display: flex;
	width: 100%;
	margin-top: 2rem;
	justify-content: space-between;
	align-items: center;
	gap: 1rem;
}
.list_holidays::-webkit-scrollbar {
	width: 0.7rem;
}
.list_holidays::-webkit-scrollbar-track {
	width: 0.7rem;
}
.list_holidays::-webkit-scrollbar-thumb {
	width: 0.7rem;
	border-radius: 0.35rem;
	border: 1px solid rgba(255, 255, 255, 0.15);
	background: var(--Stroke-medium-grey-stroke, #d5d6de);
}
.list_holidays {
	margin: 0 auto;
	display: flex;
	align-items: center;
	justify-content: center;
	width: 70%;
	max-height: 60rem;
	gap: 2rem;
	overflow-y: auto;
	overflow-x: hidden;
	flex-wrap: wrap;
	padding-bottom: 4rem;
}
.title_country {
	font-family: "Source Code Pro";
	font-size: 2rem;
	font-weight: 500;
	color: black;
	margin-bottom: 0.2rem;
}
.title_country__desc {
	font-family: "Source Code Pro";
	font-size: 2rem;
	font-weight: 400;
	color: black;
	margin-bottom: 0.2rem;
}
.title_country__year {
	font-family: "Source Code Pro";
	font-size: 2rem;
	font-weight: 500;
	color: black;
	margin-bottom: 2rem;
}
</style>
