<template>
	<div v-for="(brand, index) in brands" :key="brand">
		<div class="form-group form-check mb-1">
			<input
				type="checkbox"
				class="form-check-input"
				:id="`brand-${index}`"
				:value="brand"
				v-model="model"
			>
			<label class="form-check-label" :for="`brand-${index}`">
				{{ brand }}
			</label>
		</div>
	</div>
	<button type="button" class="btn btn-primary mt-2" @click="$emit('reset')">
		Сбросить фильтры
	</button>
</template>

<script>
export default {
	props: {
		brands: Array,
		checkedBrands: Array,
	},
	emits: ['update:checkedBrands', 'reset'],
	computed: {
		model: {
			get() {
				return this.checkedBrands;
			},
			set(brands) {
				this.$emit('update:checkedBrands', brands)
			}
		}
	}
}
</script>
