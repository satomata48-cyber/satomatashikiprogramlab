<script>
	import { onMount } from 'svelte';
	import '../app.css';
	import Sidebar from '$lib/components/Sidebar.svelte';
	import Widget from '$lib/components/Widget.svelte';
	import Header from '$lib/components/Header.svelte';

	let { children } = $props();
	let sidebarOpen = $state(false);

	// 画面サイズに応じてサイドバーの初期状態を設定
	onMount(() => {
		if (window.innerWidth >= 1024) {
			sidebarOpen = true;
		}

		// サイドバーを閉じるカスタムイベントをリッスン
		const handleCloseSidebar = () => {
			sidebarOpen = false;
		};
		window.addEventListener('closeSidebar', handleCloseSidebar);

		return () => {
			window.removeEventListener('closeSidebar', handleCloseSidebar);
		};
	});
</script>

<div class="min-h-screen bg-gray-50 dark:bg-gray-900 text-gray-900 dark:text-gray-100 transition-colors">
	<Header bind:sidebarOpen />

	<div class="flex pt-14">
		<!-- サイドバー -->
		<aside
			class="fixed left-0 top-14 h-[calc(100vh-3.5rem)] w-[85vw] max-w-xs sm:w-72 md:w-64 bg-white dark:bg-gray-800 border-r border-gray-200 dark:border-gray-700 overflow-y-auto transition-transform duration-300 z-20
			{sidebarOpen ? 'translate-x-0' : '-translate-x-full'} lg:translate-x-0"
		>
			<Sidebar />
		</aside>

		<!-- メインコンテンツ -->
		<main class="flex-1 lg:ml-64 xl:mr-60 min-h-[calc(100vh-3.5rem)] w-full">
			<div class="max-w-4xl mx-auto px-3 sm:px-4 md:px-6 py-4 sm:py-6 md:py-8">
				{@render children()}
			</div>
		</main>

		<!-- 右ウィジェット -->
		<aside class="hidden xl:block fixed right-0 top-14 h-[calc(100vh-3.5rem)] w-60 bg-white dark:bg-gray-800 border-l border-gray-200 dark:border-gray-700 overflow-y-auto">
			<Widget />
		</aside>
	</div>
</div>

<!-- モバイル用オーバーレイ -->
{#if sidebarOpen}
	<button
		class="lg:hidden fixed inset-0 bg-black/50 z-10 transition-opacity duration-300"
		onclick={() => sidebarOpen = false}
		aria-label="サイドバーを閉じる"
		tabindex="-1"
	></button>
{/if}
