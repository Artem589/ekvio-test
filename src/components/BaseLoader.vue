<template>
	<div class="base-loader"></div>
</template>

<style scoped>
.base-loader {
	width: 16px;
	height: 16px;
	border-radius: 50%;
	border: 2px solid #00a8a5;
	border-bottom-color: transparent;
	box-sizing: border-box;
	animation: rotation 1s linear infinite;
			
}

@keyframes rotation {
	0% {
		transform: rotate(0deg);
	}
	100% {
		transform: rotate(360deg);
	}
}
</style>
