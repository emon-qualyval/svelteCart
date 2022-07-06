<script>
	import { cart } from '../../store.js';
	import Product from '../../components/product.svelte';
	import data from '../../data.json';
	import { page } from '$app/stores';

	let qty = 1;
	function incQty() {
		qty++;
		document.querySelector('.num').innerHTML = qty;
	}
	const decQty = () => {
		if (qty == 1) {
			qty = 1;
		} else {
			qty--;
		}
		document.querySelector('.num').innerHTML = qty;
	};

	const id = $page.params.id;

	const filterData = data.filter((data) => {
		return data.id == id;
	});

	let cartValue;
	cart.subscribe((value) => {
		cartValue = value;
	});

	const addToCart = () => {
		const filter = cartValue.filter((data) => {
			return data.id === parseInt(id);
		});
		if (filter.length == 0) {
			const des = filterData[0].des;
			const name = filterData[0].name;
			const price = filterData[0].price;
			const id = filterData[0].id;
			const img = filterData[0].img;
			const total = qty * parseInt(filterData[0].price);
			const information = { des, name, price, id, img, qty, total };

			cart.update((data) => [...data, information]);
			document.querySelector('.successAlert').style.display = 'block';

			setTimeout(() => {
				document.querySelector('.successAlert').style.display = 'none';
			}, 3000);
		} else {
			document.querySelector('.errorAlert').style.display = 'block';

			setTimeout(() => {
				document.querySelector('.errorAlert').style.display = 'none';
			}, 3000);
		}
	};
</script>

<div class="successAlert">successfully added to cart</div>
<div class="errorAlert">Already in cart</div>

<div>
	<div class="product-detail-container">
		<div>
			<div class="image-container">
				<img src={`/image/${filterData[0].img}`} class="product-detail-image" alt="" />
			</div>
			<div class="small-images-container">
				<img src={`/image/${filterData[0].img}`} class="small-image selected-image" alt="" />
			</div>
		</div>

		<div class="product-detail-desc">
			<h1>{filterData[0].name}</h1>
			<div class="reviews">
				<div>
					<i class="fa-solid fa-star" />
					<i class="fa-solid fa-star" />
					<i class="fa-solid fa-star" />
					<i class="fa-solid fa-star" />
					<i class="fa-solid fa-star-half-stroke" />
				</div>
				<p>(20)</p>
			</div>
			<h4>Details:</h4>
			<p>{filterData[0].des}</p>
			<p class="price">${filterData[0].price}</p>
			<div class="quantity">
				<h3>Quantity:</h3>
				<p class="quantity-desc">
					<span on:click={decQty} class="fa-solid fa-minus minus" />
					<span class="num">1</span>
					<span on:click={incQty} class="fa-solid fa-plus plus" />
				</p>
			</div>
			<div class="buttons">
				<button on:click={addToCart} type="button" class="add-to-cart">Add to Cart</button>
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

<style>
	.successAlert {
		position: fixed;
		top: 20%;
		left: 35%;
		background-color: green;
		width: 30%;
		padding: 15px 20px;
		border-radius: 3px;
		color: white;
		display: none;
	}
	.errorAlert {
		position: fixed;
		top: 20%;
		left: 35%;
		background-color: rgb(187, 22, 22);
		width: 30%;
		padding: 15px 20px;
		border-radius: 3px;
		color: white;
		display: none;
	}
</style>
