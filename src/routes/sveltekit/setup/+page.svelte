<script>
	import CodePreview from '$lib/components/CodePreview.svelte';
</script>

<svelte:head>
	<title>Tailwind導入 - SvelteKit | さとまたラボ</title>
</svelte:head>

<article>
	<h1 class="text-3xl font-bold mb-2">Tailwind導入</h1>
	<p class="text-lg text-gray-600 dark:text-gray-400 mb-8">
		SvelteKit + Tailwind CSSの環境構築とプロジェクト作成
	</p>

	<!-- 概要 -->
	<section class="mb-10">
		<h2 id="overview" class="text-xl font-bold mb-4">このページで作るもの</h2>

		<div class="p-6 rounded-xl bg-gradient-to-r from-orange-50 to-cyan-50 dark:from-orange-900/20 dark:to-cyan-900/20 border border-orange-200 dark:border-orange-800 mb-6">
			<div class="flex items-center gap-4 mb-4">
				<span class="text-3xl">🔥</span>
				<span class="text-2xl">+</span>
				<span class="text-3xl">💨</span>
			</div>
			<p class="text-gray-700 dark:text-gray-300">
				<strong>SvelteKit</strong>（Webアプリフレームワーク）と<strong>Tailwind CSS</strong>（CSSフレームワーク）を組み合わせた、モダンな開発環境を構築します。
			</p>
		</div>

		<div class="p-4 rounded-lg bg-blue-50 dark:bg-blue-900/20 border border-blue-200 dark:border-blue-800 mb-6">
			<p class="font-semibold text-blue-800 dark:text-blue-200 mb-2">必要なもの</p>
			<ul class="text-sm text-blue-700 dark:text-blue-300 list-disc list-inside space-y-1">
				<li><strong>Node.js</strong>（v18以上）- <a href="https://nodejs.org/" class="underline">公式サイト</a>からダウンロード</li>
				<li><strong>テキストエディタ</strong> - VS Code がおすすめ</li>
				<li><strong>ターミナル</strong> - コマンドを実行するために必要</li>
			</ul>
		</div>

		<div class="p-4 rounded-lg bg-amber-50 dark:bg-amber-900/20 border border-amber-200 dark:border-amber-800 mb-6">
			<p class="font-semibold text-amber-800 dark:text-amber-200 mb-2">Node.jsがインストールされているか確認</p>
			<div class="text-sm text-amber-700 dark:text-amber-300">
				<p class="mb-2">ターミナルで以下を実行：</p>
				<code class="bg-amber-200 dark:bg-amber-800 px-2 py-1 rounded">node -v</code>
				<p class="mt-2">バージョン番号（v18.x.x など）が表示されればOK</p>
			</div>
		</div>
	</section>

	<!-- ステップ1: プロジェクト作成 -->
	<section class="mb-10">
		<h2 id="step1" class="text-xl font-bold mb-4">
			<span class="inline-flex items-center justify-center w-8 h-8 bg-orange-500 text-white rounded-full text-sm mr-2">1</span>
			プロジェクト作成
		</h2>

		<CodePreview
			title="SvelteKitプロジェクトの作成"
			description="npx sv create コマンドを実行"
			language="bash"
			code={`# プロジェクトを作成（my-appは好きな名前に変更可能）
npx sv create my-app

# 質問に答える：
# ┌  Welcome to the Svelte CLI!
# │
# ◆  Which template would you like?
# │  ● SvelteKit minimal（これを選択）
# │  ○ SvelteKit demo
# │  ○ Svelte library
# │
# ◆  Add type checking with Typescript?
# │  ● Yes, using Typescript syntax（TypeScriptを使う場合）
# │  ○ Yes, using JSDoc comments
# │  ○ No
# │
# ◆  What would you like to add to your project?
# │  ◻ prettier（コード整形）
# │  ◻ eslint（コード検査）
# │  ☑ tailwindcss（これを選択！）  ← 重要
# │  ◻ drizzle
# │  ◻ lucia
# │  ◻ mdsvex
# │
# ◆  tailwindcss: Which plugins would you like to add?
# │  ◻ typography（文章向けスタイル）
# │  ◻ forms（フォーム向けスタイル）
# │  ◻ container-queries
# │  （必要なものを選択、なくてもOK）
# │
# └  Your project is ready!`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div style="color:#6a9955;">✓ プロジェクト作成完了</div><div style="color:#569cd6;">my-app/</div><div style="margin-left:16px;color:#9cdcfe;">├── src/</div><div style="margin-left:16px;color:#9cdcfe;">├── tailwind.config.ts</div><div style="margin-left:16px;color:#9cdcfe;">└── package.json</div></div>`}
		/>

		<div class="mt-4 p-4 rounded-lg bg-gray-50 dark:bg-gray-800/50 border border-gray-200 dark:border-gray-700">
			<p class="font-semibold text-gray-800 dark:text-gray-200 mb-3">コード解説</p>
			<div class="text-sm text-gray-700 dark:text-gray-300 space-y-2">
				<div>
					<p class="font-medium text-purple-600 dark:text-purple-400">npx sv create my-app</p>
					<ul class="list-disc list-inside ml-2 space-y-1">
						<li><code>npx</code>：npmパッケージを一時的に実行するコマンド</li>
						<li><code>sv</code>：SvelteKit公式のCLIツール</li>
						<li><code>create</code>：新規プロジェクト作成</li>
						<li><code>my-app</code>：プロジェクト名（フォルダ名になる）</li>
					</ul>
				</div>
			</div>
		</div>
	</section>

	<!-- ステップ2: インストールと起動 -->
	<section class="mb-10">
		<h2 id="step2" class="text-xl font-bold mb-4">
			<span class="inline-flex items-center justify-center w-8 h-8 bg-orange-500 text-white rounded-full text-sm mr-2">2</span>
			依存関係のインストールと起動
		</h2>

		<CodePreview
			title="npm installと開発サーバー起動"
			description="プロジェクトフォルダに移動して実行"
			language="bash"
			code={`# プロジェクトフォルダに移動
cd my-app

# 依存関係をインストール
npm install

# 開発サーバーを起動
npm run dev

# 表示される内容：
#   VITE v5.x.x  ready in xxx ms
#
#   ➜  Local:   http://localhost:5173/
#   ➜  Network: use --host to expose
#
#   ➜  press h + enter to show help`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div style="color:#4ec9b0;">VITE</span> ready</div><div style="margin-top:8px;">➜  Local: <span style="color:#569cd6;text-decoration:underline;">http://localhost:5173/</span></div><div style="color:#6a9955;margin-top:8px;">ブラウザでこのURLを開く！</div></div>`}
		/>

		<div class="mt-4 p-4 rounded-lg bg-green-50 dark:bg-green-900/20 border border-green-200 dark:border-green-800">
			<p class="font-semibold text-green-800 dark:text-green-200 mb-2">ブラウザで確認</p>
			<p class="text-sm text-green-700 dark:text-green-300">
				<code class="bg-green-200 dark:bg-green-800 px-2 py-1 rounded">http://localhost:5173/</code> をブラウザで開くと、SvelteKitのウェルカムページが表示されます！
			</p>
		</div>

		<div class="mt-4 p-4 rounded-lg bg-gray-50 dark:bg-gray-800/50 border border-gray-200 dark:border-gray-700">
			<p class="font-semibold text-gray-800 dark:text-gray-200 mb-3">コマンド解説</p>
			<div class="text-sm text-gray-700 dark:text-gray-300 space-y-2">
				<p><code class="bg-gray-200 dark:bg-gray-700 px-1 rounded">cd my-app</code>：my-appフォルダに移動（change directory）</p>
				<p><code class="bg-gray-200 dark:bg-gray-700 px-1 rounded">npm install</code>：package.jsonに書かれたライブラリをダウンロード</p>
				<p><code class="bg-gray-200 dark:bg-gray-700 px-1 rounded">npm run dev</code>：開発サーバーを起動（ファイル保存で自動リロード）</p>
			</div>
		</div>
	</section>

	<!-- ステップ3: プロジェクト構造 -->
	<section class="mb-10">
		<h2 id="step3" class="text-xl font-bold mb-4">
			<span class="inline-flex items-center justify-center w-8 h-8 bg-orange-500 text-white rounded-full text-sm mr-2">3</span>
			プロジェクト構造を理解する
		</h2>

		<CodePreview
			title="フォルダ構造"
			description="作成されたファイルとその役割"
			language="text"
			code={`my-app/
├── src/
│   ├── routes/              ← ページを置く場所（重要！）
│   │   └── +page.svelte     ← トップページ（/）
│   ├── lib/                 ← 共通コンポーネントやユーティリティ
│   ├── app.html             ← HTMLテンプレート
│   └── app.css              ← グローバルCSS（Tailwind読み込み済み）
│
├── static/                  ← 画像などの静的ファイル
│   └── favicon.png
│
├── tailwind.config.ts       ← Tailwindの設定
├── svelte.config.js         ← SvelteKitの設定
├── vite.config.ts           ← ビルドツールの設定
├── package.json             ← 依存関係とスクリプト
└── tsconfig.json            ← TypeScript設定`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div style="color:#dcdcaa;">src/routes/</div><div style="margin-left:16px;color:#6a9955;">ここにページを作る</div><div style="margin-top:8px;color:#dcdcaa;">src/lib/</div><div style="margin-left:16px;color:#6a9955;">共通パーツを置く</div></div>`}
		/>

		<div class="mt-4 p-4 rounded-lg bg-gray-50 dark:bg-gray-800/50 border border-gray-200 dark:border-gray-700">
			<p class="font-semibold text-gray-800 dark:text-gray-200 mb-3">重要なフォルダの解説</p>
			<div class="text-sm text-gray-700 dark:text-gray-300 space-y-3">
				<div class="p-3 bg-orange-50 dark:bg-orange-900/20 rounded">
					<p class="font-medium text-orange-700 dark:text-orange-300">src/routes/ - ページの場所</p>
					<p>このフォルダの構造がそのままURLになります。</p>
					<ul class="list-disc list-inside mt-1 ml-2">
						<li><code>routes/+page.svelte</code> → <code>/</code></li>
						<li><code>routes/about/+page.svelte</code> → <code>/about</code></li>
						<li><code>routes/blog/[slug]/+page.svelte</code> → <code>/blog/記事ID</code></li>
					</ul>
				</div>
				<div class="p-3 bg-blue-50 dark:bg-blue-900/20 rounded">
					<p class="font-medium text-blue-700 dark:text-blue-300">src/lib/ - 共通部品</p>
					<p><code>$lib</code>というエイリアスでインポートできます。</p>
					<p class="mt-1"><code>import Button from '$lib/components/Button.svelte';</code></p>
				</div>
			</div>
		</div>
	</section>

	<!-- ステップ4: Tailwindの確認 -->
	<section class="mb-10">
		<h2 id="step4" class="text-xl font-bold mb-4">
			<span class="inline-flex items-center justify-center w-8 h-8 bg-orange-500 text-white rounded-full text-sm mr-2">4</span>
			Tailwind CSSが動いているか確認
		</h2>

		<CodePreview
			title="app.css の確認"
			description="Tailwindの読み込み"
			language="css"
			code={`/* src/app.css */
/* sv createで自動的に追加されている */
@import 'tailwindcss';

/* カスタムスタイルを追加する場合はここに書く */`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div style="color:#6a9955;">/* @import 'tailwindcss' で</div><div style="color:#6a9955;">   Tailwindの全機能が使える */</div></div>`}
		/>

		<CodePreview
			title="Tailwindを使ってみる"
			description="+page.svelte を編集"
			language="svelte"
			code={`<!-- src/routes/+page.svelte -->
<h1 class="text-3xl font-bold text-blue-600">
  Hello SvelteKit + Tailwind!
</h1>

<p class="mt-4 text-gray-600">
  Tailwind CSSが正常に動作しています。
</p>

<button class="mt-4 px-6 py-2 bg-orange-500 text-white rounded-lg hover:bg-orange-600 transition-colors">
  ボタン
</button>`}
			previewHtml={`<div style="padding:16px;"><h1 style="font-size:30px;font-weight:bold;color:#2563eb;">Hello SvelteKit + Tailwind!</h1><p style="margin-top:16px;color:#4b5563;">Tailwind CSSが正常に動作しています。</p><button style="margin-top:16px;padding:8px 24px;background:#f97316;color:white;border:none;border-radius:8px;cursor:pointer;">ボタン</button></div>`}
		/>

		<div class="mt-4 p-4 rounded-lg bg-gray-50 dark:bg-gray-800/50 border border-gray-200 dark:border-gray-700">
			<p class="font-semibold text-gray-800 dark:text-gray-200 mb-3">クラスの解説</p>
			<div class="text-sm text-gray-700 dark:text-gray-300 space-y-2">
				<div class="grid grid-cols-2 gap-2">
					<div><code class="text-cyan-600">text-3xl</code>：フォントサイズ30px</div>
					<div><code class="text-cyan-600">font-bold</code>：太字</div>
					<div><code class="text-cyan-600">text-blue-600</code>：青色の文字</div>
					<div><code class="text-cyan-600">mt-4</code>：上にmargin 16px</div>
					<div><code class="text-cyan-600">px-6</code>：左右padding 24px</div>
					<div><code class="text-cyan-600">py-2</code>：上下padding 8px</div>
					<div><code class="text-cyan-600">bg-orange-500</code>：オレンジ背景</div>
					<div><code class="text-cyan-600">rounded-lg</code>：角丸8px</div>
					<div><code class="text-cyan-600">hover:bg-orange-600</code>：ホバー時に色変更</div>
					<div><code class="text-cyan-600">transition-colors</code>：色変化をアニメーション</div>
				</div>
			</div>
		</div>
	</section>

	<!-- ステップ5: 最初のページを作る -->
	<section class="mb-10">
		<h2 id="step5" class="text-xl font-bold mb-4">
			<span class="inline-flex items-center justify-center w-8 h-8 bg-orange-500 text-white rounded-full text-sm mr-2">5</span>
			新しいページを追加する
		</h2>

		<CodePreview
			title="Aboutページを作成"
			description="routes/about/+page.svelte を作成"
			language="svelte"
			code={`<!-- src/routes/about/+page.svelte -->
<svelte:head>
  <title>About | My App</title>
</svelte:head>

<div class="max-w-2xl mx-auto py-12 px-4">
  <h1 class="text-3xl font-bold mb-6">About</h1>

  <p class="text-gray-600 leading-relaxed">
    このサイトはSvelteKitとTailwind CSSで作られています。
  </p>

  <a
    href="/"
    class="inline-block mt-6 text-blue-600 hover:underline"
  >
    ← ホームに戻る
  </a>
</div>`}
			previewHtml={`<div style="max-width:400px;padding:24px;"><h1 style="font-size:24px;font-weight:bold;margin-bottom:16px;">About</h1><p style="color:#4b5563;line-height:1.7;">このサイトはSvelteKitとTailwind CSSで作られています。</p><a href="#" style="display:inline-block;margin-top:16px;color:#2563eb;">← ホームに戻る</a></div>`}
		/>

		<div class="mt-4 p-4 rounded-lg bg-green-50 dark:bg-green-900/20 border border-green-200 dark:border-green-800">
			<p class="font-semibold text-green-800 dark:text-green-200 mb-2">確認方法</p>
			<p class="text-sm text-green-700 dark:text-green-300">
				ファイルを保存して <code class="bg-green-200 dark:bg-green-800 px-2 py-1 rounded">http://localhost:5173/about</code> にアクセス！
			</p>
		</div>
	</section>

	<!-- ステップ6: レイアウトを追加 -->
	<section class="mb-10">
		<h2 id="step6" class="text-xl font-bold mb-4">
			<span class="inline-flex items-center justify-center w-8 h-8 bg-orange-500 text-white rounded-full text-sm mr-2">6</span>
			共通レイアウトを作る
		</h2>

		<CodePreview
			title="+layout.svelte"
			description="全ページ共通のヘッダー・フッター"
			language="svelte"
			code={`<!-- src/routes/+layout.svelte -->
<script>
  import '../app.css';
  let { children } = $props();
</script>

<div class="min-h-screen flex flex-col">
  <!-- ヘッダー -->
  <header class="bg-white border-b sticky top-0 z-50">
    <div class="max-w-6xl mx-auto px-4 py-4 flex items-center justify-between">
      <a href="/" class="text-xl font-bold text-orange-500">
        My App
      </a>
      <nav class="flex gap-6">
        <a href="/" class="hover:text-orange-500 transition-colors">ホーム</a>
        <a href="/about" class="hover:text-orange-500 transition-colors">About</a>
      </nav>
    </div>
  </header>

  <!-- メインコンテンツ -->
  <main class="flex-1">
    {@render children()}
  </main>

  <!-- フッター -->
  <footer class="bg-gray-100 border-t">
    <div class="max-w-6xl mx-auto px-4 py-6 text-center text-gray-600">
      © 2024 My App. All rights reserved.
    </div>
  </footer>
</div>`}
			previewHtml={`<div style="border:1px solid #e5e7eb;border-radius:8px;overflow:hidden;"><div style="background:white;padding:12px 16px;border-bottom:1px solid #e5e7eb;display:flex;justify-content:space-between;align-items:center;"><span style="font-weight:bold;color:#f97316;">My App</span><div style="display:flex;gap:16px;font-size:14px;"><span>ホーム</span><span>About</span></div></div><div style="padding:24px;min-height:80px;color:#6b7280;text-align:center;">ページ内容</div><div style="background:#f3f4f6;padding:12px;text-align:center;font-size:12px;color:#6b7280;">© 2024 My App</div></div>`}
		/>

		<div class="mt-4 p-4 rounded-lg bg-gray-50 dark:bg-gray-800/50 border border-gray-200 dark:border-gray-700">
			<p class="font-semibold text-gray-800 dark:text-gray-200 mb-3">コード解説</p>
			<div class="text-sm text-gray-700 dark:text-gray-300 space-y-2">
				<p><code class="bg-gray-200 dark:bg-gray-700 px-1 rounded">import '../app.css'</code>：Tailwindを全ページで読み込む</p>
				<p><code class="bg-gray-200 dark:bg-gray-700 px-1 rounded">let {'{ children }'} = $props()</code>：各ページの内容を受け取る</p>
				<p><code class="bg-gray-200 dark:bg-gray-700 px-1 rounded">{'{@render children()}'}</code>：ページの内容をここに表示</p>
			</div>
		</div>

		<!-- レイアウトの仕組み -->
		<div class="mt-6 p-4 rounded-lg bg-blue-50 dark:bg-blue-900/20 border border-blue-200 dark:border-blue-800">
			<p class="font-semibold text-blue-800 dark:text-blue-200 mb-3">レイアウトの仕組み（重要！）</p>
			<div class="text-sm text-blue-700 dark:text-blue-300 space-y-3">
				<div class="p-3 bg-white dark:bg-gray-800 rounded">
					<p class="font-medium mb-2">自動適用される</p>
					<p><code class="bg-blue-100 dark:bg-blue-800 px-1 rounded">+layout.svelte</code> を作成するだけで、<strong>同階層と全ての子ページに自動で適用</strong>されます。インポートは不要です。</p>
				</div>
				<div class="p-3 bg-white dark:bg-gray-800 rounded">
					<p class="font-medium mb-2">配置場所による適用範囲</p>
					<div class="font-mono text-xs space-y-1 mt-2">
						<p><span class="text-orange-600">src/routes/+layout.svelte</span> → 全ページに適用（ルートレイアウト）</p>
						<p><span class="text-orange-600">src/routes/blog/+layout.svelte</span> → /blog 以下のみに適用</p>
						<p><span class="text-orange-600">src/routes/admin/+layout.svelte</span> → /admin 以下のみに適用</p>
					</div>
				</div>
			</div>
		</div>

		<!-- レイアウトのネスト -->
		<div class="mt-4 p-4 rounded-lg bg-green-50 dark:bg-green-900/20 border border-green-200 dark:border-green-800">
			<p class="font-semibold text-green-800 dark:text-green-200 mb-3">レイアウトのネスト（入れ子）</p>
			<div class="text-sm text-green-700 dark:text-green-300">
				<p class="mb-3">子フォルダにも<code class="bg-green-200 dark:bg-green-800 px-1 rounded">+layout.svelte</code>を作ると、レイアウトが入れ子になります。</p>
				<div class="bg-white dark:bg-gray-800 p-3 rounded font-mono text-xs">
					<p class="text-gray-500">例: /blog/hello にアクセスすると...</p>
					<div class="mt-2 space-y-1">
						<p>1. <span class="text-purple-600">routes/+layout.svelte</span>（ルートレイアウト：ヘッダー・フッター）</p>
						<p class="pl-4">↓ この中に</p>
						<p>2. <span class="text-purple-600">routes/blog/+layout.svelte</span>（blogレイアウト：サイドバー等）</p>
						<p class="pl-8">↓ この中に</p>
						<p>3. <span class="text-purple-600">routes/blog/[slug]/+page.svelte</span>（実際のページ内容）</p>
					</div>
				</div>
			</div>
		</div>

		<!-- 実例 -->
		<CodePreview
			title="セクション別レイアウトの例"
			description="blogセクション専用のサイドバー付きレイアウト"
			language="svelte"
			code={`<!-- src/routes/blog/+layout.svelte -->
<script>
  let { children } = $props();
</script>

<!-- ルートレイアウト(ヘッダー・フッター)の中に表示される -->
<div class="flex max-w-6xl mx-auto">
  <!-- サイドバー -->
  <aside class="w-64 p-4 border-r">
    <h3 class="font-bold mb-4">カテゴリ</h3>
    <ul class="space-y-2">
      <li><a href="/blog?cat=tech">技術</a></li>
      <li><a href="/blog?cat=life">生活</a></li>
    </ul>
  </aside>

  <!-- 記事コンテンツ -->
  <main class="flex-1 p-6">
    {@render children()}
  </main>
</div>`}
			previewHtml={`<div style="border:1px solid #e5e7eb;border-radius:8px;overflow:hidden;"><div style="background:#f9fafb;padding:8px 12px;border-bottom:1px solid #e5e7eb;font-size:12px;color:#6b7280;">← ルートレイアウト（ヘッダー）</div><div style="display:flex;"><div style="width:120px;padding:12px;border-right:1px solid #e5e7eb;background:#fafafa;"><div style="font-weight:bold;font-size:12px;margin-bottom:8px;">カテゴリ</div><div style="font-size:11px;color:#3b82f6;">技術<br>生活</div></div><div style="flex:1;padding:12px;text-align:center;color:#9ca3af;font-size:12px;">記事内容<br>(+page.svelte)</div></div><div style="background:#f9fafb;padding:8px 12px;border-top:1px solid #e5e7eb;font-size:12px;color:#6b7280;">← ルートレイアウト（フッター）</div></div>`}
		/>

		<!-- なぜ自動適用されるのか？ -->
		<div class="mt-6 p-4 rounded-lg bg-purple-50 dark:bg-purple-900/20 border border-purple-200 dark:border-purple-800">
			<p class="font-semibold text-purple-800 dark:text-purple-200 mb-3">なぜページにimportを書かなくても適用されるのか？</p>
			<div class="text-sm text-purple-700 dark:text-purple-300 space-y-4">
				<div class="p-3 bg-white dark:bg-gray-800 rounded">
					<p class="font-medium mb-2">SvelteKitの「ファイル規約」</p>
					<p>SvelteKitは<strong>ファイル名で役割を判断</strong>します。<code class="bg-purple-200 dark:bg-purple-800 px-1 rounded">+layout.svelte</code>という名前を見つけると、自動的に「これはレイアウトだ」と認識し、該当フォルダのページを包み込みます。</p>
				</div>

				<div class="p-3 bg-white dark:bg-gray-800 rounded">
					<p class="font-medium mb-2">ビルド時に自動で組み立てられる</p>
					<p>開発者が書くのはページ（<code class="bg-purple-200 dark:bg-purple-800 px-1 rounded">+page.svelte</code>）だけ。SvelteKitがビルド時に以下を自動で行います：</p>
					<ol class="list-decimal list-inside mt-2 ml-2 space-y-1">
						<li>親フォルダから順に<code class="bg-purple-200 dark:bg-purple-800 px-1 rounded">+layout.svelte</code>を探す</li>
						<li>見つけたレイアウトを順番にネストする</li>
						<li>最後にページコンテンツを<code class="bg-purple-200 dark:bg-purple-800 px-1 rounded">{'{@render children()}'}</code>の位置に挿入</li>
					</ol>
				</div>

				<div class="p-3 bg-white dark:bg-gray-800 rounded">
					<p class="font-medium mb-2">ページ側でやることは「何もない」</p>
					<div class="bg-gray-100 dark:bg-gray-900 p-3 rounded mt-2 font-mono text-xs">
						<p class="text-gray-500"><!-- src/routes/about/+page.svelte --></p>
						<p class="text-gray-500"><!-- importは一切不要！ --></p>
						<p>&lt;h1&gt;Aboutページ&lt;/h1&gt;</p>
						<p>&lt;p&gt;これだけでOK。レイアウトは自動で適用される。&lt;/p&gt;</p>
					</div>
					<p class="mt-2 text-xs">↑ このシンプルなコードだけで、ヘッダー・フッター付きで表示されます。</p>
				</div>
			</div>
		</div>

		<!-- 図解：自動適用の仕組み -->
		<div class="mt-4 p-4 rounded-lg bg-gray-50 dark:bg-gray-800/50 border border-gray-200 dark:border-gray-700">
			<p class="font-semibold text-gray-800 dark:text-gray-200 mb-3">図解：レイアウト自動適用の流れ</p>
			<div class="bg-white dark:bg-gray-900 p-4 rounded font-mono text-xs overflow-x-auto">
				<p class="text-gray-500 mb-3">例: /about にアクセスした時</p>
				<div class="space-y-2">
					<p>1. SvelteKitが <span class="text-orange-600">routes/+layout.svelte</span> を見つける</p>
					<p>2. SvelteKitが <span class="text-blue-600">routes/about/+page.svelte</span> を見つける</p>
					<p>3. 自動で以下のように組み立てる：</p>
					<div class="mt-2 ml-4 p-3 border-l-2 border-orange-400">
						<p class="text-orange-600">&lt;!-- +layout.svelte の内容 --&gt;</p>
						<p>&lt;Header /&gt;</p>
						<p>&lt;main&gt;</p>
						<p class="ml-4 text-blue-600">&lt;!-- ここに +page.svelte が自動挿入 --&gt;</p>
						<p class="ml-4 text-blue-600">&lt;h1&gt;Aboutページ&lt;/h1&gt;</p>
						<p class="ml-4 text-blue-600">&lt;p&gt;これだけでOK...&lt;/p&gt;</p>
						<p>&lt;/main&gt;</p>
						<p>&lt;Footer /&gt;</p>
					</div>
				</div>
			</div>
		</div>

		<!-- 従来のフレームワークとの比較 -->
		<div class="mt-4 p-4 rounded-lg bg-amber-50 dark:bg-amber-900/20 border border-amber-200 dark:border-amber-800">
			<p class="font-semibold text-amber-800 dark:text-amber-200 mb-3">従来のフレームワークとの違い</p>
			<div class="text-sm text-amber-700 dark:text-amber-300">
				<div class="grid md:grid-cols-2 gap-4">
					<div class="p-3 bg-white dark:bg-gray-800 rounded">
						<p class="font-medium text-red-600 dark:text-red-400 mb-2">従来の方法（React等）</p>
						<div class="bg-gray-100 dark:bg-gray-900 p-2 rounded font-mono text-xs">
							<p>import Layout from '../Layout';</p>
							<p class="mt-1">function About() {'{'}</p>
							<p class="ml-2">return (</p>
							<p class="ml-4">&lt;Layout&gt;</p>
							<p class="ml-6">&lt;h1&gt;About&lt;/h1&gt;</p>
							<p class="ml-4">&lt;/Layout&gt;</p>
							<p class="ml-2">);</p>
							<p>{'}'}</p>
						</div>
						<p class="mt-2 text-xs">毎回importして囲む必要がある</p>
					</div>
					<div class="p-3 bg-white dark:bg-gray-800 rounded">
						<p class="font-medium text-green-600 dark:text-green-400 mb-2">SvelteKitの方法</p>
						<div class="bg-gray-100 dark:bg-gray-900 p-2 rounded font-mono text-xs">
							<p>&lt;h1&gt;About&lt;/h1&gt;</p>
							<p class="mt-2 text-gray-500">// これだけ！</p>
							<p class="text-gray-500">// importもラップも不要</p>
						</div>
						<p class="mt-2 text-xs">ファイル名規約で自動適用</p>
					</div>
				</div>
			</div>
		</div>

		<div class="mt-4 p-4 rounded-lg bg-blue-50 dark:bg-blue-900/20 border border-blue-200 dark:border-blue-800">
			<p class="font-semibold text-blue-800 dark:text-blue-200 mb-2">まとめ</p>
			<ul class="text-sm text-blue-700 dark:text-blue-300 list-disc list-inside space-y-1">
				<li><code class="bg-blue-200 dark:bg-blue-800 px-1 rounded">+layout.svelte</code>を置くだけで自動適用（ページ側でimport不要）</li>
				<li>SvelteKitが<strong>ファイル名規約</strong>で役割を判断する</li>
				<li>ビルド時に自動でレイアウトとページを組み立てる</li>
				<li>開発者はページの中身だけに集中できる</li>
			</ul>
		</div>
	</section>

	<!-- よく使うコマンド -->
	<section class="mb-10">
		<h2 id="commands" class="text-xl font-bold mb-4">よく使うコマンド</h2>

		<div class="overflow-x-auto">
			<table class="w-full text-sm">
				<thead>
					<tr class="border-b border-gray-200 dark:border-gray-700">
						<th class="text-left py-3 px-4">コマンド</th>
						<th class="text-left py-3 px-4">説明</th>
					</tr>
				</thead>
				<tbody>
					<tr class="border-b border-gray-200 dark:border-gray-700">
						<td class="py-3 px-4 font-mono text-orange-600">npm run dev</td>
						<td class="py-3 px-4">開発サーバーを起動（ホットリロード付き）</td>
					</tr>
					<tr class="border-b border-gray-200 dark:border-gray-700">
						<td class="py-3 px-4 font-mono text-orange-600">npm run build</td>
						<td class="py-3 px-4">本番用にビルド</td>
					</tr>
					<tr class="border-b border-gray-200 dark:border-gray-700">
						<td class="py-3 px-4 font-mono text-orange-600">npm run preview</td>
						<td class="py-3 px-4">ビルド結果をプレビュー</td>
					</tr>
					<tr class="border-b border-gray-200 dark:border-gray-700">
						<td class="py-3 px-4 font-mono text-orange-600">npm install パッケージ名</td>
						<td class="py-3 px-4">パッケージを追加</td>
					</tr>
					<tr>
						<td class="py-3 px-4 font-mono text-orange-600">npx sv add</td>
						<td class="py-3 px-4">機能を追加（Tailwind, Drizzle, Luciaなど）</td>
					</tr>
				</tbody>
			</table>
		</div>
	</section>

	<!-- 次のステップ -->
	<section class="mb-10">
		<h2 id="next" class="text-xl font-bold mb-4">次のステップ</h2>

		<div class="grid grid-cols-1 md:grid-cols-2 gap-4">
			<a href="/sveltekit/routing" class="p-4 rounded-lg border border-gray-200 dark:border-gray-700 hover:border-orange-400 dark:hover:border-orange-400 transition-colors">
				<h3 class="font-bold mb-2">ルーティングを学ぶ</h3>
				<p class="text-sm text-gray-600 dark:text-gray-400">URLとファイル構造の関係を理解する</p>
			</a>
			<a href="/sveltekit/loading" class="p-4 rounded-lg border border-gray-200 dark:border-gray-700 hover:border-orange-400 dark:hover:border-orange-400 transition-colors">
				<h3 class="font-bold mb-2">データ読み込み</h3>
				<p class="text-sm text-gray-600 dark:text-gray-400">load関数でサーバーからデータを取得</p>
			</a>
			<a href="/sveltekit/state" class="p-4 rounded-lg border border-gray-200 dark:border-gray-700 hover:border-orange-400 dark:hover:border-orange-400 transition-colors">
				<h3 class="font-bold mb-2">状態管理（Runes）</h3>
				<p class="text-sm text-gray-600 dark:text-gray-400">$stateや$derivedの使い方</p>
			</a>
			<a href="/tailwind/utilities" class="p-4 rounded-lg border border-gray-200 dark:border-gray-700 hover:border-cyan-400 dark:hover:border-cyan-400 transition-colors">
				<h3 class="font-bold mb-2">Tailwindユーティリティ</h3>
				<p class="text-sm text-gray-600 dark:text-gray-400">よく使うクラスを覚える</p>
			</a>
		</div>
	</section>

	<!-- ナビゲーション -->
	<div class="flex justify-between pt-6 border-t border-gray-200 dark:border-gray-700">
		<a href="/sveltekit/intro" class="inline-flex items-center gap-2 px-4 py-2 rounded-lg border border-gray-300 dark:border-gray-600 hover:bg-gray-100 dark:hover:bg-gray-800 transition-colors">
			<svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
				<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 19l-7-7 7-7" />
			</svg>
			前へ：はじめに
		</a>
		<a href="/sveltekit/routing" class="inline-flex items-center gap-2 px-4 py-2 rounded-lg bg-primary-600 text-white hover:bg-primary-700 transition-colors">
			次へ：ルーティング
			<svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
				<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 5l7 7-7 7" />
			</svg>
		</a>
	</div>
</article>
