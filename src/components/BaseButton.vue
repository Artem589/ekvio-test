<script setup lang="ts">
const props = defineProps<{
	type: "button" | "reset" | "submit"
}>()
</script>

<template>
	<button
		class="base-button"
		:type="props.type"
	>
		<slot></slot>
	</button>
</template>

<style scoped>
.base-button {
	color: var(--button-color);
	font-size: 14px;
	padding: 12px;
	border-radius: 12px;
	background: var(--button-default-bg-color);
	border: 1px solid var(--button-default-border-color);
	box-shadow:
			0 4px 8px rgba(0, 0, 0, 0.02),
			0 3px 7px -3px rgba(0, 0, 0, 0.08);
}

.base-button:hover {
	background: var(--button-hover-bg-color);
	border-color: var(--button-hover-border-color);
	cursor: pointer;
}

.base-button:active {
	background: var(--button-active-bg-color);
	border-color: var(--button-active-border-color);
}

.base-button:disabled {
	color: var(--button-disabled-color);
	background: var(--button-default-bg-color);
	border-color: var(--button-default-border-color);
}
</style>
