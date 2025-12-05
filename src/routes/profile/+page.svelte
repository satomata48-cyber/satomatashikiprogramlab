<script>
</script>

<svelte:head>
	<title>著者について | さとまたラボ</title>
</svelte:head>

<article>
	<h1 class="text-3xl font-bold mb-2">著者について</h1>
	<p class="text-lg text-gray-600 dark:text-gray-400 mb-8">
		このサイトを運営している開発者のプロフィール
	</p>

	<!-- 基本情報 -->
	<section class="mb-12">
		<h2 id="basic" class="text-xl font-bold mb-4">基本情報</h2>

		<div class="p-6 rounded-xl bg-gradient-to-r from-blue-50 to-purple-50 dark:from-blue-900/20 dark:to-purple-900/20 border border-blue-200 dark:border-blue-800">
			<div class="grid md:grid-cols-2 gap-4">
				<div class="space-y-3">
					<div class="flex items-center gap-3">
						<span class="text-gray-500 dark:text-gray-400 w-32">プログラミング歴</span>
						<span class="font-semibold text-gray-800 dark:text-gray-200">10年（2015年〜）</span>
					</div>
					<div class="flex items-center gap-3">
						<span class="text-gray-500 dark:text-gray-400 w-32">開発スタイル</span>
						<span class="font-semibold text-gray-800 dark:text-gray-200">個人開発・フルスタック</span>
					</div>
				</div>
				<div class="space-y-3">
					<div class="flex items-center gap-3">
						<span class="text-gray-500 dark:text-gray-400 w-32">専門分野</span>
						<span class="font-semibold text-gray-800 dark:text-gray-200">モダンWebアプリ開発</span>
					</div>
					<div class="flex items-center gap-3">
						<span class="text-gray-500 dark:text-gray-400 w-32">最新技術</span>
						<span class="font-semibold text-gray-800 dark:text-gray-200">AI活用開発</span>
					</div>
				</div>
			</div>
		</div>
	</section>

	<!-- 強み・特徴 -->
	<section class="mb-12">
		<h2 id="strengths" class="text-xl font-bold mb-4">強み・特徴</h2>

		<div class="space-y-4">
			<div class="p-5 rounded-xl bg-orange-50 dark:bg-orange-900/20 border border-orange-200 dark:border-orange-800">
				<div class="flex items-start gap-3">
					<span class="text-2xl">1</span>
					<div>
						<p class="font-semibold text-orange-800 dark:text-orange-200">最新技術スタックでの高速開発</p>
						<p class="text-sm text-orange-700 dark:text-orange-300 mt-2">
							<strong>SvelteKit + Cloudflare D1</strong> を活用した超高速・低コストなアプリケーション開発。
							<strong>AI駆動開発</strong>（Claude Code, Cursor）による効率的な実装。
							JAMStackアーキテクチャによるスケーラブルなシステム設計。
						</p>
					</div>
				</div>
			</div>

			<div class="p-5 rounded-xl bg-blue-50 dark:bg-blue-900/20 border border-blue-200 dark:border-blue-800">
				<div class="flex items-start gap-3">
					<span class="text-2xl">2</span>
					<div>
						<p class="font-semibold text-blue-800 dark:text-blue-200">実践的なビジネスアプリケーション経験</p>
						<p class="text-sm text-blue-700 dark:text-blue-300 mt-2">
							マーケティングシステム、イーラーニングプラットフォーム等の業務システム開発。
							Stripe決済統合による収益化実装。
							Supabase/GCP認証による会員制サイト構築。
						</p>
					</div>
				</div>
			</div>

			<div class="p-5 rounded-xl bg-green-50 dark:bg-green-900/20 border border-green-200 dark:border-green-800">
				<div class="flex items-start gap-3">
					<span class="text-2xl">3</span>
					<div>
						<p class="font-semibold text-green-800 dark:text-green-200">短期間での技術習得力</p>
						<p class="text-sm text-green-700 dark:text-green-300 mt-2">
							SvelteKitをわずか<strong>5ヶ月で10個以上</strong>のアプリケーションを開発。
							常に最新技術をキャッチアップし、実践投入。
						</p>
					</div>
				</div>
			</div>
		</div>
	</section>

	<!-- 開発実績 -->
	<section class="mb-12">
		<h2 id="projects" class="text-xl font-bold mb-4">開発実績</h2>

		<!-- SvelteKit時代 -->
		<div class="mb-8">
			<h3 class="text-lg font-semibold mb-4 flex items-center gap-2">
				<span class="px-3 py-1 bg-orange-500 text-white rounded-full text-sm">2024年〜現在</span>
				SvelteKit時代
			</h3>

			<div class="grid md:grid-cols-2 gap-4">
				<div class="p-4 rounded-lg border border-gray-200 dark:border-gray-700 hover:border-orange-300 dark:hover:border-orange-700 transition-colors">
					<p class="font-semibold text-gray-800 dark:text-gray-200 mb-2">マーケティングシステム</p>
					<div class="flex flex-wrap gap-1 mb-2">
						<span class="px-2 py-0.5 bg-orange-100 dark:bg-orange-900 text-orange-700 dark:text-orange-300 rounded text-xs">SvelteKit</span>
						<span class="px-2 py-0.5 bg-orange-100 dark:bg-orange-900 text-orange-700 dark:text-orange-300 rounded text-xs">Cloudflare D1</span>
						<span class="px-2 py-0.5 bg-orange-100 dark:bg-orange-900 text-orange-700 dark:text-orange-300 rounded text-xs">Tailwind</span>
					</div>
					<p class="text-sm text-gray-600 dark:text-gray-400">
						顧客管理、キャンペーン管理、分析ダッシュボード。完全サーバーレス、月額コストほぼゼロ。
					</p>
				</div>

				<div class="p-4 rounded-lg border border-gray-200 dark:border-gray-700 hover:border-green-300 dark:hover:border-green-700 transition-colors">
					<p class="font-semibold text-gray-800 dark:text-gray-200 mb-2">イーラーニングプラットフォーム</p>
					<div class="flex flex-wrap gap-1 mb-2">
						<span class="px-2 py-0.5 bg-green-100 dark:bg-green-900 text-green-700 dark:text-green-300 rounded text-xs">SvelteKit</span>
						<span class="px-2 py-0.5 bg-green-100 dark:bg-green-900 text-green-700 dark:text-green-300 rounded text-xs">Supabase</span>
						<span class="px-2 py-0.5 bg-green-100 dark:bg-green-900 text-green-700 dark:text-green-300 rounded text-xs">Stripe</span>
					</div>
					<p class="text-sm text-gray-600 dark:text-gray-400">
						コース管理、動画配信、決済システム、進捗管理。会員制、サブスクリプション対応。
					</p>
				</div>

				<div class="p-4 rounded-lg border border-gray-200 dark:border-gray-700 hover:border-purple-300 dark:hover:border-purple-700 transition-colors">
					<p class="font-semibold text-gray-800 dark:text-gray-200 mb-2">AIチャットアプリケーション</p>
					<div class="flex flex-wrap gap-1 mb-2">
						<span class="px-2 py-0.5 bg-purple-100 dark:bg-purple-900 text-purple-700 dark:text-purple-300 rounded text-xs">SvelteKit</span>
						<span class="px-2 py-0.5 bg-purple-100 dark:bg-purple-900 text-purple-700 dark:text-purple-300 rounded text-xs">OpenRouter</span>
					</div>
					<p class="text-sm text-gray-600 dark:text-gray-400">
						複数AIモデル対応（GPT-4, Claude, Geminiなど）。ChatGPT風UI、マルチモデル切り替え。
					</p>
				</div>

				<div class="p-4 rounded-lg border border-gray-200 dark:border-gray-700 hover:border-blue-300 dark:hover:border-blue-700 transition-colors">
					<p class="font-semibold text-gray-800 dark:text-gray-200 mb-2">個人資産管理ソフト</p>
					<div class="flex flex-wrap gap-1 mb-2">
						<span class="px-2 py-0.5 bg-blue-100 dark:bg-blue-900 text-blue-700 dark:text-blue-300 rounded text-xs">SvelteKit</span>
						<span class="px-2 py-0.5 bg-blue-100 dark:bg-blue-900 text-blue-700 dark:text-blue-300 rounded text-xs">Cloudflare D1</span>
					</div>
					<p class="text-sm text-gray-600 dark:text-gray-400">
						収支管理、グラフ可視化、カテゴリ分類。プライバシー重視のローカルファースト設計。
					</p>
				</div>

				<div class="p-4 rounded-lg border border-gray-200 dark:border-gray-700 hover:border-cyan-300 dark:hover:border-cyan-700 transition-colors">
					<p class="font-semibold text-gray-800 dark:text-gray-200 mb-2">タスク管理アプリ（Trelloクローン）</p>
					<div class="flex flex-wrap gap-1 mb-2">
						<span class="px-2 py-0.5 bg-cyan-100 dark:bg-cyan-900 text-cyan-700 dark:text-cyan-300 rounded text-xs">SvelteKit</span>
						<span class="px-2 py-0.5 bg-cyan-100 dark:bg-cyan-900 text-cyan-700 dark:text-cyan-300 rounded text-xs">Supabase</span>
					</div>
					<p class="text-sm text-gray-600 dark:text-gray-400">
						ドラッグ&ドロップ、リアルタイム同期。レスポンシブデザイン、PWA対応。
					</p>
				</div>

				<div class="p-4 rounded-lg border border-gray-200 dark:border-gray-700 hover:border-amber-300 dark:hover:border-amber-700 transition-colors">
					<p class="font-semibold text-gray-800 dark:text-gray-200 mb-2">ニュースRSSリーダー</p>
					<div class="flex flex-wrap gap-1 mb-2">
						<span class="px-2 py-0.5 bg-amber-100 dark:bg-amber-900 text-amber-700 dark:text-amber-300 rounded text-xs">SvelteKit</span>
						<span class="px-2 py-0.5 bg-amber-100 dark:bg-amber-900 text-amber-700 dark:text-amber-300 rounded text-xs">RSS API</span>
					</div>
					<p class="text-sm text-gray-600 dark:text-gray-400">
						フィード購読、記事検索、お気に入り管理機能。
					</p>
				</div>
			</div>
		</div>

		<!-- 過去のプロジェクト -->
		<div class="mb-8">
			<h3 class="text-lg font-semibold mb-4 flex items-center gap-2">
				<span class="px-3 py-1 bg-gray-500 text-white rounded-full text-sm">2018〜2023年</span>
				Next.js時代
			</h3>
			<div class="p-4 rounded-lg bg-gray-50 dark:bg-gray-800">
				<p class="text-gray-700 dark:text-gray-300">
					複数の会員制サイト・Webアプリケーション開発。Next.js, GraphQL, Supabaseを活用。
				</p>
			</div>
		</div>

		<div>
			<h3 class="text-lg font-semibold mb-4 flex items-center gap-2">
				<span class="px-3 py-1 bg-gray-400 text-white rounded-full text-sm">2015〜2018年</span>
				Rails/Django学習期
			</h3>
			<div class="p-4 rounded-lg bg-gray-50 dark:bg-gray-800">
				<p class="text-gray-700 dark:text-gray-300">
					TrelloクローンやTwitterクローンを開発。CRUD操作、MVC設計の基礎を習得。AWS EC2でのデプロイ経験。
				</p>
			</div>
		</div>
	</section>

	<!-- 技術スタック -->
	<section class="mb-12">
		<h2 id="tech-stack" class="text-xl font-bold mb-4">技術スタック</h2>

		<!-- 言語 -->
		<div class="mb-6">
			<h3 class="text-lg font-semibold mb-3">言語</h3>
			<div class="grid md:grid-cols-2 gap-3">
				<div class="flex items-center gap-3 p-3 rounded-lg bg-gray-50 dark:bg-gray-800">
					<span class="font-medium w-28">JavaScript</span>
					<div class="flex gap-1">
						<span class="text-yellow-500">★★★★</span><span class="text-gray-300">☆</span>
					</div>
					<span class="text-xs text-gray-500">実務で多用</span>
				</div>
				<div class="flex items-center gap-3 p-3 rounded-lg bg-gray-50 dark:bg-gray-800">
					<span class="font-medium w-28">TypeScript</span>
					<div class="flex gap-1">
						<span class="text-blue-500">★★★★</span><span class="text-gray-300">☆</span>
					</div>
					<span class="text-xs text-gray-500">JS/TS両対応</span>
				</div>
				<div class="flex items-center gap-3 p-3 rounded-lg bg-gray-50 dark:bg-gray-800">
					<span class="font-medium w-28">Python</span>
					<div class="flex gap-1">
						<span class="text-green-500">★★★</span><span class="text-gray-300">☆☆</span>
					</div>
					<span class="text-xs text-gray-500">Django経験</span>
				</div>
				<div class="flex items-center gap-3 p-3 rounded-lg bg-gray-50 dark:bg-gray-800">
					<span class="font-medium w-28">HTML/CSS</span>
					<div class="flex gap-1">
						<span class="text-orange-500">★★★★</span><span class="text-gray-300">☆</span>
					</div>
					<span class="text-xs text-gray-500">実務レベル</span>
				</div>
			</div>
		</div>

		<!-- フロントエンド -->
		<div class="mb-6">
			<h3 class="text-lg font-semibold mb-3">フロントエンド</h3>
			<div class="grid md:grid-cols-3 gap-3">
				<div class="p-3 rounded-lg bg-orange-50 dark:bg-orange-900/20 border border-orange-200 dark:border-orange-800">
					<p class="font-semibold text-orange-800 dark:text-orange-200">SvelteKit</p>
					<div class="flex gap-1 my-1">
						<span class="text-orange-500">★★★★★</span>
					</div>
					<p class="text-xs text-orange-700 dark:text-orange-300">メイン技術（10+プロジェクト）</p>
				</div>
				<div class="p-3 rounded-lg bg-gray-50 dark:bg-gray-800">
					<p class="font-semibold text-gray-800 dark:text-gray-200">Next.js</p>
					<div class="flex gap-1 my-1">
						<span class="text-gray-600">★★★★</span><span class="text-gray-300">☆</span>
					</div>
					<p class="text-xs text-gray-600 dark:text-gray-400">複数アプリ開発実績</p>
				</div>
				<div class="p-3 rounded-lg bg-gray-50 dark:bg-gray-800">
					<p class="font-semibold text-gray-800 dark:text-gray-200">React</p>
					<div class="flex gap-1 my-1">
						<span class="text-gray-600">★★★</span><span class="text-gray-300">☆☆</span>
					</div>
					<p class="text-xs text-gray-600 dark:text-gray-400">基礎レベル</p>
				</div>
			</div>
		</div>

		<!-- データベース -->
		<div class="mb-6">
			<h3 class="text-lg font-semibold mb-3">データベース</h3>
			<div class="grid md:grid-cols-2 gap-3">
				<div class="p-3 rounded-lg bg-orange-50 dark:bg-orange-900/20 border border-orange-200 dark:border-orange-800">
					<p class="font-semibold text-orange-800 dark:text-orange-200">Cloudflare D1</p>
					<div class="flex gap-1 my-1">
						<span class="text-orange-500">★★★★★</span>
					</div>
					<p class="text-xs text-orange-700 dark:text-orange-300">メインDB（使用率90%）</p>
				</div>
				<div class="p-3 rounded-lg bg-green-50 dark:bg-green-900/20 border border-green-200 dark:border-green-800">
					<p class="font-semibold text-green-800 dark:text-green-200">Supabase</p>
					<div class="flex gap-1 my-1">
						<span class="text-green-500">★★★★</span><span class="text-gray-300">☆</span>
					</div>
					<p class="text-xs text-green-700 dark:text-green-300">認証・リアルタイム機能で使用</p>
				</div>
			</div>
		</div>

		<!-- インフラ -->
		<div class="mb-6">
			<h3 class="text-lg font-semibold mb-3">インフラ・デプロイ</h3>
			<div class="flex flex-wrap gap-2">
				<span class="px-3 py-1.5 bg-orange-100 dark:bg-orange-900 text-orange-700 dark:text-orange-300 rounded-lg text-sm font-medium">Cloudflare Pages（メイン）</span>
				<span class="px-3 py-1.5 bg-gray-100 dark:bg-gray-800 text-gray-700 dark:text-gray-300 rounded-lg text-sm">Vercel</span>
				<span class="px-3 py-1.5 bg-gray-100 dark:bg-gray-800 text-gray-700 dark:text-gray-300 rounded-lg text-sm">Git / GitHub</span>
			</div>
		</div>

		<!-- 開発ツール -->
		<div>
			<h3 class="text-lg font-semibold mb-3">開発ツール</h3>
			<div class="flex flex-wrap gap-2">
				<span class="px-3 py-1.5 bg-purple-100 dark:bg-purple-900 text-purple-700 dark:text-purple-300 rounded-lg text-sm font-medium">Cursor（メインエディタ）</span>
				<span class="px-3 py-1.5 bg-purple-100 dark:bg-purple-900 text-purple-700 dark:text-purple-300 rounded-lg text-sm font-medium">Claude Code</span>
				<span class="px-3 py-1.5 bg-gray-100 dark:bg-gray-800 text-gray-700 dark:text-gray-300 rounded-lg text-sm">VS Code</span>
			</div>
		</div>
	</section>

	<!-- キャリア -->
	<section class="mb-12">
		<h2 id="career" class="text-xl font-bold mb-4">キャリア</h2>

		<div class="relative">
			<!-- タイムライン -->
			<div class="absolute left-4 top-0 bottom-0 w-0.5 bg-gray-200 dark:bg-gray-700"></div>

			<div class="space-y-6">
				<div class="relative pl-12">
					<div class="absolute left-2 w-5 h-5 bg-orange-500 rounded-full border-4 border-white dark:border-gray-900"></div>
					<div class="p-4 rounded-lg bg-orange-50 dark:bg-orange-900/20 border border-orange-200 dark:border-orange-800">
						<p class="font-semibold text-orange-800 dark:text-orange-200">2024年〜現在：SvelteKit集中期</p>
						<p class="text-sm text-orange-700 dark:text-orange-300 mt-1">
							5ヶ月で10+アプリケーション開発。Next.jsでのClaude Code開発時のエラー頻発・複雑化を解決。
							開発速度・保守性の大幅向上を実現。
						</p>
					</div>
				</div>

				<div class="relative pl-12">
					<div class="absolute left-2 w-5 h-5 bg-gray-400 rounded-full border-4 border-white dark:border-gray-900"></div>
					<div class="p-4 rounded-lg bg-gray-50 dark:bg-gray-800">
						<p class="font-semibold text-gray-800 dark:text-gray-200">2018〜2023年：Next.js/React期</p>
						<p class="text-sm text-gray-600 dark:text-gray-400 mt-1">
							複数の会員制サイト・Webアプリケーション開発。JAMStack、サーバーレス、GraphQLを習得。
						</p>
					</div>
				</div>

				<div class="relative pl-12">
					<div class="absolute left-2 w-5 h-5 bg-gray-300 rounded-full border-4 border-white dark:border-gray-900"></div>
					<div class="p-4 rounded-lg bg-gray-50 dark:bg-gray-800">
						<p class="font-semibold text-gray-800 dark:text-gray-200">2015〜2018年：Rails/Django学習期</p>
						<p class="text-sm text-gray-600 dark:text-gray-400 mt-1">
							CRUD操作・MVC設計の習得。クローンアプリ開発・AWS EC2デプロイ経験。
						</p>
					</div>
				</div>

				<div class="relative pl-12">
					<div class="absolute left-2 w-5 h-5 bg-blue-500 rounded-full border-4 border-white dark:border-gray-900"></div>
					<div class="p-4 rounded-lg bg-blue-50 dark:bg-blue-900/20 border border-blue-200 dark:border-blue-800">
						<p class="font-semibold text-blue-800 dark:text-blue-200">2015年：プログラミング開始</p>
						<p class="text-sm text-blue-700 dark:text-blue-300 mt-1">
							25歳でプログラミングを始める。現在10年目。
						</p>
					</div>
				</div>
			</div>
		</div>
	</section>

	<!-- 開発哲学 -->
	<section class="mb-12">
		<h2 id="philosophy" class="text-xl font-bold mb-4">開発哲学</h2>

		<div class="grid md:grid-cols-2 gap-4">
			<div class="p-4 rounded-lg bg-blue-50 dark:bg-blue-900/20 border border-blue-200 dark:border-blue-800">
				<p class="font-semibold text-blue-800 dark:text-blue-200 mb-2">スピード重視</p>
				<p class="text-sm text-blue-700 dark:text-blue-300">
					AI駆動開発による高速プロトタイピング。モダンツールによる効率的な実装。
				</p>
			</div>
			<div class="p-4 rounded-lg bg-green-50 dark:bg-green-900/20 border border-green-200 dark:border-green-800">
				<p class="font-semibold text-green-800 dark:text-green-200 mb-2">コスト最適化</p>
				<p class="text-sm text-green-700 dark:text-green-300">
					Cloudflare D1/Pagesによるほぼゼロコストインフラ。サーバーレスアーキテクチャの活用。
				</p>
			</div>
			<div class="p-4 rounded-lg bg-purple-50 dark:bg-purple-900/20 border border-purple-200 dark:border-purple-800">
				<p class="font-semibold text-purple-800 dark:text-purple-200 mb-2">継続的学習</p>
				<p class="text-sm text-purple-700 dark:text-purple-300">
					常に最新技術をキャッチアップ。実践を通じた技術習得（SvelteKit 5ヶ月で10+アプリ）。
				</p>
			</div>
			<div class="p-4 rounded-lg bg-amber-50 dark:bg-amber-900/20 border border-amber-200 dark:border-amber-800">
				<p class="font-semibold text-amber-800 dark:text-amber-200 mb-2">実用性重視</p>
				<p class="text-sm text-amber-700 dark:text-amber-300">
					ビジネス価値を生む実装。保守性・拡張性を考慮した設計。
				</p>
			</div>
		</div>
	</section>

	<!-- キーワード -->
	<section class="mb-10">
		<h2 id="keywords" class="text-xl font-bold mb-4">キーワード</h2>

		<div class="flex flex-wrap gap-2">
			<span class="px-3 py-1 bg-orange-100 dark:bg-orange-900 text-orange-700 dark:text-orange-300 rounded-full text-sm">SvelteKit</span>
			<span class="px-3 py-1 bg-gray-100 dark:bg-gray-800 text-gray-700 dark:text-gray-300 rounded-full text-sm">Next.js</span>
			<span class="px-3 py-1 bg-orange-100 dark:bg-orange-900 text-orange-700 dark:text-orange-300 rounded-full text-sm">Cloudflare D1</span>
			<span class="px-3 py-1 bg-green-100 dark:bg-green-900 text-green-700 dark:text-green-300 rounded-full text-sm">Supabase</span>
			<span class="px-3 py-1 bg-cyan-100 dark:bg-cyan-900 text-cyan-700 dark:text-cyan-300 rounded-full text-sm">Tailwind CSS</span>
			<span class="px-3 py-1 bg-purple-100 dark:bg-purple-900 text-purple-700 dark:text-purple-300 rounded-full text-sm">Stripe</span>
			<span class="px-3 py-1 bg-pink-100 dark:bg-pink-900 text-pink-700 dark:text-pink-300 rounded-full text-sm">AI統合</span>
			<span class="px-3 py-1 bg-blue-100 dark:bg-blue-900 text-blue-700 dark:text-blue-300 rounded-full text-sm">JAMStack</span>
			<span class="px-3 py-1 bg-indigo-100 dark:bg-indigo-900 text-indigo-700 dark:text-indigo-300 rounded-full text-sm">サーバーレス</span>
			<span class="px-3 py-1 bg-yellow-100 dark:bg-yellow-900 text-yellow-700 dark:text-yellow-300 rounded-full text-sm">フルスタック</span>
			<span class="px-3 py-1 bg-red-100 dark:bg-red-900 text-red-700 dark:text-red-300 rounded-full text-sm">個人開発</span>
			<span class="px-3 py-1 bg-purple-100 dark:bg-purple-900 text-purple-700 dark:text-purple-300 rounded-full text-sm">Claude Code</span>
			<span class="px-3 py-1 bg-purple-100 dark:bg-purple-900 text-purple-700 dark:text-purple-300 rounded-full text-sm">Cursor</span>
		</div>
	</section>

	<!-- ナビゲーション -->
	<div class="flex justify-between pt-6 border-t border-gray-200 dark:border-gray-700">
		<a href="/intro" class="inline-flex items-center gap-2 px-4 py-2 rounded-lg border border-gray-300 dark:border-gray-600 hover:bg-gray-100 dark:hover:bg-gray-800 transition-colors">
			<svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
				<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 19l-7-7 7-7" />
			</svg>
			前へ：はじめに
		</a>
		<a href="/html/basics" class="inline-flex items-center gap-2 px-4 py-2 rounded-lg bg-primary-600 text-white hover:bg-primary-700 transition-colors">
			次へ：HTML基本構造
			<svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
				<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 5l7 7-7 7" />
			</svg>
		</a>
	</div>
</article>
