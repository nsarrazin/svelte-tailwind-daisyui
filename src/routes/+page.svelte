<script lang="ts">
	import { onMount } from 'svelte';
	import { themes } from '$lib/themes';

	let currentTheme = '';

	onMount(() => {
		if (typeof window !== 'undefined') {
			const theme = window.localStorage.getItem('theme');
			if (theme && themes.includes(theme)) {
				document.documentElement.setAttribute('data-theme', theme);
				currentTheme = theme;
			}
		}
	});

	function setTheme(event: Event) {
		const select = event.target as HTMLSelectElement;
		const theme = select.value;
		if (themes.includes(theme)) {
			const one_year = 60 * 60 * 24 * 365;
			window.localStorage.setItem('theme', theme);
			document.cookie = `theme=${theme}; max-age=${one_year}; path=/; SameSite=Strict;`;
			document.documentElement.setAttribute('data-theme', theme);
			currentTheme = theme;
		}
	}
</script>

<div class="mx-auto w-full pt-5">
	<article class="prose mx-auto max-w-4xl lg:prose-xl">
		<h3>sveltekit+tailwind+daisyui</h3>
		<p>
			Half of my web projects always start the same way so I figured I could save myself some time
			and create a template.
		</p>
		<p>
			I'm using <a href="https://kit.svelte.dev/">SvelteKit</a>,
			<a href="https://tailwindcss.com/">tailwindcss</a>
			and <a href="https://daisyui.com/">daisyui</a>.
		</p>
	</article>
</div>

<div class="mx-auto w-full max-w-xl px-10">
	<select
		data-choose-theme
		class="select select-bordered select-primary mx-auto my-5 w-full max-w-3xl text-xl capitalize"
		on:change={setTheme}
	>
		<option disabled selected>Choose a theme</option>
		{#each themes as theme}
			<option value={theme} class="capitalize">{theme}</option>
		{/each}
	</select>

	<div class="card mx-auto w-96 bg-neutral text-neutral-content">
		<div class="card-body items-center text-center">
			<h2 class="card-title">Thing !</h2>
			<p>Text.</p>
			<div class="card-actions justify-end">
				<button class="btn btn-primary">Accept</button>
				<button class="btn btn-ghost">Deny</button>
			</div>
		</div>
	</div>
</div>
