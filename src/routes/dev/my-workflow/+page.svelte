<script>
	import CodePreview from '$lib/components/CodePreview.svelte';
</script>

<svelte:head>
	<title>私の開発フロー | さとまたラボ</title>
</svelte:head>

<article>
	<h1 class="text-3xl font-bold mb-2">私の開発フロー</h1>
	<p class="text-lg text-gray-600 dark:text-gray-400 mb-8">
		個人開発で使っているシンプルで高速な開発手法
	</p>

	<!-- 概要 -->
	<section class="mb-12">
		<h2 id="overview" class="text-xl font-bold mb-4">開発スタイルの特徴</h2>

		<div class="p-6 rounded-xl bg-gradient-to-r from-orange-50 to-purple-50 dark:from-orange-900/20 dark:to-purple-900/20 border border-orange-200 dark:border-orange-800 mb-6">
			<p class="text-lg text-orange-800 dark:text-orange-200 mb-4">
				<strong>バイブコーディング</strong> × <strong>AI駆動開発</strong>
			</p>
			<p class="text-sm text-orange-700 dark:text-orange-300">
				自分でコードを打たず、Claude Codeに要件を伝えて開発する手法。
				高速なプロトタイピングと、低コストな運用を実現。
			</p>
		</div>

		<div class="grid md:grid-cols-3 gap-4">
			<div class="p-4 rounded-lg bg-orange-50 dark:bg-orange-900/20 border border-orange-200 dark:border-orange-800">
				<p class="font-semibold text-orange-800 dark:text-orange-200 mb-2">SvelteKit</p>
				<p class="text-sm text-orange-700 dark:text-orange-300">
					フルスタックフレームワーク。シンプルで高速。
				</p>
			</div>
			<div class="p-4 rounded-lg bg-cyan-50 dark:bg-cyan-900/20 border border-cyan-200 dark:border-cyan-800">
				<p class="font-semibold text-cyan-800 dark:text-cyan-200 mb-2">Tailwind CSS</p>
				<p class="text-sm text-cyan-700 dark:text-cyan-300">
					ユーティリティファースト。デザインが高速に。
				</p>
			</div>
			<div class="p-4 rounded-lg bg-blue-50 dark:bg-blue-900/20 border border-blue-200 dark:border-blue-800">
				<p class="font-semibold text-blue-800 dark:text-blue-200 mb-2">Cloudflare D1</p>
				<p class="text-sm text-blue-700 dark:text-blue-300">
					エッジDB。超高速・ほぼ無料。
				</p>
			</div>
		</div>
	</section>

	<!-- 開発フロー全体 -->
	<section class="mb-12">
		<h2 id="full-flow" class="text-xl font-bold mb-4">開発フロー全体像</h2>

		<div class="p-4 rounded-lg bg-gray-50 dark:bg-gray-800 mb-6">
			<div class="flex flex-col md:flex-row md:items-center md:justify-center gap-2 md:gap-4 text-sm">
				<div class="px-4 py-3 bg-purple-500 text-white rounded-lg text-center">
					<div class="font-bold">1. フォルダ作成</div>
					<div class="text-xs opacity-80">ローカル</div>
				</div>
				<span class="hidden md:block text-gray-400 text-2xl">→</span>
				<div class="px-4 py-3 bg-blue-500 text-white rounded-lg text-center">
					<div class="font-bold">2. 要件定義</div>
					<div class="text-xs opacity-80">Claude Code</div>
				</div>
				<span class="hidden md:block text-gray-400 text-2xl">→</span>
				<div class="px-4 py-3 bg-orange-500 text-white rounded-lg text-center">
					<div class="font-bold">3. 開発</div>
					<div class="text-xs opacity-80">バイブコーディング</div>
				</div>
				<span class="hidden md:block text-gray-400 text-2xl">→</span>
				<div class="px-4 py-3 bg-gray-700 text-white rounded-lg text-center">
					<div class="font-bold">4. Git保存</div>
					<div class="text-xs opacity-80">セーブポイント</div>
				</div>
				<span class="hidden md:block text-gray-400 text-2xl">→</span>
				<div class="px-4 py-3 bg-green-500 text-white rounded-lg text-center">
					<div class="font-bold">5. デプロイ</div>
					<div class="text-xs opacity-80">Cloudflare</div>
				</div>
			</div>
		</div>
	</section>

	<!-- Step 1: プロジェクト作成 -->
	<section class="mb-12">
		<h2 id="step1" class="text-xl font-bold mb-4">
			<span class="inline-flex items-center justify-center w-8 h-8 bg-purple-500 text-white rounded-full mr-2 text-sm">1</span>
			プロジェクト作成
		</h2>

		<p class="text-gray-700 dark:text-gray-300 mb-4">
			まずはローカルにフォルダを作成し、SvelteKitプロジェクトをセットアップします。
		</p>

		<CodePreview
			title="プロジェクトの初期化"
			description="ターミナルで実行"
			language="bash"
			code={`# 1. プロジェクトフォルダを作成
mkdir my-new-app
cd my-new-app

# 2. SvelteKitプロジェクトを作成
npx sv create .
# → Skeleton project を選択
# → TypeScript を選択
# → Tailwind CSS を追加

# 3. 依存関係をインストール
npm install

# 4. Cloudflare D1用のアダプターをインストール
npm install -D @sveltejs/adapter-cloudflare

# 5. 開発サーバーを起動して確認
npm run dev`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div style="color:#6a9955;">// これで準備完了！</div><div style="color:#6a9955;">// http://localhost:5173 で確認</div></div>`}
		/>

		<div class="mt-4 p-4 rounded-lg bg-amber-50 dark:bg-amber-900/20 border border-amber-200 dark:border-amber-800">
			<p class="font-semibold text-amber-800 dark:text-amber-200 mb-2">ポイント</p>
			<p class="text-sm text-amber-700 dark:text-amber-300">
				この時点ではまだGitは初期化しません。
				ある程度動くものができてからGitに保存（セーブ）します。
			</p>
		</div>
	</section>

	<!-- Step 2: 要件定義 -->
	<section class="mb-12">
		<h2 id="step2" class="text-xl font-bold mb-4">
			<span class="inline-flex items-center justify-center w-8 h-8 bg-blue-500 text-white rounded-full mr-2 text-sm">2</span>
			Claude Codeで要件定義
		</h2>

		<p class="text-gray-700 dark:text-gray-300 mb-4">
			作りたいアプリの要件をClaude Codeに伝えます。
			具体的であるほど、良いコードが生成されます。
		</p>

		<CodePreview
			title="Claude Codeへの指示例"
			description="要件を明確に伝える"
			language="text"
			code={`# 悪い例（曖昧）
「Todoアプリを作って」

# 良い例（具体的）
「SvelteKit + Cloudflare D1 + Tailwind CSSで
Todoアプリを作成してください。

機能要件：
- Todoの追加・編集・削除
- 完了/未完了の切り替え
- カテゴリ分類（仕事、プライベート、買い物）
- 期限の設定と期限切れの表示

技術要件：
- +page.server.ts でサーバーサイド処理
- Form Actions で CRUD 操作
- wrangler.toml に D1 の設定
- レスポンシブデザイン

ファイル構成：
- src/routes/+page.svelte
- src/routes/+page.server.ts
- src/lib/components/TodoItem.svelte
- schema.sql`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div style="color:#6a9955;">// 具体的に伝えるほど</div><div style="color:#6a9955;">// 期待通りのコードが出力される</div></div>`}
		/>

		<div class="mt-4 p-4 rounded-lg bg-blue-50 dark:bg-blue-900/20 border border-blue-200 dark:border-blue-800">
			<p class="font-semibold text-blue-800 dark:text-blue-200 mb-2">Claude Codeの活用ポイント</p>
			<ul class="text-sm text-blue-700 dark:text-blue-300 space-y-1">
				<li>・使用する技術スタック（SvelteKit, D1, Tailwind）を明示</li>
				<li>・機能を箇条書きで列挙</li>
				<li>・ファイル構成を指定すると整理されたコードに</li>
				<li>・既存コードがあれば「〇〇を参考に」と伝える</li>
			</ul>
		</div>
	</section>

	<!-- Step 3: バイブコーディング -->
	<section class="mb-12">
		<h2 id="step3" class="text-xl font-bold mb-4">
			<span class="inline-flex items-center justify-center w-8 h-8 bg-orange-500 text-white rounded-full mr-2 text-sm">3</span>
			バイブコーディングで開発
		</h2>

		<div class="p-6 rounded-xl bg-orange-50 dark:bg-orange-900/20 border border-orange-200 dark:border-orange-800 mb-6">
			<p class="text-lg text-orange-800 dark:text-orange-200 mb-4">
				<strong>バイブコーディング</strong>とは？
			</p>
			<p class="text-sm text-orange-700 dark:text-orange-300">
				自分でコードを打たず、AIに指示を出して開発する手法。
				「こうしたい」という要望を言葉で伝え、AIがコードを生成。
				生成されたコードをレビューし、修正指示を出す。この繰り返し。
			</p>
		</div>

		<div class="space-y-4 mb-6">
			<div class="p-4 rounded-lg bg-gray-50 dark:bg-gray-800">
				<p class="font-semibold text-gray-800 dark:text-gray-200 mb-2">1. 機能を依頼</p>
				<p class="text-sm text-gray-600 dark:text-gray-400">
					「ログイン機能を追加して」「このボタンの色を変えて」など
				</p>
			</div>
			<div class="text-center text-gray-400">↓</div>
			<div class="p-4 rounded-lg bg-gray-50 dark:bg-gray-800">
				<p class="font-semibold text-gray-800 dark:text-gray-200 mb-2">2. AIがコードを生成</p>
				<p class="text-sm text-gray-600 dark:text-gray-400">
					Claude Codeがファイルを作成・編集
				</p>
			</div>
			<div class="text-center text-gray-400">↓</div>
			<div class="p-4 rounded-lg bg-gray-50 dark:bg-gray-800">
				<p class="font-semibold text-gray-800 dark:text-gray-200 mb-2">3. ブラウザで確認</p>
				<p class="text-sm text-gray-600 dark:text-gray-400">
					npm run dev で動作確認。問題があれば修正を依頼
				</p>
			</div>
			<div class="text-center text-gray-400">↓</div>
			<div class="p-4 rounded-lg bg-gray-50 dark:bg-gray-800">
				<p class="font-semibold text-gray-800 dark:text-gray-200 mb-2">4. 繰り返し</p>
				<p class="text-sm text-gray-600 dark:text-gray-400">
					満足するまで1〜3を繰り返す
				</p>
			</div>
		</div>

		<div class="p-4 rounded-lg bg-green-50 dark:bg-green-900/20 border border-green-200 dark:border-green-800">
			<p class="font-semibold text-green-800 dark:text-green-200 mb-2">D1の開発時</p>
			<p class="text-sm text-green-700 dark:text-green-300">
				D1を使う場合は <code class="bg-green-200 dark:bg-green-700 px-1 rounded">npm run dev</code> ではなく、
				wranglerでローカルD1を使うため以下を使用：
			</p>
			<code class="block mt-2 bg-gray-800 text-green-400 p-2 rounded text-sm">
				npm run build && wrangler pages dev .svelte-kit/cloudflare
			</code>
		</div>
	</section>

	<!-- Step 4: Git保存 -->
	<section class="mb-12">
		<h2 id="step4" class="text-xl font-bold mb-4">
			<span class="inline-flex items-center justify-center w-8 h-8 bg-gray-700 text-white rounded-full mr-2 text-sm">4</span>
			GitHubに保存（セーブポイント）
		</h2>

		<p class="text-gray-700 dark:text-gray-300 mb-4">
			ある程度動くものができたら、GitHubにプッシュして保存します。
			これがセーブポイントになり、いつでも戻れます。
		</p>

		<CodePreview
			title="GitHubへの保存"
			description="初回セットアップ"
			language="bash"
			code={`# 1. Gitを初期化
git init

# 2. 全ファイルをステージング
git add .

# 3. 最初のコミット
git commit -m "feat: 初期セットアップ完了"

# 4. GitHubでリポジトリを作成後、リモートを追加
git remote add origin https://github.com/username/my-new-app.git

# 5. プッシュ
git push -u origin main`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div style="color:#6a9955;">// これでセーブ完了！</div><div style="color:#6a9955;">// いつでもこの状態に戻れる</div></div>`}
		/>

		<div class="mt-4 p-4 rounded-lg bg-purple-50 dark:bg-purple-900/20 border border-purple-200 dark:border-purple-800">
			<p class="font-semibold text-purple-800 dark:text-purple-200 mb-2">この時点でやること</p>
			<ul class="text-sm text-purple-700 dark:text-purple-300 space-y-1">
				<li>・GitHubにリポジトリを作成</li>
				<li>・Cloudflare Pagesでプロジェクトを作成</li>
				<li>・GitHubリポジトリと連携</li>
				<li>・環境変数（D1のbindingなど）を設定</li>
			</ul>
		</div>
	</section>

	<!-- Step 5: デプロイ -->
	<section class="mb-12">
		<h2 id="step5" class="text-xl font-bold mb-4">
			<span class="inline-flex items-center justify-center w-8 h-8 bg-green-500 text-white rounded-full mr-2 text-sm">5</span>
			Cloudflareにデプロイ
		</h2>

		<p class="text-gray-700 dark:text-gray-300 mb-4">
			ローカルで問題なければ、GitHubにプッシュするだけで自動デプロイ。
		</p>

		<CodePreview
			title="デプロイの流れ"
			description="GitHubプッシュで自動"
			language="bash"
			code={`# ローカルで変更をコミット
git add .
git commit -m "feat: 新機能を追加"

# プッシュすると自動でCloudflareにデプロイ
git push origin main

# Cloudflare Pagesのダッシュボードでデプロイ状況を確認
# 数分で本番環境に反映される`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div style="color:#4ec9b0;">git push → 自動ビルド → 自動デプロイ</div></div>`}
		/>

		<div class="mt-6 grid md:grid-cols-2 gap-4">
			<div class="p-4 rounded-lg bg-blue-50 dark:bg-blue-900/20 border border-blue-200 dark:border-blue-800">
				<p class="font-semibold text-blue-800 dark:text-blue-200 mb-2">本番D1への初回適用</p>
				<p class="text-sm text-blue-700 dark:text-blue-300 mb-2">
					本番のD1データベースにスキーマを適用：
				</p>
				<code class="block bg-gray-800 text-blue-400 p-2 rounded text-xs">
					wrangler d1 execute my-db --remote --file=./schema.sql
				</code>
			</div>
			<div class="p-4 rounded-lg bg-orange-50 dark:bg-orange-900/20 border border-orange-200 dark:border-orange-800">
				<p class="font-semibold text-orange-800 dark:text-orange-200 mb-2">プレビューURL</p>
				<p class="text-sm text-orange-700 dark:text-orange-300">
					mainブランチ以外にプッシュすると、プレビューURLが発行される。
					本番に影響を与えずにテスト可能。
				</p>
			</div>
		</div>
	</section>

	<!-- エラー対応 -->
	<section class="mb-12">
		<h2 id="error-handling" class="text-xl font-bold mb-4">本番エラーの対応</h2>

		<p class="text-gray-700 dark:text-gray-300 mb-4">
			本番でエラーが発生した場合の対応フローです。
		</p>

		<div class="p-4 rounded-lg bg-red-50 dark:bg-red-900/20 border border-red-200 dark:border-red-800 mb-6">
			<div class="flex flex-col md:flex-row md:items-center md:justify-center gap-2 md:gap-4 text-sm">
				<div class="px-3 py-2 bg-red-500 text-white rounded text-center">
					本番でエラー発見
				</div>
				<span class="hidden md:block text-gray-400">→</span>
				<div class="px-3 py-2 bg-blue-500 text-white rounded text-center">
					ローカルで再現
				</div>
				<span class="hidden md:block text-gray-400">→</span>
				<div class="px-3 py-2 bg-purple-500 text-white rounded text-center">
					Claude Codeで修正
				</div>
				<span class="hidden md:block text-gray-400">→</span>
				<div class="px-3 py-2 bg-green-500 text-white rounded text-center">
					プッシュして確認
				</div>
			</div>
		</div>

		<CodePreview
			title="エラー修正の依頼例"
			description="Claude Codeへの指示"
			language="text"
			code={`本番で以下のエラーが発生しています：

エラーメッセージ：
"TypeError: Cannot read properties of undefined"

発生場所：
/dashboard ページを開いたとき

再現手順：
1. ログイン
2. ダッシュボードに移動
3. データがない状態だとエラー

原因を特定して修正してください。`}
		/>
	</section>

	<!-- メリット・デメリット -->
	<section class="mb-12">
		<h2 id="pros-cons" class="text-xl font-bold mb-4">この開発フローのメリット・デメリット</h2>

		<div class="grid md:grid-cols-2 gap-4">
			<div class="p-4 rounded-lg bg-green-50 dark:bg-green-900/20 border border-green-200 dark:border-green-800">
				<p class="font-semibold text-green-800 dark:text-green-200 mb-3">メリット</p>
				<ul class="text-sm text-green-700 dark:text-green-300 space-y-2">
					<li>・<strong>超高速開発</strong>：コードを打たないので速い</li>
					<li>・<strong>低コスト運用</strong>：Cloudflare無料枠で十分</li>
					<li>・<strong>シンプル</strong>：覚えることが少ない</li>
					<li>・<strong>セーブポイント</strong>：Gitでいつでも戻れる</li>
					<li>・<strong>自動デプロイ</strong>：プッシュだけで本番反映</li>
				</ul>
			</div>
			<div class="p-4 rounded-lg bg-red-50 dark:bg-red-900/20 border border-red-200 dark:border-red-800">
				<p class="font-semibold text-red-800 dark:text-red-200 mb-3">デメリット・注意点</p>
				<ul class="text-sm text-red-700 dark:text-red-300 space-y-2">
					<li>・<strong>テストなし</strong>：品質保証は手動確認のみ</li>
					<li>・<strong>チーム開発向きではない</strong>：レビューなし</li>
					<li>・<strong>AI依存</strong>：AIの出力を理解する必要あり</li>
					<li>・<strong>本番で確認</strong>：ステージング環境なし</li>
				</ul>
			</div>
		</div>

		<div class="mt-6 p-4 rounded-lg bg-amber-50 dark:bg-amber-900/20 border border-amber-200 dark:border-amber-800">
			<p class="font-semibold text-amber-800 dark:text-amber-200 mb-2">向いているプロジェクト</p>
			<p class="text-sm text-amber-700 dark:text-amber-300">
				・個人開発、サイドプロジェクト<br>
				・プロトタイプ、MVP開発<br>
				・小〜中規模のアプリケーション<br>
				・自分だけが使うツール
			</p>
		</div>
	</section>

	<!-- まとめ -->
	<section class="mb-10">
		<h2 id="summary" class="text-xl font-bold mb-4">まとめ</h2>

		<div class="space-y-4">
			<div class="p-4 rounded-lg bg-purple-50 dark:bg-purple-900/20 border border-purple-200 dark:border-purple-800">
				<p class="font-semibold text-purple-800 dark:text-purple-200">フォルダ作成 → 要件定義 → 開発 → Git保存 → デプロイ</p>
				<p class="text-sm text-purple-700 dark:text-purple-300">
					シンプルな5ステップで開発からデプロイまで完了。
				</p>
			</div>
			<div class="p-4 rounded-lg bg-blue-50 dark:bg-blue-900/20 border border-blue-200 dark:border-blue-800">
				<p class="font-semibold text-blue-800 dark:text-blue-200">バイブコーディング</p>
				<p class="text-sm text-blue-700 dark:text-blue-300">
					自分でコードを打たず、Claude Codeに指示を出して開発。
				</p>
			</div>
			<div class="p-4 rounded-lg bg-orange-50 dark:bg-orange-900/20 border border-orange-200 dark:border-orange-800">
				<p class="font-semibold text-orange-800 dark:text-orange-200">SvelteKit + D1 + Cloudflare</p>
				<p class="text-sm text-orange-700 dark:text-orange-300">
					超低コスト・高速・シンプルな技術スタック。
				</p>
			</div>
			<div class="p-4 rounded-lg bg-green-50 dark:bg-green-900/20 border border-green-200 dark:border-green-800">
				<p class="font-semibold text-green-800 dark:text-green-200">Gitプッシュで自動デプロイ</p>
				<p class="text-sm text-green-700 dark:text-green-300">
					プッシュするだけで本番に反映。手動デプロイ不要。
				</p>
			</div>
		</div>
	</section>

	<!-- ナビゲーション -->
	<div class="flex justify-between pt-6 border-t border-gray-200 dark:border-gray-700">
		<a href="/cloudflare/pages" class="inline-flex items-center gap-2 px-4 py-2 rounded-lg border border-gray-300 dark:border-gray-600 hover:bg-gray-100 dark:hover:bg-gray-800 transition-colors">
			<svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
				<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 19l-7-7 7-7" />
			</svg>
			前へ：Pages デプロイ
		</a>
		<a href="/dev/best-practices" class="inline-flex items-center gap-2 px-4 py-2 rounded-lg bg-primary-600 text-white hover:bg-primary-700 transition-colors">
			次へ：開発ベストプラクティス
			<svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
				<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 5l7 7-7 7" />
			</svg>
		</a>
	</div>
</article>
