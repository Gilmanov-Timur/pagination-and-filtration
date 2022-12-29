<template>
	<div class="card">
		<div class="card-body p-3">
			<h5 class="card-title">
				{{ product.name }}
			</h5>
			<table class="table table-sm mb-0">
				<tr>
					<th>Артикул</th>
					<td>{{ product.artnumber }}</td>
				</tr>
				<tr>
					<th>Бренд</th>
					<td>{{ product.brand }}</td>
				</tr>
				<tr>
					<th>Вес</th>
					<td>{{ product.weight }}</td>
				</tr>
				<tr>
					<th>Фасовка</th>
					<td>{{ product.quantity }}</td>
				</tr>
				<tr>
					<th>Цена</th>
					<td>{{ product.price }}</td>
				</tr>
				<tr>
					<th>Наличие</th>
					<td>
						<span class="text-success" v-if="product.stock">
							Есть
						</span>
						<span class="text-danger" v-else>
							Нет
						</span>
					</td>
				</tr>
			</table>
		</div>
	</div>
</template>

<script>
export default {
	props: {
		product: Object,
	}
}
</script>
