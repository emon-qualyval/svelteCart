<script>
	import Footer from '../components/footer.svelte';
	import Header from '../components/header.svelte';
	import '../styles/global.css';
</script>

<header>
	<Header />
</header>
<main>
	<slot />
</main>
<footer>
	<Footer />
</footer>
