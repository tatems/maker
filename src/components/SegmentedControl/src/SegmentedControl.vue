<template>
	<div
		:class="[
			$s.Container,
			$s[`shape_${shapeInner}`],
			$s[`size_${sizeInner}`],
		]"
	>
		<slot />
	</div>
</template>

<script>
import key from './key';

export default {
	provide() {
		return {
			[key]: this.$data,
		};
	},
	model: {
		prop: 'selected',
		event: 'segmented-control:update',
	},
	props: {
		/**
		 * Selected Segment inside Control
		 */
		selected: {
			type: undefined,
			required: true,
		},
		/**
		 * Shape of Control & Segments
		 */
		shape: {
			type: String,
			default: 'rounded',
			validator: (shape) => ['squared', 'rounded', 'pill'].includes(shape),
		},
		/**
		 * Size of Control & Segments
		 */
		size: {
			type: String,
			default: 'medium',
			validator: (size) => ['small', 'medium'].includes(size),
		},
	},
	data() {
		return {
			currentValue: this.selected,
			shapeInner: this.shape,
			sizeInner: this.size,
		};
	},
	watch: {
		currentValue(newValue) {
			this.$emit('segmented-control:update', newValue);
		},
	},
};
</script>

<style module="$s">
.Container {
	display: flex;
	box-sizing: border-box;
	height: 56px;
	padding: 4px;
	font-size: 14px;
	line-height: 24px;
	background-color: #f6f7f9;
	border-radius: 4px;
}

.shape_pill {
	border-radius: 32px;
}

.shape_squared {
	border-radius: 0;
}

.size_small {
	height: 40px;
	font-size: 12px;
	line-height: 16px;
}
</style>
