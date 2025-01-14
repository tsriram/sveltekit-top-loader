<script lang="ts">
	import { SvelteKitTopLoader } from '$lib/index.js';
	interface Props {
		children?: import('svelte').Snippet;
	}

	let { children }: Props = $props();
</script>

<SvelteKitTopLoader />
{@render children?.()}
