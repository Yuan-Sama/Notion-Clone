<script>
	import Logo from '$components/Logo.svelte';
	import ModeToggle from '$components/ToggleDarkMode.svelte';

	let { children } = $props();
	/**
	 * @type {any}
	 */
	let scrollY = $state();
	let threshold = 10;
</script>

<svelte:window bind:scrollY />

<div class="h-full dark:bg-[#1f1f1f]">
	<header
		class="fixed top-0 z-50 flex w-full items-center bg-background dark:bg-[#1f1f1f] p-6{scrollY >
		threshold
			? ' border-b shadow-sm'
			: ''}"
	>
		<Logo />
		<div class="flex w-full items-center justify-between gap-x-2 md:ml-auto md:justify-end">
			<ModeToggle />
		</div>
	</header>
	<main class="h-full pt-40">
		{@render children()}
	</main>
</div>
