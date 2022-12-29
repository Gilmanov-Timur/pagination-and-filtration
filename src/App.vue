<template>
	<div class="container">
		<div class="row">
			<div class="col-md-3 mb-4">
				<div class="h3">Фильтры</div>
				<Filters
					:brands="brands"
					v-model:checkedBrands="checkedBrands"
					@reset="checkedBrands = []"
				/>
			</div>
			<div class="col-md-9">
				<h3>Товары {{ filteredProducts.length }} / {{ allProducts.length }}</h3>
				<div class="row">
					<div class="col-sm-6 mb-4" v-for="product in productsToShow" :key="product.artnumber">
						<ProductCard :product="product" />
					</div>
				</div>
				<Pagination
					:currentPage="currentPage"
					:totalPages="totalPages"
					v-if="totalPages > 1"
					@goTo="currentPage = $event"
				/>
			</div>
		</div>
	</div>
</template>

<script>
import products from '@/data.json'
import ProductCard from '@/components/ProductCard.vue'
import Pagination from '@/components/Pagination.vue'
import Filters from '@/components/Filters.vue'

export default {
	components: {
		ProductCard,
		Pagination,
		Filters,
	},
	data() {
		return {
			allProducts: products,
			brands: [],
			checkedBrands: [],
			currentPage: 0,
			perPage: 4,
		}
	},
	created() {
		this.brands = [...new Set(this.allProducts.map(product => product.brand))].sort()
	},
	computed: {
		filteredProducts() {
			if (this.checkedBrands.length) {
				return this.allProducts.filter(product => this.checkedBrands.includes(product.brand))
			}

			return this.allProducts
		},
		productsToShow() {
			return this.filteredProducts.slice(this.currentPage * this.perPage, (this.currentPage + 1) * this.perPage)
		},
		totalPages() {
			return Math.ceil(this.filteredProducts.length / this.perPage)
		}
	},
	watch: {
		totalPages(total) {
			if (total < this.currentPage + 1) {
				this.currentPage = total - 1
			}
		},
	},
}
</script>
