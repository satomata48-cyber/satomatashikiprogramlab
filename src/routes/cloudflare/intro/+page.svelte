<script>
	import FeatureCard from '$lib/components/FeatureCard.svelte';

	const services = [
		{ icon: '🗄️', title: 'D1', description: 'サーバーレスSQLiteデータベース', tag: 'データベース' },
		{ icon: '📦', title: 'R2', description: 'S3互換オブジェクトストレージ', tag: 'ストレージ' },
		{ icon: '🚀', title: 'Pages', description: '静的サイト & フルスタックホスティング', tag: 'ホスティング' },
		{ icon: '⚡', title: 'Workers', description: 'エッジで動くサーバーレス関数', tag: 'コンピュート' },
		{ icon: '🔑', title: 'KV', description: 'グローバル分散キーバリューストア', tag: 'ストレージ' },
		{ icon: '🔒', title: 'Access', description: 'ゼロトラストセキュリティ', tag: 'セキュリティ' }
	];
</script>

<svelte:head>
	<title>Cloudflare はじめに | さとまたラボ</title>
</svelte:head>

<article>
	<h1 class="text-3xl font-bold mb-2">Cloudflare</h1>
	<p class="text-lg text-gray-600 dark:text-gray-400 mb-8">
		エッジコンピューティングで世界中を高速に
	</p>

	<!-- Cloudflareとは -->
	<section class="mb-10">
		<h2 id="what-is" class="text-xl font-bold mb-4">Cloudflareとは？</h2>

		<div class="p-6 rounded-xl bg-orange-50 dark:bg-orange-900/20 border border-orange-200 dark:border-orange-800 mb-6">
			<p class="text-orange-800 dark:text-orange-200 mb-4">
				<strong>一言で言うと：</strong>「世界中のエッジで動くクラウドプラットフォーム」
			</p>
			<div class="grid grid-cols-1 md:grid-cols-2 gap-4 text-sm">
				<div class="p-3 bg-white dark:bg-gray-800 rounded-lg">
					<div class="font-semibold text-orange-700 dark:text-orange-300 mb-2">従来のクラウド</div>
					<ul class="text-gray-600 dark:text-gray-400 space-y-1">
						<li>・特定のリージョンにサーバーがある</li>
						<li>・遠いユーザーは遅延が発生</li>
						<li>・サーバー管理が必要な場合も</li>
						<li>・リソースベースの課金</li>
					</ul>
				</div>
				<div class="p-3 bg-white dark:bg-gray-800 rounded-lg">
					<div class="font-semibold text-orange-700 dark:text-orange-300 mb-2">Cloudflareなら...</div>
					<ul class="text-gray-600 dark:text-gray-400 space-y-1">
						<li>・世界300+のエッジロケーション</li>
						<li>・ユーザーに最も近い場所で実行</li>
						<li>・完全サーバーレス</li>
						<li>・使った分だけの課金</li>
					</ul>
				</div>
			</div>
		</div>

		<div class="p-4 rounded-lg bg-blue-50 dark:bg-blue-900/20 border border-blue-200 dark:border-blue-800">
			<p class="font-semibold text-blue-800 dark:text-blue-200">エッジコンピューティングとは？</p>
			<p class="text-sm text-blue-700 dark:text-blue-300 mt-2">
				ユーザーに物理的に近い場所（エッジ）でコードを実行する技術。
				東京のユーザーには東京のエッジで、ニューヨークのユーザーにはニューヨークのエッジで処理されるため、
				レイテンシが大幅に削減されます。
			</p>
		</div>
	</section>

	<!-- 主要サービス -->
	<section class="mb-10">
		<h2 id="services" class="text-xl font-bold mb-4">主要サービス</h2>
		<div class="grid grid-cols-1 md:grid-cols-2 gap-3">
			{#each services as service}
				<FeatureCard {...service} />
			{/each}
		</div>
	</section>

	<!-- 個人開発での活用 -->
	<section class="mb-10">
		<h2 id="for-indie" class="text-xl font-bold mb-4">個人開発に最適な理由</h2>

		<div class="space-y-4">
			<div class="p-4 rounded-lg bg-green-50 dark:bg-green-900/20 border border-green-200 dark:border-green-800">
				<p class="font-semibold text-green-800 dark:text-green-200 mb-2">1. 無料枠が充実</p>
				<ul class="text-sm text-green-700 dark:text-green-300 space-y-1">
					<li>・<strong>D1</strong>：読み取り500万回/日、書き込み10万回/日</li>
					<li>・<strong>R2</strong>：10GB、100万リクエスト/月</li>
					<li>・<strong>Pages</strong>：無制限のサイト、500ビルド/月</li>
					<li>・<strong>Workers</strong>：10万リクエスト/日</li>
				</ul>
			</div>

			<div class="p-4 rounded-lg bg-blue-50 dark:bg-blue-900/20 border border-blue-200 dark:border-blue-800">
				<p class="font-semibold text-blue-800 dark:text-blue-200 mb-2">2. セットアップが簡単</p>
				<p class="text-sm text-blue-700 dark:text-blue-300">
					Wrangler CLIで数コマンドでデプロイ完了。
					GitHubと連携すれば、プッシュするだけで自動デプロイ。
				</p>
			</div>

			<div class="p-4 rounded-lg bg-purple-50 dark:bg-purple-900/20 border border-purple-200 dark:border-purple-800">
				<p class="font-semibold text-purple-800 dark:text-purple-200 mb-2">3. SvelteKitとの相性抜群</p>
				<p class="text-sm text-purple-700 dark:text-purple-300">
					公式アダプター（adapter-cloudflare）があり、
					SvelteKitのすべての機能をCloudflare上で動かせます。
				</p>
			</div>
		</div>
	</section>

	<!-- 技術スタック -->
	<section class="mb-10">
		<h2 id="stack" class="text-xl font-bold mb-4">おすすめ技術スタック</h2>

		<div class="p-6 rounded-xl bg-gradient-to-r from-orange-50 to-blue-50 dark:from-orange-900/20 dark:to-blue-900/20 border border-orange-200 dark:border-orange-800">
			<div class="grid md:grid-cols-4 gap-4 text-center">
				<div class="p-3 bg-white dark:bg-gray-800 rounded-lg">
					<span class="text-2xl">🔥</span>
					<p class="font-semibold mt-1">SvelteKit</p>
					<p class="text-xs text-gray-500">フロントエンド</p>
				</div>
				<div class="p-3 bg-white dark:bg-gray-800 rounded-lg">
					<span class="text-2xl">💨</span>
					<p class="font-semibold mt-1">Tailwind</p>
					<p class="text-xs text-gray-500">スタイリング</p>
				</div>
				<div class="p-3 bg-white dark:bg-gray-800 rounded-lg">
					<span class="text-2xl">🗄️</span>
					<p class="font-semibold mt-1">D1</p>
					<p class="text-xs text-gray-500">データベース</p>
				</div>
				<div class="p-3 bg-white dark:bg-gray-800 rounded-lg">
					<span class="text-2xl">📦</span>
					<p class="font-semibold mt-1">R2</p>
					<p class="text-xs text-gray-500">ファイル保存</p>
				</div>
			</div>
			<p class="text-center text-sm text-gray-600 dark:text-gray-400 mt-4">
				この組み合わせで、個人開発のほとんどのユースケースをカバーできます
			</p>
		</div>
	</section>

	<!-- 始め方 -->
	<section class="mb-10">
		<h2 id="getting-started" class="text-xl font-bold mb-4">始め方</h2>

		<div class="space-y-3">
			<div class="flex items-start gap-3 p-3 rounded-lg bg-gray-50 dark:bg-gray-800">
				<span class="flex-shrink-0 w-8 h-8 flex items-center justify-center rounded-full bg-orange-500 text-white font-bold">1</span>
				<div>
					<p class="font-semibold">Cloudflareアカウント作成</p>
					<p class="text-sm text-gray-600 dark:text-gray-400">
						<a href="https://dash.cloudflare.com/sign-up" target="_blank" class="text-orange-600 hover:underline">cloudflare.com</a> で無料アカウントを作成
					</p>
				</div>
			</div>
			<div class="flex items-start gap-3 p-3 rounded-lg bg-gray-50 dark:bg-gray-800">
				<span class="flex-shrink-0 w-8 h-8 flex items-center justify-center rounded-full bg-orange-500 text-white font-bold">2</span>
				<div>
					<p class="font-semibold">Wrangler CLIをインストール</p>
					<p class="text-sm text-gray-600 dark:text-gray-400">
						<code class="bg-gray-200 dark:bg-gray-700 px-1 rounded">npm install -D wrangler</code>
					</p>
				</div>
			</div>
			<div class="flex items-start gap-3 p-3 rounded-lg bg-gray-50 dark:bg-gray-800">
				<span class="flex-shrink-0 w-8 h-8 flex items-center justify-center rounded-full bg-orange-500 text-white font-bold">3</span>
				<div>
					<p class="font-semibold">ログイン</p>
					<p class="text-sm text-gray-600 dark:text-gray-400">
						<code class="bg-gray-200 dark:bg-gray-700 px-1 rounded">wrangler login</code>
					</p>
				</div>
			</div>
			<div class="flex items-start gap-3 p-3 rounded-lg bg-gray-50 dark:bg-gray-800">
				<span class="flex-shrink-0 w-8 h-8 flex items-center justify-center rounded-full bg-green-500 text-white font-bold">4</span>
				<div>
					<p class="font-semibold">サービスを使い始める</p>
					<p class="text-sm text-gray-600 dark:text-gray-400">
						D1、R2、Pagesなど、必要なサービスをセットアップ
					</p>
				</div>
			</div>
		</div>
	</section>

	<!-- ナビゲーション -->
	<div class="flex justify-between pt-6 border-t border-gray-200 dark:border-gray-700">
		<a href="/supabase/storage" class="inline-flex items-center gap-2 px-4 py-2 rounded-lg border border-gray-300 dark:border-gray-600 hover:bg-gray-100 dark:hover:bg-gray-800 transition-colors">
			<svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
				<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 19l-7-7 7-7" />
			</svg>
			前へ：Supabase
		</a>
		<a href="/cloudflare/d1" class="inline-flex items-center gap-2 px-4 py-2 rounded-lg bg-primary-600 text-white hover:bg-primary-700 transition-colors">
			次へ：D1 データベース
			<svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
				<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 5l7 7-7 7" />
			</svg>
		</a>
	</div>
</article>
