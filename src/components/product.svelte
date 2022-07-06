<script>
	export let product;
	import data from '../data.json'
</script>

<div class="products-container">
		{#each data as product}
			<a href={`/products/${product.id}`}>
				<div class="product-card">
					<img
						src={`/image/${product.img}`}
						width={250}
						height={250}
						alt="Product Image"
						class="product-image"
					/>
					<p class="product-name">{product.name}</p>
					<p class="product-price">${product.price}</p>
				</div>
			</a>
		{/each}
</div>
