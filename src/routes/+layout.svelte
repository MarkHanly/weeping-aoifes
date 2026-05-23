<script lang="ts">
	import './layout.css';
	import '../app.css';
	import favicon from '$lib/assets/favicon.ico';
	import Header from '$lib/components/Header.svelte';

	let { children } = $props();
</script>

<svelte:head>
	<link rel="icon" href={favicon} />
	
  <meta property="og:title" content="Weeping Aoifes" />
  <meta property="og:description" content="Explore the Blindboy Podcast" />
  <meta property="og:image" content="$lib/assets/android-chrome-512x512.png" />
  <meta property="og:url" content="https://weeping-aoifes.netlify.app/" />
  <meta property="og:type" content="website" />
  <meta name="twitter:card" content="summary_large_image" />
  <meta name="twitter:title" content="Weeping Aoifes" />
  <meta name="twitter:description" content="Explore the Blindboy Podcast" />
  <meta name="twitter:image" content="$lib/assets/android-chrome-512x512.png" />

</svelte:head>
<Header />
{@render children()}

