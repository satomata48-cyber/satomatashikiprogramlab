<script>
	const technologies = [
		{ name: 'HTML', icon: '🌐', color: 'bg-orange-500', href: '/html/basics', desc: 'Webページの構造を作る' },
		{ name: 'CSS', icon: '🎨', color: 'bg-blue-500', href: '/css/selectors', desc: 'スタイルとデザインを適用' },
		{ name: 'JavaScript', icon: '⚡', color: 'bg-yellow-500', href: '/js/variables', desc: '動的な機能を実装' },
		{ name: 'Next.js', icon: '▲', color: 'bg-gray-900 dark:bg-white', href: '/nextjs/intro', desc: 'Reactベースのフレームワーク' },
		{ name: 'SvelteKit', icon: '🔥', color: 'bg-orange-600', href: '/sveltekit/intro', desc: '高速でシンプルなフレームワーク' },
		{ name: 'Tailwind', icon: '💨', color: 'bg-cyan-500', href: '/tailwind/intro', desc: 'ユーティリティファーストCSS' }
	];
</script>

<svelte:head>
	<title>プログラミング解説 | ホーム</title>
</svelte:head>

<div class="space-y-6 sm:space-y-8">
	<!-- ヒーローセクション -->
	<section class="text-center py-6 sm:py-8 md:py-12">
		<h1 class="text-2xl sm:text-3xl md:text-4xl font-bold mb-3 sm:mb-4 bg-gradient-to-r from-primary-600 to-cyan-500 bg-clip-text text-transparent px-2">
			プログラミングを視覚的に学ぼう
		</h1>
		<p class="text-sm sm:text-base md:text-lg text-gray-600 dark:text-gray-400 max-w-2xl mx-auto px-2">
			初心者向けに、Web開発の基礎から最新のフレームワークまで、
			分かりやすく解説しています。
		</p>
	</section>

	<!-- 技術カード -->
	<section>
		<h2 id="technologies" class="text-xl sm:text-2xl font-bold mb-4 sm:mb-6">学べる技術</h2>
		<div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-3 sm:gap-4">
			{#each technologies as tech}
				<a
					href={tech.href}
					class="block p-4 sm:p-6 rounded-xl border border-gray-200 dark:border-gray-700 bg-white dark:bg-gray-800 hover:shadow-lg hover:border-primary-300 dark:hover:border-primary-600 transition-all group"
				>
					<div class="flex items-center gap-3 sm:gap-4 mb-2 sm:mb-3">
						<span class="text-2xl sm:text-3xl flex-shrink-0">{tech.icon}</span>
						<h3 class="text-lg sm:text-xl font-semibold group-hover:text-primary-600 dark:group-hover:text-primary-400 transition-colors">
							{tech.name}
						</h3>
					</div>
					<p class="text-sm sm:text-base text-gray-600 dark:text-gray-400">{tech.desc}</p>
				</a>
			{/each}
		</div>
	</section>

	<!-- 特徴セクション -->
	<section>
		<h2 id="features" class="text-xl sm:text-2xl font-bold mb-4 sm:mb-6">このサイトの特徴</h2>
		<div class="grid grid-cols-1 sm:grid-cols-2 gap-3 sm:gap-6">
			<div class="flex gap-3 sm:gap-4 p-3 sm:p-4 rounded-lg bg-gray-100 dark:bg-gray-800">
				<div class="text-2xl sm:text-3xl flex-shrink-0">📖</div>
				<div class="min-w-0">
					<h3 class="font-semibold mb-1 text-sm sm:text-base">初心者向け解説</h3>
					<p class="text-xs sm:text-sm text-gray-600 dark:text-gray-400">
						専門用語を避け、図解を交えて分かりやすく説明
					</p>
				</div>
			</div>
			<div class="flex gap-3 sm:gap-4 p-3 sm:p-4 rounded-lg bg-gray-100 dark:bg-gray-800">
				<div class="text-2xl sm:text-3xl flex-shrink-0">💻</div>
				<div class="min-w-0">
					<h3 class="font-semibold mb-1 text-sm sm:text-base">実践的なコード例</h3>
					<p class="text-xs sm:text-sm text-gray-600 dark:text-gray-400">
						すぐに試せるサンプルコードを豊富に掲載
					</p>
				</div>
			</div>
			<div class="flex gap-3 sm:gap-4 p-3 sm:p-4 rounded-lg bg-gray-100 dark:bg-gray-800">
				<div class="text-2xl sm:text-3xl flex-shrink-0">🌙</div>
				<div class="min-w-0">
					<h3 class="font-semibold mb-1 text-sm sm:text-base">ダークモード対応</h3>
					<p class="text-xs sm:text-sm text-gray-600 dark:text-gray-400">
						目に優しいダークモードで快適に学習
					</p>
				</div>
			</div>
			<div class="flex gap-3 sm:gap-4 p-3 sm:p-4 rounded-lg bg-gray-100 dark:bg-gray-800">
				<div class="text-2xl sm:text-3xl flex-shrink-0">📱</div>
				<div class="min-w-0">
					<h3 class="font-semibold mb-1 text-sm sm:text-base">レスポンシブ対応</h3>
					<p class="text-xs sm:text-sm text-gray-600 dark:text-gray-400">
						スマホやタブレットでも快適に閲覧
					</p>
				</div>
			</div>
		</div>
	</section>

	<!-- 始め方 -->
	<section>
		<h2 id="getting-started" class="text-xl sm:text-2xl font-bold mb-4 sm:mb-6">はじめ方</h2>
		<div class="prose dark:prose-invert max-w-none">
			<p class="text-sm sm:text-base text-gray-600 dark:text-gray-400">
				左のサイドバーから学びたい技術を選んでください。
				各セクションは基礎から順番に学べるように構成されています。
			</p>
			<p class="text-sm sm:text-base text-gray-600 dark:text-gray-400 mt-3 sm:mt-4">
				Web開発が初めての方は、<strong>HTML → CSS → JavaScript</strong> の順番で学習することをおすすめします。
			</p>
		</div>
	</section>
</div>
