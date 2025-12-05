<script>
	import '../app.css';
	import Sidebar from '$lib/components/Sidebar.svelte';
	import Widget from '$lib/components/Widget.svelte';
	import Header from '$lib/components/Header.svelte';

	let { children } = $props();
	let sidebarOpen = $state(true);
</script>

<div class="min-h-screen bg-gray-50 dark:bg-gray-900 text-gray-900 dark:text-gray-100 transition-colors">
	<Header bind:sidebarOpen />

	<div class="flex pt-14">
		<!-- サイドバー -->
		<aside
			class="fixed left-0 top-14 h-[calc(100vh-3.5rem)] w-64 bg-white dark:bg-gray-800 border-r border-gray-200 dark:border-gray-700 overflow-y-auto transition-transform z-20
			{sidebarOpen ? 'translate-x-0' : '-translate-x-full'} lg:translate-x-0"
		>
			<Sidebar />
		</aside>

		<!-- メインコンテンツ -->
		<main class="flex-1 lg:ml-64 lg:mr-60 min-h-[calc(100vh-3.5rem)]">
			<div class="max-w-4xl mx-auto px-6 py-8">
				{@render children()}
			</div>
		</main>

		<!-- 右ウィジェット -->
		<aside class="hidden lg:block fixed right-0 top-14 h-[calc(100vh-3.5rem)] w-60 bg-white dark:bg-gray-800 border-l border-gray-200 dark:border-gray-700 overflow-y-auto">
			<Widget />
		</aside>
	</div>
</div>

<!-- モバイル用オーバーレイ -->
{#if sidebarOpen}
	<button
		class="lg:hidden fixed inset-0 bg-black/50 z-10"
		onclick={() => sidebarOpen = false}
		aria-label="サイドバーを閉じる"
	></button>
{/if}
