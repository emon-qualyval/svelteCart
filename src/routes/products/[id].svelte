<script>

	import Product from '../../components/product.svelte'
  	import ProductImage from '../../image/a64b345016e96adfb8849af5521c8e0ecfe8f027-555x555.webp'
	import data from '../../data.json'
	import { page } from '$app/stores';

	let qty = 1
    function incQty(){	
		qty++
        document.querySelector('.num').innerHTML = qty
    }
	const decQty = () => {
		if(qty == 1){
			qty = 1
		}else{
			qty--
		}
        document.querySelector('.num').innerHTML = qty
	}

	const id = $page.params.id

	const filterData = data.filter(data => {
		return data.id == id
	})


	
</script>

<div>
	<div class="product-detail-container">
		<div>
			<div class="image-container">
				<img src={ProductImage} class="product-detail-image" alt="" />
			</div>
			<div class="small-images-container">
				<img src={ProductImage} class="small-image selected-image" alt="" />
			</div>
		</div>

		<div class="product-detail-desc">
			<h1>{filterData[0].name}</h1>
			<div class="reviews">
                <div>
                    <i class="fa-solid fa-star"></i>
                    <i class="fa-solid fa-star"></i>
                    <i class="fa-solid fa-star"></i>
                    <i class="fa-solid fa-star"></i>
                    <i class="fa-solid fa-star-half-stroke"></i>
                </div>
				<p>(20)</p>
			</div>
			<h4>Details:</h4>
			<p>{filterData[0].des}</p>
			<p class="price">${filterData[0].price}</p>
			<div class="quantity">
				<h3>Quantity:</h3>
				<p class="quantity-desc">
                    <span on:click={decQty} class="fa-solid fa-minus minus"></span>
					<span class="num">1</span>
					<span on:click={incQty} class="fa-solid fa-plus plus"></span>
				</p>
			</div>
			<div class="buttons">
				<button type="button" class="add-to-cart">Add to Cart</button>
				<button type="button" class="buy-now">Buy Now</button>
			</div>
		</div>
	</div>

	<div class="maylike-products-wrapper">
		<h2>You may also like</h2>
		<div class="marquee">
			<div class="maylike-products-container track">
				<Product />
				<Product />
				<Product />
				<Product />
				<Product />
				<Product />
				<Product />
			</div>
		</div>
	</div>
</div>
