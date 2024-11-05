<script>
	import DocumentImg from '$assets/images/documents.png';
	import DocumentImg_Dark from '$assets/images/documents-dark.png';
	import ReadingImg from '$assets/images/reading.png';
	import ReadingImg_Dark from '$assets/images/reading-dark.png';

	import Button from '$components/Button.svelte';
	import Logo from '$components/Logo.svelte';
</script>

<div class="flex min-h-full flex-col dark:bg-[#1f1f1f]">
	<div
		class="flex flex-1 flex-col items-center justify-center gap-y-8 px-6 pb-10 text-center md:justify-start"
	>
		<div class="max-w-3xl space-y-4">
			<h1 class="text-3xl font-bold sm:text-5xl md:text-6xl">
				Your Ideas, Documents, & Plans. Unified. Welcome to <span class="underline">Jotion</span>
			</h1>
			<h3 class="text-base font-medium sm:text-xl md:text-2xl">
				Jotion is the connected workspace where <br /> better, faster work happens.
			</h3>
			<Button>
				Enter Jotion <i class="fa-solid fa-arrow-right-long ml-2 text-center text-base"></i>
			</Button>
		</div>
		<div class="flex max-w-5xl flex-col items-center justify-center">
			<div class="flex items-center">
				<div class="relative size-[300px] sm:size-[350px] md:size-[400px]">
					<img src={DocumentImg} class="object-contain dark:hidden" alt="Documents" />
					<img src={DocumentImg_Dark} class="hidden object-contain dark:block" alt="Documents" />
				</div>
				<div class="relative hidden size-[400px] md:block">
					<img class="object-contain dark:hidden" src={ReadingImg} alt="Reading" />
					<img class="hidden object-contain dark:block" src={ReadingImg_Dark} alt="Reading" />
				</div>
			</div>
		</div>
	</div>
	<footer class="z-50 flex w-full items-center bg-background p-6 dark:bg-[#1f1f1f]">
		<Logo />
		<div
			class="flex w-full items-center justify-between gap-x-2 text-muted-foreground md:ml-auto md:justify-end"
		>
			<Button variant="ghost" size="sm">Privacy Policy</Button>
			<Button variant="ghost" size="sm">Terms & Conditions</Button>
		</div>
	</footer>
</div>
