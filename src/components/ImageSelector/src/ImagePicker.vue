<template>
	<div
		:class="$s.ImagePickerInputContainer"
		@click="$refs.input.click()"
	>
		<input
			ref="input"
			:class="$s.ImagePickerInput"
			type="file"
			multiple="true"
			accept="image/jpeg, image/png"
			@change="selectImages"
		>
		<plus-icon
			inline
			:class="$s.ImagePickerInputIcon"
		/>
	</div>
</template>

<script>
import PlusIcon from '@square/maker-icons/Plus';

export default {
	name: 'MImagePicker',
	components: {
		PlusIcon,
	},

	methods: {
		selectImages(fileEvent) {
			this.$emit('selectImages', [...fileEvent.target.files]);
		},
	},
};
</script>

<style module="$s">
.ImagePickerInputContainer {
	display: flex;
	align-items: center;
	justify-content: center;
	box-sizing: border-box;
	width: 96px;
	height: 96px;
	border: 1px solid rgba(0, 0, 0, 0.9);
	border-radius: 8px;
	cursor: pointer;
	transition: background-color 150ms linear;
}

.ImagePickerInputIcon {
	width: 15px;
	height: 15px;
}

.ImagePickerInput {
	display: none;
}
</style>
