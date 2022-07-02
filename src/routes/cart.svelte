<script>
    export let status = false;


    const closeCart = () => {
        status = false
    }
</script>

<div class="cart-wrapper">
	<div class="cart-container">
		<button type="button" class="cart-heading">
            <i on:click={closeCart} class="fa-solid fa-angle-left"></i>
			<span class="heading">Your Cart</span>
			<span class="cart-num-items">0 items</span>
		</button>

		<div class="empty-cart">
            <i style="font-size: 150px;" class="fa-solid fa-bag-shopping"></i>
			<h3>Your shopping bag is empty</h3>
			<a href="/">
				<button type="button" class="btn"> Continue Shopping </button>
			</a>
		</div>
	</div>
</div>
