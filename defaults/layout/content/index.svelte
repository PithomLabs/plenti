<script>
	export let title, intro, components, allContent;
	import Grid from '../components/grid.svelte';
	import { loadComponent } from '../scripts/load_component.svelte';
</script>

<h1>{title}</h1>

<section id="intro">
	<p>{@html intro.slogan}</p>
</section>

<section id="intro">
	{#each intro.help as paragraph}
		<p>{@html paragraph}</p>
	{/each}
</section>

<div>
	<h3>Recent blog posts:</h3>
	<Grid items={allContent} filter="blog" />
	<br />
</div>

{#if components}
	{#each components as { component, fields }}
		{#await loadComponent(component)}
			loading component...
		{:then compClass}
			<svelte:component this="{compClass}" {...fields} />
		{:catch error}
			{console.log(error.message)}
		{/await}
	{/each}
{/if}