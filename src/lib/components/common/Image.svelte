<script lang="ts">
	import { TUTOR_BASE_URL } from '$lib/constants';
	import ImagePreview from './ImagePreview.svelte';

	export let src = '';
	export let alt = '';

	export let className = ' w-full outline-hidden focus:outline-hidden';
	export let imageClassName = 'rounded-lg';

	let _src = '';
	$: _src = src.startsWith('/') ? `${TUTOR_BASE_URL}${src}` : src;

	let showImagePreview = false;
</script>

<button
	class={className}
	on:click={() => {
		showImagePreview = true;
	}}
	type="button"
>
	<img src={_src} {alt} class={imageClassName} draggable="false" data-cy="image" />
</button>

<ImagePreview bind:show={showImagePreview} src={_src} {alt} />
