<script setup lang="ts">
import BaseFileInput from "./components/BaseFileInput.vue";
</script>

<template>
	<header>
		<div class="header__logo">
			<img src="./components/icons/Shape.png" alt="">
			<p>Ekvio DS</p>
		</div>
	</header>
	<main class="main">
		<BaseFileInput
			:label="'Label'"
			:hint="'Hint text'"
			:input-id="'my-input1'"
		/>
	</main>
</template>

<style scoped>
 .header__logo {
	 width: 125px;
	 height: 44px;
	 background: #F3F4F6;
	 border-radius: 100px;
	 margin-top: 48px;
	 
	 display: flex;
	 justify-content: center;
	 gap: 10px;
	 align-items: center;
	 margin-left: 56px;
}

.main {
	width: 100vw;
	height: 80vh;
	display: flex;
	flex-direction: column;
	align-items: center;
	justify-content: center;
}
</style>

