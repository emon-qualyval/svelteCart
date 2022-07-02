<script>
	export let product;
	import img1 from '../image/a64b345016e96adfb8849af5521c8e0ecfe8f027-555x555.webp';
	import data from '../data.json'
</script>

<div class="products-container">
		{#each data as product}
			<a href={`/products/${product.id}`}>
				<div class="product-card">
					<img
						src={img1}
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
