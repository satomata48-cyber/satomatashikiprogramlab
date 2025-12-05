<script>
	import { onMount } from 'svelte';

	let isDark = $state(false);

	onMount(() => {
		// ローカルストレージから取得、なければシステム設定を使用
		const stored = localStorage.getItem('theme');
		if (stored) {
			isDark = stored === 'dark';
		} else {
			isDark = window.matchMedia('(prefers-color-scheme: dark)').matches;
		}
		updateTheme();
	});

	function toggleTheme() {
		isDark = !isDark;
		localStorage.setItem('theme', isDark ? 'dark' : 'light');
		updateTheme();
	}

	function updateTheme() {
		if (isDark) {
			document.documentElement.classList.add('dark');
		} else {
			document.documentElement.classList.remove('dark');
		}
	}
</script>

<button
	onclick={toggleTheme}
	class="p-2 rounded-lg hover:bg-gray-100 dark:hover:bg-gray-700 transition-colors"
	aria-label={isDark ? 'ライトモードに切替' : 'ダークモードに切替'}
>
	{#if isDark}
		<!-- 太陽アイコン -->
		<svg class="w-5 h-5 text-yellow-500" fill="currentColor" viewBox="0 0 24 24">
			<path d="M12 3v1m0 16v1m9-9h-1M4 12H3m15.364 6.364l-.707-.707M6.343 6.343l-.707-.707m12.728 0l-.707.707M6.343 17.657l-.707.707M16 12a4 4 0 11-8 0 4 4 0 018 0z"/>
		</svg>
	{:else}
		<!-- 月アイコン -->
		<svg class="w-5 h-5 text-gray-600" fill="currentColor" viewBox="0 0 24 24">
			<path d="M21 12.79A9 9 0 1 1 11.21 3 7 7 0 0 0 21 12.79z"/>
		</svg>
	{/if}
</button>
