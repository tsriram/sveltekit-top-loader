<script lang="ts">
	import { afterNavigate, beforeNavigate } from '$app/navigation';
	import nProgress from 'nprogress';
	import { onMount } from 'svelte';

	/**
	 * Color for the TopLoader.
	 * @default "#29d"
	 */
	export let color: string = '#29d';
	/**
	 * The initial position for the TopLoader in percentage, 0.08 is 8%.
	 * @default 0.08
	 */
	export let minimum: number = 0.08;
	/**
	 * The increament delay speed in milliseconds.
	 * @default 200
	 */
	export let trickleSpeed: number = 200;
	/**
	 * The height for the TopLoader in pixels (px).
	 * @default 3
	 */
	export let height: number = 3;
	/**
	 * Auto increamenting behaviour for the TopLoader.
	 * @default true
	 */
	export let trickle: boolean = true;
	/**
	 * To show spinner or not.
	 * @default true
	 */
	export let showSpinner: boolean = true;
	/**
	 * Animation settings using easing (a CSS easing string).
	 * @default "ease"
	 */
	export let easing: string = 'ease';
	/**
	 * Animation speed in ms for the TopLoader.
	 * @default 200
	 */
	export let speed: number = 200;
	/**
	 * Defines a shadow for the TopLoader.
	 * @default "0 0 10px ${color},0 0 5px ${color}"
	 *
	 * @ you can disable it by setting it to `false`
	 */
	export let shadow: string | false = `0 0 10px ${color},0 0 5px ${color}`;
	/**
	 * Defines a template for the TopLoader.
	 * @default "<div class="bar" role="bar"><div class="peg"></div></div>
	 * <div class="spinner" role="spinner"><div class="spinner-icon"></div></div>"
	 */
	export let template: string = `<div class="bar" role="bar"><div class="peg"></div></div><div class="spinner" role="spinner"><div class="spinner-icon"></div></div>`;
	/**
	 * Defines zIndex for the TopLoader.
	 * @default 1600
	 *
	 */
	export let zIndex: number = 1600;

	const boxShadow =
		!shadow && shadow !== undefined
			? ''
			: shadow
				? `box-shadow:${shadow}`
				: `box-shadow:0 0 10px ${color},0 0 5px ${color}`;

	let styleElement: HTMLStyleElement;

	$: styles = `#nprogress{pointer-events:none}#nprogress .bar{background:${color};position:fixed;z-index:${zIndex};top:0;left:0;width:100%;height:${height}px}#nprogress .peg{display:block;position:absolute;right:0;width:100px;height:100%;${boxShadow};opacity:1;-webkit-transform:rotate(3deg) translate(0px,-4px);-ms-transform:rotate(3deg) translate(0px,-4px);transform:rotate(3deg) translate(0px,-4px)}#nprogress .spinner{display:block;position:fixed;z-index:${zIndex};top:15px;right:15px}#nprogress .spinner-icon{width:18px;height:18px;box-sizing:border-box;border:2px solid transparent;border-top-color:${color};border-left-color:${color};border-radius:50%;-webkit-animation:nprogress-spinner 400ms linear infinite;animation:nprogress-spinner 400ms linear infinite}.nprogress-custom-parent{overflow:hidden;position:relative}.nprogress-custom-parent #nprogress .bar,.nprogress-custom-parent #nprogress .spinner{position:absolute}@-webkit-keyframes nprogress-spinner{0%{-webkit-transform:rotate(0deg)}100%{-webkit-transform:rotate(360deg)}}@keyframes nprogress-spinner{0%{transform:rotate(0deg)}100%{transform:rotate(360deg)}}`;

	onMount(() => {
		styleElement = document.createElement('style');
		document.head.appendChild(styleElement);

		nProgress.configure({
			showSpinner,
			trickle,
			trickleSpeed,
			minimum,
			easing,
			speed,
			template
		});

		return () => {
			document.head.removeChild(styleElement);
		};
	});

	$: if (styleElement) {
		styleElement.textContent = styles;
	}

	beforeNavigate(() => {
		nProgress.start();
	});

	afterNavigate(() => {
		nProgress.done();
	});
</script>

<svelte:head>
	<style>
		{@html styles}
	</style>
</svelte:head>
