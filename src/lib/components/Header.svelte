<script>
	import ThemeToggle from './ThemeToggle.svelte';

	let { sidebarOpen = $bindable() } = $props();
</script>

<header class="fixed top-0 left-0 right-0 h-14 bg-white dark:bg-gray-800 border-b border-gray-200 dark:border-gray-700 z-30 flex items-center px-4">
	<!-- メニューボタン（モバイル） -->
	<button
		class="lg:hidden p-2 rounded-lg hover:bg-gray-100 dark:hover:bg-gray-700 mr-2"
		onclick={() => sidebarOpen = !sidebarOpen}
		aria-label="メニュー"
	>
		<svg class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24">
			<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 6h16M4 12h16M4 18h16" />
		</svg>
	</button>

	<!-- ロゴ -->
	<a href="/" class="flex items-center gap-2 font-bold text-xl text-primary-600 dark:text-primary-400">
		<svg class="w-8 h-8" fill="currentColor" viewBox="0 0 24 24">
			<path d="M12 2L2 7l10 5 10-5-10-5zM2 17l10 5 10-5M2 12l10 5 10-5"/>
		</svg>
		<span>さとまたプログラミングラボ</span>
	</a>

	<!-- スペーサー -->
	<div class="flex-1"></div>

	<!-- テーマ切替 -->
	<ThemeToggle />
</header>
