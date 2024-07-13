# sveltekit-top-loader

A SvelteKit top loading bar component made using nprogress.

## Installation

Using npm:

```sh
npm install sveltekit-top-loader
```

## Usage

In your root `+layout.svelte` file, import the component and render it at the top.

```svelte
<script lang="ts">
	import { SvelteKitTopLoader } from 'sveltekit-top-loader';
</script>

<div>
	<SvelteKitTopLoader />
	<slot />
</div>
```

## props

### color

Color for the top loader.

- Type: `string`
- Default: `#29d`

### minimum

The initial position for the top loader in percentage, 0.08 is 8%.

- Type: `number`
- Default: `0.08`

### trickleSpeed

The increment delay speed in milliseconds.

- Type: `number`
- Default: `200`

### height

The height for the top loader in pixel.

- Type: `number`
- Default: `3`

### trickle

Auto increamenting behaviour for the top loader.

- Type: `boolean`
- Default: `true`

### showSpinner

To show spinner or not.

- Type: `boolean`
- Default: `true`

### easing

Animation settings using easing (a CSS easing string).

- Type: `string`
- Default: `ease`

### speed

Animation speed in ms for the top loader.

- Type: `number`
- Default: `200`

### shadow

Shadow for the top loader. You can disable it by setting it to `false`.

- Type: `string | false`
- Default: `0 0 10px ${color},0 0 5px ${color}`

### template

Template for the top loader.

- Type: `string`
- Default: `<div class="bar" role="bar"><div class="peg"></div></div><div class="spinner" role="spinner"><div class="spinner-icon"></div></div>`

### zIndex

z-index for the top loader.

- Type: `number`
- Default: `1600`

## Credits

This library is a port of Next.js top loader. A huge thanks to the creators and contributors of [nextjs-toploader](https://github.com/TheSGJ/nextjs-toploader/) and [nprogress](https://github.com/rstacruz/nprogress).
