<script>
	import { cart } from '../store';
	export let status = false;

	//get data from state
	let cartValue;
	cart.subscribe((value) => {
		cartValue = value;
	});

	//close the cart popup
	const closeCart = () => {
		status = false;
	};

	//delete from cart
	const deleteFromCart = (id) => {
		const filterCartData = cartValue.filter((data) => {
			return data.id !== id;
		});

		cart.update(() => [...filterCartData]);
	};

	let total = 0;
	cartValue.map((data) => {
		total = total + data.total;
	});

	let itemCount = 0;
	cartValue.map((data) => {
		itemCount = data.qty + itemCount;
	});

	const payWithStripe = () => {
		fetch('http://localhost:4000/charge', {
			mode: 'no-cors',
			method: 'POST'
		});
	};
</script>

<div class="cart-wrapper">
	<div class="cart-container">
		<button type="button" class="cart-heading">
			<i on:click={closeCart} class="fa-solid fa-angle-left" />
			<span class="heading">Your Cart</span>
			<span class="cart-num-items">{itemCount} items</span>
		</button>

		{#if cartValue.length == 0}
			<div class="empty-cart">
				<i style="font-size: 150px;" class="fa-solid fa-bag-shopping" />
				<h3>Your shopping bag is empty</h3>
				<a href="/">
					<button type="button" class="btn"> Continue Shopping </button>
				</a>
			</div>
		{/if}

		<div class="product-container">
			{#if cartValue.length >= 1}
				{#each cartValue as item}
					<div class="product" key={item.id}>
						<img src={`/image/${item.img}`} alt="" class="cart-product-image" />
						<div class="item-desc">
							<div class="flex top">
								<h5>{item.name}</h5>
								<h4>${item.price}</h4>
							</div>
							<div class="flex bottom">
								<div>
									<p class="quantity-desc">
										<span class="num">{item.qty}</span>
									</p>
								</div>
								<button type="button" class="remove-item"
									><i on:click={() => deleteFromCart(item.id)} class="fa-solid fa-xmark" /></button
								>
							</div>
						</div>
					</div>
				{/each}
			{/if}
		</div>
		{#if cartValue.length >= 1}
			<div class="cart-bottom">
				<div class="total">
					<h3>Subtotal:</h3>
					<h3>${total}</h3>
				</div>
				<div class="btn-container">
					<button on:click={payWithStripe} type="button" class="btn">
						Pay with Stripe
					</button>
				</div>
			</div>
		{/if}
	</div>
</div>
