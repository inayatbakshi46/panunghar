<script>
	import { page } from '$app/state';
</script>

<svelte:head>
	<title>{page.status} - Error</title>
</svelte:head>

<div class="flex min-h-screen flex-col items-center justify-center">
	<h1 class="text-7xl font-bold">{page.status}</h1>
	<p>{page.error?.message}</p>

	<a href="/" class="mt-6 rounded bg-blue-600 px-4 py-2 text-white">
		Go Home
	</a>
</div>