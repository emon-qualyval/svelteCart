<script>
	import Cart from "../routes/cart.svelte";

	let cartStatus = false;
	const showCart = () => {
		cartStatus = true
	}
</script>

<div class="navbar-container">
	<p class="logo">
		<a href="/">JSM Headphones</a>
	</p>
	<button type="button" class="cart-icon">
		<i on:click={showCart} class="fa-solid fa-cart-shopping" />
	</button>
</div>
{#if cartStatus }<Cart bind:status={cartStatus} />{/if}