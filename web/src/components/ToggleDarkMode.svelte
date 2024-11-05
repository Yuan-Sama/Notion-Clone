<script>
	import { theme } from '$lib/shared.svelte';
	import { onMount } from 'svelte';

	let hidden = $state(true);
	let choice = $state();

	function getCurrentMode() {
		return localStorage.theme === 'dark' ||
			(!('theme' in localStorage) && window.matchMedia('(prefers-color-scheme: dark)').matches)
			? 'dark'
			: 'light';
	}

	/**
	 * @param {'dark' | 'light' | 'system'} newChoice
	 */
	function setTheme(newChoice) {
		if (newChoice in ['dark', 'light', 'system']) return;

		choice = newChoice;
		if (choice === 'system') localStorage.removeItem('theme');
		else localStorage.setItem('theme', choice);
		theme.mode = getCurrentMode();
		document.documentElement.classList.toggle('dark', theme.mode === 'dark');
	}

	onMount(() => {
		theme.mode = getCurrentMode();
		choice =
			localStorage.theme ?? (window.matchMedia('(prefers-color-scheme: dark)').matches && 'dark');
	});
</script>

<div class="relative">
	<button
		class="inline-flex h-10 w-10 items-center justify-center gap-2 whitespace-nowrap rounded-lg border border-input bg-background text-sm font-medium ring-offset-background transition-colors hover:bg-accent hover:text-accent-foreground focus-visible:outline-none focus-visible:ring-2 focus-visible:ring-ring focus-visible:ring-offset-2 disabled:pointer-events-none disabled:opacity-50 [&_svg]:pointer-events-none [&_svg]:size-4 [&_svg]:shrink-0"
		aria-label=" "
		onclick={() => (hidden = !hidden)}
	>
		<span class="dark:hidden">
			<svg
				viewBox="0 0 24 24"
				fill="none"
				stroke-width="2"
				stroke-linecap="round"
				stroke-linejoin="round"
				class="h-6 w-6"
			>
				<path d="M15 12a3 3 0 1 1-6 0 3 3 0 0 1 6 0Z" class="fill-sky-400/20 stroke-sky-500"></path>
				<path
					d="M12 4v1M17.66 6.344l-.828.828M20.005 12.004h-1M17.66 17.664l-.828-.828M12 20.01V19M6.34 17.664l.835-.836M3.995 12.004h1.01M6 6l.835.836"
					class="stroke-sky-500"
				></path>
			</svg>
		</span>
		<span class="hidden dark:inline">
			<svg viewBox="0 0 24 24" fill="none" class="h-6 w-6"
				><path
					fill-rule="evenodd"
					clip-rule="evenodd"
					d="M17.715 15.15A6.5 6.5 0 0 1 9 6.035C6.106 6.922 4 9.645 4 12.867c0 3.94 3.153 7.136 7.042 7.136 3.101 0 5.734-2.032 6.673-4.853Z"
					class="fill-sky-400/20"
				></path><path
					d="m17.715 15.15.95.316a1 1 0 0 0-1.445-1.185l.495.869ZM9 6.035l.846.534a1 1 0 0 0-1.14-1.49L9 6.035Zm8.221 8.246a5.47 5.47 0 0 1-2.72.718v2a7.47 7.47 0 0 0 3.71-.98l-.99-1.738Zm-2.72.718A5.5 5.5 0 0 1 9 9.5H7a7.5 7.5 0 0 0 7.5 7.5v-2ZM9 9.5c0-1.079.31-2.082.845-2.93L8.153 5.5A7.47 7.47 0 0 0 7 9.5h2Zm-4 3.368C5 10.089 6.815 7.75 9.292 6.99L8.706 5.08C5.397 6.094 3 9.201 3 12.867h2Zm6.042 6.136C7.718 19.003 5 16.268 5 12.867H3c0 4.48 3.588 8.136 8.042 8.136v-2Zm5.725-4.17c-.81 2.433-3.074 4.17-5.725 4.17v2c3.552 0 6.553-2.327 7.622-5.537l-1.897-.632Z"
					class="fill-sky-500"
				></path><path
					fill-rule="evenodd"
					clip-rule="evenodd"
					d="M17 3a1 1 0 0 1 1 1 2 2 0 0 0 2 2 1 1 0 1 1 0 2 2 2 0 0 0-2 2 1 1 0 1 1-2 0 2 2 0 0 0-2-2 1 1 0 1 1 0-2 2 2 0 0 0 2-2 1 1 0 0 1 1-1Z"
					class="fill-sky-500"
				></path></svg
			>
		</span>
	</button>

	<div
		class="dark:highlight-white/5 data-[state=open]:animate-in data-[state=closed]:animate-out data-[state=closed]:fade-out-0 data-[state=open]:fade-in-0 data-[state=closed]:zoom-out-95 data-[state=open]:zoom-in-95 data-[side=bottom]:slide-in-from-top-2 data-[side=left]:slide-in-from-right-2 data-[side=right]:slide-in-from-left-2 data-[side=top]:slide-in-from-bottom-2 absolute right-0 top-full z-50 mt-4 w-36 min-w-[8rem] overflow-hidden rounded-lg border bg-popover p-1 py-1 text-sm font-semibold text-popover-foreground shadow-md{hidden
			? ' hidden'
			: ''}"
		aria-orientation="vertical"
		role="listbox"
		tabindex="0"
		style="--button-width: 24px;"
	>
		<button
			class="flex w-full items-center px-2 hover:bg-slate-300 hover:dark:bg-slate-600 py-1{choice ===
			'light'
				? ' text-sky-500'
				: ''}"
			onclick={() => setTheme('light')}
		>
			<svg
				viewBox="0 0 24 24"
				fill="none"
				stroke-width="2"
				stroke-linecap="round"
				stroke-linejoin="round"
				class="mr-2 h-6 w-6"
			>
				<path
					d="M15 12a3 3 0 1 1-6 0 3 3 0 0 1 6 0Z"
					class={choice !== 'light'
						? 'stroke-slate-400 dark:stroke-slate-500'
						: 'fill-sky-400/20 stroke-sky-500'}
				>
				</path>
				<path
					d="M12 4v1M17.66 6.344l-.828.828M20.005 12.004h-1M17.66 17.664l-.828-.828M12 20.01V19M6.34 17.664l.835-.836M3.995 12.004h1.01M6 6l.835.836"
					class={choice !== 'light'
						? 'stroke-slate-400 dark:stroke-slate-500'
						: 'fill-sky-400/20 stroke-sky-500'}
				>
				</path>
			</svg>
			Light
		</button>
		<button
			class="flex w-full items-center px-2 hover:bg-slate-300 hover:dark:bg-slate-600 py-1{choice ===
			'dark'
				? ' text-sky-500'
				: ''}"
			onclick={() => setTheme('dark')}
		>
			<svg viewBox="0 0 24 24" fill="none" class="mr-2 h-6 w-6">
				<path
					fill-rule="evenodd"
					clip-rule="evenodd"
					d="M17.715 15.15A6.5 6.5 0 0 1 9 6.035C6.106 6.922 4 9.645 4 12.867c0 3.94 3.153 7.136 7.042 7.136 3.101 0 5.734-2.032 6.673-4.853Z"
					class={choice !== 'dark' ? 'fill-transparent' : 'fill-sky-400/20'}
				>
				</path>
				<path
					d="m17.715 15.15.95.316a1 1 0 0 0-1.445-1.185l.495.869ZM9 6.035l.846.534a1 1 0 0 0-1.14-1.49L9 6.035Zm8.221 8.246a5.47 5.47 0 0 1-2.72.718v2a7.47 7.47 0 0 0 3.71-.98l-.99-1.738Zm-2.72.718A5.5 5.5 0 0 1 9 9.5H7a7.5 7.5 0 0 0 7.5 7.5v-2ZM9 9.5c0-1.079.31-2.082.845-2.93L8.153 5.5A7.47 7.47 0 0 0 7 9.5h2Zm-4 3.368C5 10.089 6.815 7.75 9.292 6.99L8.706 5.08C5.397 6.094 3 9.201 3 12.867h2Zm6.042 6.136C7.718 19.003 5 16.268 5 12.867H3c0 4.48 3.588 8.136 8.042 8.136v-2Zm5.725-4.17c-.81 2.433-3.074 4.17-5.725 4.17v2c3.552 0 6.553-2.327 7.622-5.537l-1.897-.632Z"
					class={choice !== 'dark' ? 'fill-slate-400 dark:fill-slate-500' : ' fill-sky-500'}
				>
				</path>
				<path
					fill-rule="evenodd"
					clip-rule="evenodd"
					d="M17 3a1 1 0 0 1 1 1 2 2 0 0 0 2 2 1 1 0 1 1 0 2 2 2 0 0 0-2 2 1 1 0 1 1-2 0 2 2 0 0 0-2-2 1 1 0 1 1 0-2 2 2 0 0 0 2-2 1 1 0 0 1 1-1Z"
					class={choice !== 'dark' ? 'fill-slate-400 dark:fill-slate-500' : 'fill-sky-500'}
				>
				</path>
			</svg>
			Dark
		</button>
		<button
			class="flex w-full items-center px-2 hover:bg-slate-300 hover:dark:bg-slate-600 py-1{choice ===
			'system'
				? ' text-sky-500'
				: ''}"
			onclick={() => setTheme('system')}
		>
			<svg viewBox="0 0 24 24" fill="none" class="mr-2 h-6 w-6">
				<path
					d="M4 6a2 2 0 0 1 2-2h12a2 2 0 0 1 2 2v7a2 2 0 0 1-2 2H6a2 2 0 0 1-2-2V6Z"
					stroke-width="2"
					stroke-linejoin="round"
					class={choice !== 'system'
						? 'stroke-slate-400 dark:stroke-slate-500'
						: 'fill-sky-400/20 stroke-sky-500'}
				>
				</path>
				<path
					d="M14 15c0 3 2 5 2 5H8s2-2 2-5"
					stroke-width="2"
					stroke-linecap="round"
					stroke-linejoin="round"
					class={choice !== 'system' ? 'stroke-slate-400 dark:stroke-slate-500' : 'stroke-sky-500'}
				>
				</path>
			</svg>
			System
		</button>
	</div>
</div>
