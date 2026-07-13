<script>
	import { WEBUI_BASE_URL } from '$lib/constants';

	import ArrowRightCircle from './icons/ArrowRightCircle.svelte';

	export let show = true;
	export let getStartedHandler = () => {};

	function setLogoImage() {
		const logo = document.getElementById('logo');

		if (logo) {
			const isDarkMode = document.documentElement.classList.contains('dark');

			if (isDarkMode) {
				const darkImage = new Image();
				darkImage.src = `${WEBUI_BASE_URL}/static/favicon-dark.png`;

				darkImage.onload = () => {
					logo.src = `${WEBUI_BASE_URL}/static/favicon-dark.png`;
					logo.style.filter = ''; // Ensure no inversion is applied if splash-dark.png exists
				};

				darkImage.onerror = () => {
					logo.style.filter = 'invert(1)'; // Invert image if splash-dark.png is missing
				};
			}
		}
	}

	$: if (show) {
		setLogoImage();
	}
</script>

{#if show}
	<div class="w-full h-screen max-h-[100dvh] text-white relative bg-black">
		<div class="fixed m-10 z-50">
			<div class="flex space-x-2">
				<div class=" self-center">
					<img
						id="logo"
						crossorigin="anonymous"
						src="{WEBUI_BASE_URL}/static/favicon.png"
						class=" w-24 rounded-full"
						alt="logo"
					/>
				</div>
			</div>
		</div>

		<div class="relative bg-transparent w-full h-screen max-h-[100dvh] flex z-10">
			<div class="flex flex-col justify-center w-full items-center text-center">
				<div class="flex justify-center">
					<div class="flex flex-col justify-center items-center">
						<button
							aria-label="Setup Paisley Chat..."
							class="relative z-20 flex p-1 rounded-full bg-white/5 hover:bg-white/10 transition font-medium text-sm"
							on:click={() => {
								getStartedHandler();
							}}
						>
							<ArrowRightCircle className="size-24" aria-hidden="true" />
						</button>
						<div class="mt-1.5 font-primary text-xl font-medium" aria-hidden="true">
							Setup Paisley Chat...
						</div>
					</div>
				</div>
			</div>
		</div>
	</div>
{/if}
