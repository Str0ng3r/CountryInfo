<script lang="ts" setup></script>

<template>
	<div class="main_wrap">
		<header><NuxtLink to="/" class="main_link">Home</NuxtLink></header>
		<slot></slot>
	</div>
</template>

<style scoped lang="scss">
.main_wrap {
	width: 100%;
	display: flex;
	flex-direction: column;
	align-items: center;
	justify-content: center;
}
.main_link {
	font-family: "Source Code Pro";
	font-size: 2.8rem;
	font-weight: 600;
	color: #212121;
}
header {
	width: 100%;
	padding: 1rem;
	display: flex;
	align-items: center;
	justify-content: center;
	-webkit-box-shadow: 0px 14px 11px -5px rgba(66, 68, 90, 1);
	-moz-box-shadow: 0px 14px 11px -5px rgba(66, 68, 90, 1);
	box-shadow: 0px 14px 11px -5px rgba(66, 68, 90, 1);
}
</style>
