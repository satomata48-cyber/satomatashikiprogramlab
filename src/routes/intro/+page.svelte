<script>
	import CodePreview from '$lib/components/CodePreview.svelte';
</script>

<svelte:head>
	<title>はじめに | さとまたラボ</title>
</svelte:head>

<article>
	<h1 class="text-3xl font-bold mb-2">はじめに</h1>
	<p class="text-lg text-gray-600 dark:text-gray-400 mb-8">
		このサイトについてと、2025年のWeb開発トレンド
	</p>

	<!-- このサイトについて -->
	<section class="mb-12">
		<h2 id="about" class="text-xl font-bold mb-4">このサイトについて</h2>

		<div class="p-6 rounded-xl bg-gradient-to-r from-blue-50 to-purple-50 dark:from-blue-900/20 dark:to-purple-900/20 border border-blue-200 dark:border-blue-800 mb-6">
			<p class="text-lg text-blue-800 dark:text-blue-200 mb-4">
				<strong>初心者から実務レベルまで</strong>、モダンWeb開発を学べるサイトです
			</p>
			<p class="text-sm text-blue-700 dark:text-blue-300">
				HTML/CSS/JavaScriptの基礎から、SvelteKit、TypeScript、Tailwind CSSなどの
				最新技術まで、実践的なコード例とともに解説しています。
			</p>
		</div>

		<div class="grid md:grid-cols-3 gap-4 mb-6">
			<div class="p-4 rounded-lg bg-green-50 dark:bg-green-900/20 border border-green-200 dark:border-green-800">
				<p class="font-semibold text-green-800 dark:text-green-200 mb-2">初心者向け</p>
				<p class="text-sm text-green-700 dark:text-green-300">
					「なぜ必要か」「何をしているか」を丁寧に説明
				</p>
			</div>
			<div class="p-4 rounded-lg bg-blue-50 dark:bg-blue-900/20 border border-blue-200 dark:border-blue-800">
				<p class="font-semibold text-blue-800 dark:text-blue-200 mb-2">実践的</p>
				<p class="text-sm text-blue-700 dark:text-blue-300">
					すぐに使えるコード例とプレビュー付き
				</p>
			</div>
			<div class="p-4 rounded-lg bg-purple-50 dark:bg-purple-900/20 border border-purple-200 dark:border-purple-800">
				<p class="font-semibold text-purple-800 dark:text-purple-200 mb-2">最新技術</p>
				<p class="text-sm text-purple-700 dark:text-purple-300">
					2025年のトレンド技術を中心に解説
				</p>
			</div>
		</div>
	</section>

	<!-- 2025年のフレームワーク傾向 -->
	<section class="mb-12">
		<h2 id="trends-2025" class="text-xl font-bold mb-4">2025年のWeb開発トレンド</h2>

		<p class="text-gray-700 dark:text-gray-300 mb-6">
			Web開発の世界は常に進化しています。2025年現在の主要なトレンドを見ていきましょう。
		</p>

		<!-- フロントエンド -->
		<div class="mb-8">
			<h3 class="text-lg font-semibold mb-4 flex items-center gap-2">
				<span class="w-8 h-8 bg-blue-500 text-white rounded-full flex items-center justify-center text-sm">1</span>
				フロントエンドフレームワーク
			</h3>

			<div class="p-5 rounded-xl bg-blue-50 dark:bg-blue-900/20 border border-blue-200 dark:border-blue-800 mb-4">
				<p class="font-semibold text-blue-800 dark:text-blue-200 mb-3">主要プレイヤーの現状</p>
				<div class="space-y-3">
					<div class="flex items-center gap-3">
						<div class="w-20 text-sm font-medium text-gray-700 dark:text-gray-300">React</div>
						<div class="flex-1 bg-gray-200 dark:bg-gray-700 rounded-full h-4">
							<div class="bg-blue-500 h-4 rounded-full" style="width: 82%;"></div>
						</div>
						<span class="text-sm text-gray-600 dark:text-gray-400 w-12">82%</span>
					</div>
					<div class="flex items-center gap-3">
						<div class="w-20 text-sm font-medium text-gray-700 dark:text-gray-300">Next.js</div>
						<div class="flex-1 bg-gray-200 dark:bg-gray-700 rounded-full h-4">
							<div class="bg-gray-800 dark:bg-white h-4 rounded-full" style="width: 53%;"></div>
						</div>
						<span class="text-sm text-gray-600 dark:text-gray-400 w-12">53%</span>
					</div>
					<div class="flex items-center gap-3">
						<div class="w-20 text-sm font-medium text-gray-700 dark:text-gray-300">Vue.js</div>
						<div class="flex-1 bg-gray-200 dark:bg-gray-700 rounded-full h-4">
							<div class="bg-green-500 h-4 rounded-full" style="width: 46%;"></div>
						</div>
						<span class="text-sm text-gray-600 dark:text-gray-400 w-12">46%</span>
					</div>
					<div class="flex items-center gap-3">
						<div class="w-20 text-sm font-medium text-gray-700 dark:text-gray-300">Svelte</div>
						<div class="flex-1 bg-gray-200 dark:bg-gray-700 rounded-full h-4">
							<div class="bg-orange-500 h-4 rounded-full" style="width: 26%;"></div>
						</div>
						<span class="text-sm text-gray-600 dark:text-gray-400 w-12">26%</span>
					</div>
					<div class="flex items-center gap-3">
						<div class="w-20 text-sm font-medium text-gray-700 dark:text-gray-300">Astro</div>
						<div class="flex-1 bg-gray-200 dark:bg-gray-700 rounded-full h-4">
							<div class="bg-purple-500 h-4 rounded-full" style="width: 25%;"></div>
						</div>
						<span class="text-sm text-gray-600 dark:text-gray-400 w-12">25%</span>
					</div>
				</div>
				<p class="text-xs text-gray-500 mt-3">※ State of JS 2024 調査データより</p>
			</div>

			<div class="grid md:grid-cols-2 gap-4">
				<div class="p-4 rounded-lg bg-orange-50 dark:bg-orange-900/20 border border-orange-200 dark:border-orange-800">
					<p class="font-semibold text-orange-800 dark:text-orange-200 mb-2">Svelteが急成長中</p>
					<p class="text-sm text-orange-700 dark:text-orange-300">
						現在25.8%の開発者が使用し、さらに43.6%が「学びたい」と回答。
						ビルド時にコンパイルされるため、ランタイムが不要で高速。
					</p>
				</div>
				<div class="p-4 rounded-lg bg-purple-50 dark:bg-purple-900/20 border border-purple-200 dark:border-purple-800">
					<p class="font-semibold text-purple-800 dark:text-purple-200 mb-2">Astroの台頭</p>
					<p class="text-sm text-purple-700 dark:text-purple-300">
						新しいフレームワークながら25%の採用率。
						「アイランドアーキテクチャ」で必要な部分だけJSを読み込む。
					</p>
				</div>
			</div>
		</div>

		<!-- アーキテクチャトレンド -->
		<div class="mb-8">
			<h3 class="text-lg font-semibold mb-4 flex items-center gap-2">
				<span class="w-8 h-8 bg-green-500 text-white rounded-full flex items-center justify-center text-sm">2</span>
				アーキテクチャのトレンド
			</h3>

			<div class="space-y-4">
				<div class="p-4 rounded-lg bg-green-50 dark:bg-green-900/20 border border-green-200 dark:border-green-800">
					<p class="font-semibold text-green-800 dark:text-green-200 mb-2">サーバーサイドへの回帰</p>
					<p class="text-sm text-green-700 dark:text-green-300">
						「ブラウザに送るJavaScriptを減らす」という方向性が主流に。
						SSR（サーバーサイドレンダリング）やSSG（静的サイト生成）が再び注目されています。
						Next.jsのServer Components、SvelteKitのサーバーサイド処理がその代表例です。
					</p>
				</div>

				<div class="p-4 rounded-lg bg-blue-50 dark:bg-blue-900/20 border border-blue-200 dark:border-blue-800">
					<p class="font-semibold text-blue-800 dark:text-blue-200 mb-2">エッジコンピューティング</p>
					<p class="text-sm text-blue-700 dark:text-blue-300">
						2024年に世界で14%増加。Cloudflare Workers、Vercel Edge Functions、Deno Deployなど、
						ユーザーに近いサーバーで処理を行うことで、超高速なレスポンスを実現。
					</p>
				</div>

				<div class="p-4 rounded-lg bg-amber-50 dark:bg-amber-900/20 border border-amber-200 dark:border-amber-800">
					<p class="font-semibold text-amber-800 dark:text-amber-200 mb-2">ローカルファースト</p>
					<p class="text-sm text-amber-700 dark:text-amber-300">
						データをまずローカルに保存し、後からサーバーと同期する設計が増加中。
						オフライン対応、プライバシー重視のアプリに最適。
					</p>
				</div>
			</div>
		</div>

		<!-- バックエンド・ランタイム -->
		<div class="mb-8">
			<h3 class="text-lg font-semibold mb-4 flex items-center gap-2">
				<span class="w-8 h-8 bg-purple-500 text-white rounded-full flex items-center justify-center text-sm">3</span>
				バックエンド・ランタイム
			</h3>

			<div class="grid md:grid-cols-2 gap-4">
				<div class="p-4 rounded-lg bg-yellow-50 dark:bg-yellow-900/20 border border-yellow-200 dark:border-yellow-800">
					<p class="font-semibold text-yellow-800 dark:text-yellow-200 mb-2">Bunの成熟</p>
					<p class="text-sm text-yellow-700 dark:text-yellow-300">
						Node.jsの代替として注目されていたBunが本番環境で安定稼働。
						Express、Fastifyなど主要フレームワークと互換性あり。圧倒的な速度が魅力。
					</p>
				</div>
				<div class="p-4 rounded-lg bg-red-50 dark:bg-red-900/20 border border-red-200 dark:border-red-800">
					<p class="font-semibold text-red-800 dark:text-red-200 mb-2">NestJSの躍進</p>
					<p class="text-sm text-red-700 dark:text-red-300">
						TypeScript + MVCアーキテクチャで、エンタープライズ向け開発に人気。
						モジュラー設計でテストしやすく、大規模開発に最適。
					</p>
				</div>
			</div>
		</div>

		<!-- TypeScript -->
		<div class="mb-8">
			<h3 class="text-lg font-semibold mb-4 flex items-center gap-2">
				<span class="w-8 h-8 bg-blue-600 text-white rounded-full flex items-center justify-center text-sm">4</span>
				TypeScriptの標準化
			</h3>

			<div class="p-5 rounded-xl bg-blue-50 dark:bg-blue-900/20 border border-blue-200 dark:border-blue-800">
				<p class="text-blue-800 dark:text-blue-200 mb-3">
					<strong>TypeScriptはもはや「オプション」ではなく「標準」に</strong>
				</p>
				<p class="text-sm text-blue-700 dark:text-blue-300 mb-3">
					静的型付けにより、エラーを早期に発見でき、コード品質が向上。
					ほぼすべてのモダンフレームワークがTypeScriptを公式サポートしています。
				</p>
				<div class="flex flex-wrap gap-2">
					<span class="px-2 py-1 bg-blue-200 dark:bg-blue-800 rounded text-xs">SvelteKit</span>
					<span class="px-2 py-1 bg-blue-200 dark:bg-blue-800 rounded text-xs">Next.js</span>
					<span class="px-2 py-1 bg-blue-200 dark:bg-blue-800 rounded text-xs">NestJS</span>
					<span class="px-2 py-1 bg-blue-200 dark:bg-blue-800 rounded text-xs">Astro</span>
					<span class="px-2 py-1 bg-blue-200 dark:bg-blue-800 rounded text-xs">Vue 3</span>
				</div>
			</div>
		</div>

		<!-- AI駆動開発 -->
		<div class="mb-8">
			<h3 class="text-lg font-semibold mb-4 flex items-center gap-2">
				<span class="w-8 h-8 bg-gradient-to-r from-pink-500 to-purple-500 text-white rounded-full flex items-center justify-center text-sm">5</span>
				AI駆動開発
			</h3>

			<div class="p-5 rounded-xl bg-gradient-to-r from-pink-50 to-purple-50 dark:from-pink-900/20 dark:to-purple-900/20 border border-pink-200 dark:border-pink-800">
				<p class="font-semibold text-purple-800 dark:text-purple-200 mb-3">2025年最大のゲームチェンジャー</p>
				<p class="text-sm text-purple-700 dark:text-purple-300 mb-4">
					Claude Code、Cursor、GitHub Copilotなど、AIを活用した開発ツールが急速に普及。
					コーディング、デバッグ、ドキュメント作成の効率が劇的に向上しています。
				</p>
				<div class="grid md:grid-cols-3 gap-3">
					<div class="bg-white dark:bg-gray-800 p-3 rounded">
						<p class="font-semibold text-sm text-gray-800 dark:text-gray-200">Claude Code</p>
						<p class="text-xs text-gray-600 dark:text-gray-400">CLIでのAI開発支援</p>
					</div>
					<div class="bg-white dark:bg-gray-800 p-3 rounded">
						<p class="font-semibold text-sm text-gray-800 dark:text-gray-200">Cursor</p>
						<p class="text-xs text-gray-600 dark:text-gray-400">AI統合エディタ</p>
					</div>
					<div class="bg-white dark:bg-gray-800 p-3 rounded">
						<p class="font-semibold text-sm text-gray-800 dark:text-gray-200">GitHub Copilot</p>
						<p class="text-xs text-gray-600 dark:text-gray-400">コード補完AI</p>
					</div>
				</div>
			</div>
		</div>
	</section>

	<!-- このサイトで学べること -->
	<section class="mb-12">
		<h2 id="what-you-learn" class="text-xl font-bold mb-4">このサイトで学べること</h2>

		<div class="grid md:grid-cols-2 gap-4">
			<div class="p-4 rounded-lg border border-gray-200 dark:border-gray-700">
				<p class="font-semibold text-gray-800 dark:text-gray-200 mb-2">基礎技術</p>
				<ul class="text-sm text-gray-600 dark:text-gray-400 space-y-1">
					<li>HTML - Webページの構造</li>
					<li>CSS - スタイリングとレイアウト</li>
					<li>JavaScript - 動的な処理</li>
					<li>TypeScript - 型安全な開発</li>
				</ul>
			</div>
			<div class="p-4 rounded-lg border border-gray-200 dark:border-gray-700">
				<p class="font-semibold text-gray-800 dark:text-gray-200 mb-2">モダンフレームワーク</p>
				<ul class="text-sm text-gray-600 dark:text-gray-400 space-y-1">
					<li>SvelteKit - フルスタック開発</li>
					<li>Next.js - React ベース開発</li>
					<li>Tailwind CSS - ユーティリティCSS</li>
				</ul>
			</div>
			<div class="p-4 rounded-lg border border-gray-200 dark:border-gray-700">
				<p class="font-semibold text-gray-800 dark:text-gray-200 mb-2">バックエンド・データベース</p>
				<ul class="text-sm text-gray-600 dark:text-gray-400 space-y-1">
					<li>Supabase - BaaS（認証・DB）</li>
					<li>Cloudflare D1 - エッジDB</li>
					<li>APIエンドポイント設計</li>
				</ul>
			</div>
			<div class="p-4 rounded-lg border border-gray-200 dark:border-gray-700">
				<p class="font-semibold text-gray-800 dark:text-gray-200 mb-2">開発の考え方</p>
				<ul class="text-sm text-gray-600 dark:text-gray-400 space-y-1">
					<li>オブジェクト指向プログラミング</li>
					<li>状態管理</li>
					<li>非同期処理</li>
				</ul>
			</div>
		</div>
	</section>

	<!-- 学習の進め方 -->
	<section class="mb-10">
		<h2 id="how-to-learn" class="text-xl font-bold mb-4">おすすめの学習順序</h2>

		<div class="space-y-3">
			<div class="flex items-center gap-4 p-4 rounded-lg bg-gray-50 dark:bg-gray-800">
				<span class="w-10 h-10 bg-orange-500 text-white rounded-full flex items-center justify-center font-bold">1</span>
				<div>
					<p class="font-semibold text-gray-800 dark:text-gray-200">HTML → CSS → JavaScript</p>
					<p class="text-sm text-gray-600 dark:text-gray-400">Webの基礎を固める</p>
				</div>
			</div>
			<div class="flex items-center gap-4 p-4 rounded-lg bg-gray-50 dark:bg-gray-800">
				<span class="w-10 h-10 bg-blue-500 text-white rounded-full flex items-center justify-center font-bold">2</span>
				<div>
					<p class="font-semibold text-gray-800 dark:text-gray-200">TypeScript</p>
					<p class="text-sm text-gray-600 dark:text-gray-400">型安全な開発を学ぶ</p>
				</div>
			</div>
			<div class="flex items-center gap-4 p-4 rounded-lg bg-gray-50 dark:bg-gray-800">
				<span class="w-10 h-10 bg-cyan-500 text-white rounded-full flex items-center justify-center font-bold">3</span>
				<div>
					<p class="font-semibold text-gray-800 dark:text-gray-200">Tailwind CSS</p>
					<p class="text-sm text-gray-600 dark:text-gray-400">効率的なスタイリング</p>
				</div>
			</div>
			<div class="flex items-center gap-4 p-4 rounded-lg bg-gray-50 dark:bg-gray-800">
				<span class="w-10 h-10 bg-orange-600 text-white rounded-full flex items-center justify-center font-bold">4</span>
				<div>
					<p class="font-semibold text-gray-800 dark:text-gray-200">SvelteKit（Svelte + Vite）</p>
					<p class="text-sm text-gray-600 dark:text-gray-400">フルスタック開発の実践</p>
				</div>
			</div>
			<div class="flex items-center gap-4 p-4 rounded-lg bg-gray-50 dark:bg-gray-800">
				<span class="w-10 h-10 bg-green-500 text-white rounded-full flex items-center justify-center font-bold">5</span>
				<div>
					<p class="font-semibold text-gray-800 dark:text-gray-200">Supabase / Cloudflare D1</p>
					<p class="text-sm text-gray-600 dark:text-gray-400">データベース連携</p>
				</div>
			</div>
		</div>
	</section>

	<!-- ナビゲーション -->
	<div class="flex justify-between pt-6 border-t border-gray-200 dark:border-gray-700">
		<span></span>
		<a href="/profile" class="inline-flex items-center gap-2 px-4 py-2 rounded-lg bg-primary-600 text-white hover:bg-primary-700 transition-colors">
			次へ：著者について
			<svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
				<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 5l7 7-7 7" />
			</svg>
		</a>
	</div>
</article>
