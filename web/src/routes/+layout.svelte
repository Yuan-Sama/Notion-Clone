<script>
	import '../app.css';
	import '@fortawesome/fontawesome-free/css/fontawesome.min.css';
	import '@fortawesome/fontawesome-free/css/regular.min.css';
	import '@fortawesome/fontawesome-free/css/solid.min.css';

	import LogoImg from '$assets/images/logo.svg';
	import LogoImg_Dark from '$assets/images/logo-dark.svg';
	import { theme } from '$lib/shared.svelte';

	let { children } = $props();
</script>

<svelte:head>
	{#if theme.mode === 'dark'}
		<link rel="shortcut icon" href={LogoImg_Dark} type="image/svg" />
	{:else}
		<link rel="shortcut icon" href={LogoImg} type="image/svg" />
	{/if}
</svelte:head>

{@render children()}
