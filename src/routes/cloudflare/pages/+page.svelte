<script>
	import CodePreview from '$lib/components/CodePreview.svelte';
	import FeatureCard from '$lib/components/FeatureCard.svelte';

	const features = [
		{ icon: '🚀', title: '高速デプロイ', description: 'Git pushで自動デプロイ', tag: 'CI/CD' },
		{ icon: '🌍', title: 'グローバルCDN', description: '世界中で高速配信', tag: 'パフォーマンス' },
		{ icon: '🔄', title: 'プレビュー', description: 'PRごとにプレビューURL', tag: '開発' },
		{ icon: '⚡', title: 'サーバーレス', description: 'フルスタックアプリ対応', tag: '機能' }
	];
</script>

<svelte:head>
	<title>Cloudflare Pages | さとまたラボ</title>
</svelte:head>

<article>
	<h1 class="text-3xl font-bold mb-2">Pages デプロイ</h1>
	<p class="text-lg text-gray-600 dark:text-gray-400 mb-8">
		SvelteKitアプリをCloudflare Pagesにデプロイ
	</p>

	<!-- Pagesとは -->
	<section class="mb-10">
		<h2 id="what-is" class="text-xl font-bold mb-4">Cloudflare Pagesとは？</h2>

		<div class="p-6 rounded-xl bg-orange-50 dark:bg-orange-900/20 border border-orange-200 dark:border-orange-800 mb-6">
			<p class="text-orange-800 dark:text-orange-200 mb-4">
				<strong>一言で言うと：</strong>「Vercelみたいな、でもCloudflareエッジで動くホスティング」
			</p>
			<p class="text-sm text-orange-700 dark:text-orange-300">
				静的サイトからフルスタックアプリまで、GitHubと連携して自動デプロイ。
				D1やR2などCloudflareサービスとシームレスに連携できます。
			</p>
		</div>
	</section>

	<!-- 特徴 -->
	<section class="mb-10">
		<h2 id="features" class="text-xl font-bold mb-4">Pagesの特徴</h2>
		<div class="grid grid-cols-1 md:grid-cols-2 gap-3">
			{#each features as feature}
				<FeatureCard {...feature} />
			{/each}
		</div>
	</section>

	<!-- 料金 -->
	<section class="mb-10">
		<h2 id="pricing" class="text-xl font-bold mb-4">料金</h2>

		<div class="grid md:grid-cols-2 gap-4">
			<div class="p-4 rounded-lg bg-gray-50 dark:bg-gray-800 border border-gray-200 dark:border-gray-700">
				<h3 class="font-bold text-lg mb-2">Free</h3>
				<ul class="text-sm text-gray-600 dark:text-gray-400 space-y-1">
					<li>・プロジェクト数: 無制限</li>
					<li>・ビルド: 500回/月</li>
					<li>・同時ビルド: 1</li>
					<li>・帯域幅: 無制限</li>
				</ul>
			</div>
			<div class="p-4 rounded-lg bg-orange-50 dark:bg-orange-900/20 border border-orange-200 dark:border-orange-800">
				<h3 class="font-bold text-lg mb-2">Pro ($20/月〜)</h3>
				<ul class="text-sm text-gray-600 dark:text-gray-400 space-y-1">
					<li>・ビルド: 5000回/月</li>
					<li>・同時ビルド: 5</li>
					<li>・ビルド時間: 20分まで</li>
					<li>・Web Analytics</li>
				</ul>
			</div>
		</div>

		<p class="mt-3 text-sm text-gray-600 dark:text-gray-400">
			個人開発なら無料プランで十分です。
		</p>
	</section>

	<!-- デプロイ方法 -->
	<section class="mb-10">
		<h2 id="deploy" class="text-xl font-bold mb-4">デプロイ方法</h2>

		<h3 class="text-lg font-semibold mb-3">方法1: Wrangler CLI（推奨）</h3>

		<CodePreview
			title="CLIでデプロイ"
			description="ローカルからデプロイ"
			language="bash"
			code={`# ビルド
npm run build

# デプロイ（初回は対話形式でプロジェクト作成）
wrangler pages deploy .svelte-kit/cloudflare

# プロジェクト名を指定してデプロイ
wrangler pages deploy .svelte-kit/cloudflare --project-name=my-app`}
		/>

		<h3 class="text-lg font-semibold mb-3 mt-6">方法2: GitHub連携</h3>

		<div class="space-y-3">
			<div class="flex items-start gap-3 p-3 rounded-lg bg-gray-50 dark:bg-gray-800">
				<span class="flex-shrink-0 w-8 h-8 flex items-center justify-center rounded-full bg-orange-500 text-white font-bold">1</span>
				<div>
					<p class="font-semibold">Cloudflare ダッシュボードへ</p>
					<p class="text-sm text-gray-600 dark:text-gray-400">
						Workers & Pages → Create → Pages → Connect to Git
					</p>
				</div>
			</div>
			<div class="flex items-start gap-3 p-3 rounded-lg bg-gray-50 dark:bg-gray-800">
				<span class="flex-shrink-0 w-8 h-8 flex items-center justify-center rounded-full bg-orange-500 text-white font-bold">2</span>
				<div>
					<p class="font-semibold">リポジトリを選択</p>
					<p class="text-sm text-gray-600 dark:text-gray-400">
						GitHubアカウントを連携して、リポジトリを選択
					</p>
				</div>
			</div>
			<div class="flex items-start gap-3 p-3 rounded-lg bg-gray-50 dark:bg-gray-800">
				<span class="flex-shrink-0 w-8 h-8 flex items-center justify-center rounded-full bg-orange-500 text-white font-bold">3</span>
				<div>
					<p class="font-semibold">ビルド設定</p>
					<p class="text-sm text-gray-600 dark:text-gray-400">
						Framework: SvelteKit<br/>
						Build command: npm run build<br/>
						Build output: .svelte-kit/cloudflare
					</p>
				</div>
			</div>
			<div class="flex items-start gap-3 p-3 rounded-lg bg-gray-50 dark:bg-gray-800">
				<span class="flex-shrink-0 w-8 h-8 flex items-center justify-center rounded-full bg-green-500 text-white font-bold">4</span>
				<div>
					<p class="font-semibold">完了！</p>
					<p class="text-sm text-gray-600 dark:text-gray-400">
						mainにpushするたびに自動デプロイ
					</p>
				</div>
			</div>
		</div>
	</section>

	<!-- D1/R2バインディング -->
	<section class="mb-10">
		<h2 id="bindings" class="text-xl font-bold mb-4">D1/R2のバインディング設定</h2>

		<p class="text-gray-700 dark:text-gray-300 mb-4">
			GitHub連携の場合、ダッシュボードでバインディングを設定する必要があります。
		</p>

		<div class="space-y-3">
			<div class="flex items-start gap-3 p-3 rounded-lg bg-gray-50 dark:bg-gray-800">
				<span class="flex-shrink-0 w-8 h-8 flex items-center justify-center rounded-full bg-blue-500 text-white font-bold">1</span>
				<div>
					<p class="font-semibold">Settings → Functions → D1 database bindings</p>
					<p class="text-sm text-gray-600 dark:text-gray-400">
						Variable name: DB（wrangler.jsonのbindingと同じ）<br/>
						D1 database: 作成したD1を選択
					</p>
				</div>
			</div>
			<div class="flex items-start gap-3 p-3 rounded-lg bg-gray-50 dark:bg-gray-800">
				<span class="flex-shrink-0 w-8 h-8 flex items-center justify-center rounded-full bg-blue-500 text-white font-bold">2</span>
				<div>
					<p class="font-semibold">R2 bucket bindings（R2を使う場合）</p>
					<p class="text-sm text-gray-600 dark:text-gray-400">
						Variable name: BUCKET<br/>
						R2 bucket: 作成したバケットを選択
					</p>
				</div>
			</div>
		</div>

		<div class="mt-4 p-4 rounded-lg bg-amber-50 dark:bg-amber-900/20 border border-amber-200 dark:border-amber-800">
			<p class="font-semibold text-amber-800 dark:text-amber-200 mb-2">Wrangler CLIなら自動</p>
			<p class="text-sm text-amber-700 dark:text-amber-300">
				<code>wrangler pages deploy</code> を使う場合、wrangler.jsonの設定が自動で反映されるので
				ダッシュボードでの設定は不要です。
			</p>
		</div>
	</section>

	<!-- プレビュー -->
	<section class="mb-10">
		<h2 id="preview" class="text-xl font-bold mb-4">プレビューデプロイ</h2>

		<div class="p-4 rounded-lg bg-green-50 dark:bg-green-900/20 border border-green-200 dark:border-green-800">
			<p class="font-semibold text-green-800 dark:text-green-200 mb-2">ブランチごとにプレビューURL</p>
			<p class="text-sm text-green-700 dark:text-green-300 mb-3">
				main以外のブランチにpushすると、自動でプレビューURLが発行されます。
				本番に影響を与えずにテストできます。
			</p>
			<div class="font-mono text-xs bg-white dark:bg-gray-800 p-2 rounded">
				<p>main → https://my-app.pages.dev/</p>
				<p>feature/new-ui → https://abc123.my-app.pages.dev/</p>
			</div>
		</div>
	</section>

	<!-- ナビゲーション -->
	<div class="flex justify-between pt-6 border-t border-gray-200 dark:border-gray-700">
		<a href="/cloudflare/r2" class="inline-flex items-center gap-2 px-4 py-2 rounded-lg border border-gray-300 dark:border-gray-600 hover:bg-gray-100 dark:hover:bg-gray-800 transition-colors">
			<svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
				<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 19l-7-7 7-7" />
			</svg>
			前へ：R2 ストレージ
		</a>
		<a href="/dev/my-workflow" class="inline-flex items-center gap-2 px-4 py-2 rounded-lg bg-primary-600 text-white hover:bg-primary-700 transition-colors">
			次へ：開発方法
			<svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
				<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 5l7 7-7 7" />
			</svg>
		</a>
	</div>
</article>
