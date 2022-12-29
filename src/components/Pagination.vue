<template>
	<ul class="pagination">
		<li
			class="page-item"
			:class="{active: page === currentPage + 1}"
			v-for="page in totalPages"
		>
			<button type="button" class="page-link" @click="$emit('goTo', page - 1)">
				{{ page }}
			</button>
		</li>
	</ul>
</template>

<script>
export default {
	props: {
		currentPage: Number,
		totalPages: Number,
	}
}
</script>
