<script setup lang="ts">
import { ref, computed } from 'vue'
import BaseButton from './BaseButton.vue'
import BaseLoader from './BaseLoader.vue'
import type { File } from '@/types.ts'

const props = defineProps<{
	label: string
	hint: string
	accept?: string
	disabled?: boolean
	inputId: string
}>()

const inputElement = ref()
const fileText = ref('Файл не выбран')
const fileLoaded = ref(false)
const error = ref(false)
const errorText = ref('')
const loadingIndicator = ref(false)

function inputClick() {
	fileLoaded.value ? clearInput() : inputElement.value.click()
}

function inputChange() {
	const file = inputElement.value.files[0]
	if (file) {
		fileLoaded.value = true
		error.value = !checkInputFileSize(file)
		fileText.value = file.name
		loadFile(file)
	}
}

function clearInput() {
	inputElement.value.value = null
	fileLoaded.value = false
	error.value = false
	errorText.value = ''
	fileText.value = 'Файл не выбран'
}

const btnText = computed(() =>
	loadingIndicator.value ? 'Отменить' : fileLoaded.value ? 'Удалить' : 'Выбрать файл'
)

function checkInputFileSize(file: File) {
	return file.size / 1000000 < 2
}

function loadFile(file: Blob) {
	const reader = new FileReader()
	
	reader.onprogress = () => (loadingIndicator.value = true)
	reader.onload = () => (loadingIndicator.value = false)
	reader.onerror = function (event) {
		error.value = true
		errorText.value = 'Ошибка загрузки файла:' + event.target?.error
	}
	
	reader.readAsDataURL(file)
}
</script>

<template>
	<div class="file-input">
		<label
			class="file-input__label"
			:for="props.inputId"
		>{{ props.label }}</label
		>
		<div class="file-input__main">
			<input
				:id="props.inputId"
				class="file-input__input"
				type="file"
				ref="inputElement"
				@change="inputChange"
				:accept="props.accept"
				:disabled="props.disabled"
				aria-describedby="fileHint"
			/>
			<BaseButton
				class="file-input__btn"
				:disabled="props.disabled"
				:type="'button'"
				@click="inputClick"
			>{{ btnText }}</BaseButton
			>
			<BaseLoader
				v-if="loadingIndicator"
				class="file-input__loader"
			/>
			<span
				class="file-input__file-text"
				:class="{ 'file-input__file-text_accent': fileLoaded }"
			>{{ fileText }}</span
			>
		</div>
		<span
			class="file-input__hint-text"
			:class="{ 'file-input__hint-text_error': error }"
		>{{ error ? errorText || 'Размер файла не должен превышать 2 МБ' : props.hint }}</span
		>
	</div>
</template>

<style scoped>
.file-input {
	display: flex;
	flex-direction: column;
}

.file-input__label {
	color: #111827;
	font-size: 13px;
	font-weight: 500;
	margin-bottom: 12px;
}

.file-input__main {
	display: flex;
	align-items: center;
	margin-bottom: 8px;
	position: relative;
}

.file-input__btn {
	margin-right: 16px;
}

.file-input__loader {
	margin-right: 8px;
}

.file-input__file-text {
	color: #9ca3b0;
	font-size: 14px;
}

.file-input__file-text_accent {
	color: #6b7280;
}

.file-input__input {
	opacity: 0;
	width: 0;
	height: 0;
	position: absolute;
	z-index: -1;
}

.file-input__input:focus + .file-input__btn {
	box-shadow: 0px 0px 0px 2px #6b72801a;
}

.file-input__hint-text {
	color: #6b7280;
	font-size: 13px;
}

.file-input__hint-text_error {
	color: #ef4343;
}
</style>
