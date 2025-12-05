<script>
	import CodePreview from '$lib/components/CodePreview.svelte';
</script>

<svelte:head>
	<title>SvelteKit レイアウト | さとまたラボ</title>
</svelte:head>

<article>
	<h1 class="text-3xl font-bold mb-2">レイアウト</h1>
	<p class="text-lg text-gray-600 dark:text-gray-400 mb-8">
		ページ間で共通のUIを定義する
	</p>

	<!-- レイアウトとは -->
	<section class="mb-10">
		<h2 id="what-is" class="text-xl font-bold mb-4">レイアウトとは？</h2>

		<div class="p-6 rounded-xl bg-blue-50 dark:bg-blue-900/20 border border-blue-200 dark:border-blue-800 mb-6">
			<p class="text-blue-800 dark:text-blue-200 mb-4">
				<strong>日常での例え：</strong>額縁（フレーム）
			</p>
			<div class="grid grid-cols-1 md:grid-cols-2 gap-4 text-sm">
				<div class="p-3 bg-white dark:bg-gray-800 rounded-lg">
					<div class="font-semibold text-blue-700 dark:text-blue-300 mb-2">額縁</div>
					<p class="text-gray-600 dark:text-gray-400">
						どんな絵を入れても<br>
						外枠は同じデザイン
					</p>
				</div>
				<div class="p-3 bg-white dark:bg-gray-800 rounded-lg">
					<div class="font-semibold text-blue-700 dark:text-blue-300 mb-2">レイアウト</div>
					<p class="text-gray-600 dark:text-gray-400">
						どんなページでも<br>
						ヘッダーとフッターは同じ
					</p>
				</div>
			</div>
		</div>

		<div class="p-4 rounded-lg bg-amber-50 dark:bg-amber-900/20 border border-amber-200 dark:border-amber-800 mb-6">
			<p class="font-semibold text-amber-800 dark:text-amber-200">なぜレイアウトが必要？</p>
			<div class="text-sm text-amber-700 dark:text-amber-300 mt-2">
				<p class="mb-2"><strong>レイアウトがないと困ること：</strong></p>
				<ul class="list-disc list-inside space-y-1 mb-3">
					<li>全ページにヘッダーのコードをコピペ（10ページあれば10回！）</li>
					<li>ヘッダーを修正→全ファイルを手作業で修正</li>
					<li>修正漏れでページによってデザインが違う...</li>
				</ul>
				<p><strong>レイアウトがあれば：</strong>1箇所書くだけで全ページに適用！修正も1箇所だけ。</p>
			</div>
		</div>

		<div class="p-4 rounded-lg bg-gray-100 dark:bg-gray-800 mb-6">
			<p class="font-semibold text-gray-800 dark:text-gray-200 mb-2">用語解説</p>
			<div class="text-sm text-gray-700 dark:text-gray-300 space-y-2">
				<p><strong>レイアウト</strong>：ページの共通部分（枠組み）のこと。ヘッダーやフッターなど。</p>
				<p><strong>ヘッダー</strong>：ページ上部の共通部分。ロゴやナビゲーションメニューを置く場所。</p>
				<p><strong>フッター</strong>：ページ下部の共通部分。著作権表示やリンク集を置く場所。</p>
				<p><strong>サイドバー</strong>：ページ横の共通部分。メニューや補足情報を置く場所。</p>
				<p><strong>children</strong>：子要素のこと。レイアウトでは「ページの中身」を指す。</p>
			</div>
		</div>

		<div class="p-4 rounded-lg bg-gray-100 dark:bg-gray-800 mb-6">
			<p class="font-semibold text-gray-800 dark:text-gray-200 mb-2">レイアウトでできること</p>
			<div class="text-sm text-gray-700 dark:text-gray-300 space-y-1">
				<p>✓ ヘッダー、フッター、サイドバーの共通化</p>
				<p>✓ ナビゲーションメニューの配置</p>
				<p>✓ 認証チェック（ログイン必須ページなど）</p>
				<p>✓ ページ遷移時のアニメーション</p>
			</div>
		</div>
	</section>

	<!-- 基本的なレイアウト -->
	<section class="mb-10">
		<h2 id="basic" class="text-xl font-bold mb-4">基本的なレイアウト</h2>

		<CodePreview
			title="+layout.svelte"
			description="すべてのページに適用"
			language="svelte"
			code={`<!-- src/routes/+layout.svelte -->
<script>
  let { children } = $props();
</script>

<div class="app">
  <header>
    <nav>
      <a href="/">ホーム</a>
      <a href="/about">アバウト</a>
      <a href="/contact">お問い合わせ</a>
    </nav>
  </header>

  <main>
    {@render children()}  <!-- ここにページが表示される -->
  </main>

  <footer>
    <p>© 2024 My Website</p>
  </footer>
</div>

<style>
  .app {
    display: flex;
    flex-direction: column;
    min-height: 100vh;
  }
  main {
    flex: 1;
  }
</style>`}
			previewHtml={`<div style="border:1px solid #e5e7eb;border-radius:8px;overflow:hidden;"><div style="background:#f3f4f6;padding:8px 12px;border-bottom:1px solid #e5e7eb;display:flex;gap:16px;"><a href="#" style="color:#3b82f6;">ホーム</a><a href="#" style="color:#6b7280;">アバウト</a><a href="#" style="color:#6b7280;">お問い合わせ</a></div><div style="padding:20px;text-align:center;color:#6b7280;">ページ内容</div><div style="background:#f3f4f6;padding:8px 12px;border-top:1px solid #e5e7eb;text-align:center;font-size:12px;color:#6b7280;">© 2024 My Website</div></div>`}
		/>

		<div class="p-4 rounded-lg bg-amber-50 dark:bg-amber-900/20 border border-amber-200 dark:border-amber-800 mb-6">
			<p class="font-semibold text-amber-800 dark:text-amber-200">@render children() とは？</p>
			<p class="text-sm text-amber-700 dark:text-amber-300 mt-2">
				Svelte 5の書き方です。ここにページの内容（+page.svelte）が挿入されます。<br>
				レイアウトは「枠」、childrenは「中身」と考えてください。
			</p>
		</div>
	</section>

	<!-- ネストしたレイアウト -->
	<section class="mb-10">
		<h2 id="nested" class="text-xl font-bold mb-4">ネストしたレイアウト</h2>

		<div class="p-4 rounded-lg bg-blue-50 dark:bg-blue-900/20 border border-blue-200 dark:border-blue-800 mb-6">
			<p class="font-semibold text-blue-800 dark:text-blue-200 mb-2">レイアウトは入れ子にできる</p>
			<p class="text-sm text-blue-700 dark:text-blue-300">
				<code>/dashboard</code> 以下だけ別のレイアウト、という設定ができます。
			</p>
		</div>

		<CodePreview
			title="ディレクトリ構造"
			description="レイアウトの継承"
			language="text"
			code={`src/routes/
├── +layout.svelte        # 全ページ共通（ヘッダー・フッター）
├── +page.svelte          # / (トップページ)
├── about/
│   └── +page.svelte      # /about
└── dashboard/
    ├── +layout.svelte    # dashboardだけのレイアウト（サイドバー）
    ├── +page.svelte      # /dashboard
    ├── settings/
    │   └── +page.svelte  # /dashboard/settings
    └── profile/
        └── +page.svelte  # /dashboard/profile

/dashboard/* のページは：
1. routes/+layout.svelte（ルート）
2. routes/dashboard/+layout.svelte（ダッシュボード）
の両方が適用される`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div style="color:#6a9955;">// /dashboard/settings の表示</div><div style="margin-top:8px;">[ルートレイアウト]</div><div style="margin-left:10px;">[ダッシュボードレイアウト]</div><div style="margin-left:20px;">[settingsページ]</div></div>`}
		/>

		<CodePreview
			title="ダッシュボード用レイアウト"
			description="サイドバー付きレイアウト"
			language="svelte"
			code={`<!-- src/routes/dashboard/+layout.svelte -->
<script>
  let { children } = $props();
</script>

<div class="dashboard-layout">
  <aside class="sidebar">
    <nav>
      <a href="/dashboard">ダッシュボード</a>
      <a href="/dashboard/profile">プロフィール</a>
      <a href="/dashboard/settings">設定</a>
    </nav>
  </aside>

  <div class="content">
    {@render children()}
  </div>
</div>

<style>
  .dashboard-layout {
    display: flex;
    min-height: calc(100vh - 120px);
  }
  .sidebar {
    width: 250px;
    background: #f3f4f6;
    padding: 1rem;
  }
  .content {
    flex: 1;
    padding: 1rem;
  }
</style>`}
			previewHtml={`<div style="display:flex;border:1px solid #e5e7eb;border-radius:8px;overflow:hidden;"><div style="width:120px;background:#f3f4f6;padding:12px;border-right:1px solid #e5e7eb;"><div style="font-size:12px;color:#6b7280;margin-bottom:8px;">サイドバー</div><a href="#" style="display:block;font-size:12px;color:#3b82f6;margin-bottom:4px;">ダッシュボード</a><a href="#" style="display:block;font-size:12px;color:#6b7280;margin-bottom:4px;">プロフィール</a><a href="#" style="display:block;font-size:12px;color:#6b7280;">設定</a></div><div style="flex:1;padding:12px;text-align:center;color:#6b7280;">ページ内容</div></div>`}
		/>
	</section>

	<!-- レイアウトのリセット -->
	<section class="mb-10">
		<h2 id="reset" class="text-xl font-bold mb-4">レイアウトのリセット</h2>

		<CodePreview
			title="+page@.svelte"
			description="親レイアウトを使わない"
			language="text"
			code={`src/routes/
├── +layout.svelte           # 通常のレイアウト
├── +page.svelte             # / (レイアウト適用)
└── login/
    └── +page@.svelte        # /login (レイアウトなし！)

ファイル名を +page@.svelte にすると
ルートレイアウトを含む全レイアウトをリセット

+page@dashboard.svelte なら
dashboardレイアウト以降をリセット`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div style="color:#4ec9b0;">+page@.svelte</div><div style="color:#6a9955;">// ログインページなど</div><div style="color:#6a9955;">// ヘッダー不要なページに使う</div></div>`}
		/>
	</section>

	<!-- レイアウトデータ -->
	<section class="mb-10">
		<h2 id="data" class="text-xl font-bold mb-4">レイアウトでデータを読み込む</h2>

		<CodePreview
			title="+layout.server.ts"
			description="レイアウト用のload関数"
			language="typescript"
			code={`// src/routes/+layout.server.ts
export async function load({ cookies }) {
  const sessionId = cookies.get('session');
  const user = sessionId ? await getUser(sessionId) : null;

  return {
    user  // 全ページで使える
  };
}

// src/routes/+layout.svelte
<script>
  let { data, children } = $props();
</script>

<header>
  {#if data.user}
    <span>ようこそ、{data.user.name}さん</span>
    <a href="/logout">ログアウト</a>
  {:else}
    <a href="/login">ログイン</a>
  {/if}
</header>

{@render children()}

// 子ページからもアクセス可能
// src/routes/dashboard/+page.svelte
<script>
  let { data } = $props();
  // data.userにアクセスできる！
</script>`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div style="color:#6a9955;">// +layout.server.ts のデータは</div><div style="color:#6a9955;">// 子ページにも引き継がれる</div></div>`}
		/>
	</section>

	<!-- グループレイアウト -->
	<section class="mb-10">
		<h2 id="group" class="text-xl font-bold mb-4">グループ（括弧フォルダ）</h2>

		<div class="p-4 rounded-lg bg-blue-50 dark:bg-blue-900/20 border border-blue-200 dark:border-blue-800 mb-6">
			<p class="font-semibold text-blue-800 dark:text-blue-200 mb-2">(folder) とは？</p>
			<p class="text-sm text-blue-700 dark:text-blue-300">
				括弧でフォルダ名を囲むと、<strong>URLには影響しない</strong>グループを作れます。<br>
				レイアウトだけを共有したいページをまとめるのに便利です。
			</p>
		</div>

		<CodePreview
			title="グループの使用例"
			description="URLに影響しないフォルダ"
			language="text"
			code={`src/routes/
├── (marketing)/           # URLには含まれない
│   ├── +layout.svelte     # マーケティング用レイアウト
│   ├── about/
│   │   └── +page.svelte   # /about
│   └── pricing/
│       └── +page.svelte   # /pricing
│
├── (app)/                 # URLには含まれない
│   ├── +layout.svelte     # アプリ用レイアウト
│   ├── dashboard/
│   │   └── +page.svelte   # /dashboard
│   └── settings/
│       └── +page.svelte   # /settings

(marketing)と(app)で別のレイアウトを適用
でもURLは /about, /dashboard のまま`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div style="color:#ce9178;">(marketing)/about</span> → /about</div><div style="color:#ce9178;">(app)/dashboard</span> → /dashboard</div><div style="color:#6a9955;margin-top:8px;">// 括弧はURLに含まれない</div></div>`}
		/>
	</section>

	<!-- 実践例 -->
	<section class="mb-10">
		<h2 id="practical" class="text-xl font-bold mb-4">実践的な構成例</h2>

		<CodePreview
			title="一般的なWebサイト構成"
			description="よくあるレイアウトパターン"
			language="text"
			code={`src/routes/
├── +layout.svelte              # 基本レイアウト（ヘッダー・フッター）
├── +layout.server.ts           # 認証情報の取得
│
├── (public)/                   # 公開ページ
│   ├── +layout.svelte          # シンプルなレイアウト
│   ├── +page.svelte            # / (トップ)
│   ├── about/+page.svelte      # /about
│   └── contact/+page.svelte    # /contact
│
├── (auth)/                     # 認証ページ
│   ├── +layout@.svelte         # レイアウトリセット（ヘッダーなし）
│   ├── login/+page.svelte      # /login
│   └── register/+page.svelte   # /register
│
└── (app)/                      # ログイン後のページ
    ├── +layout.svelte          # サイドバー付きレイアウト
    ├── +layout.server.ts       # 認証チェック（リダイレクト）
    ├── dashboard/+page.svelte  # /dashboard
    ├── profile/+page.svelte    # /profile
    └── settings/+page.svelte   # /settings`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div style="color:#4ec9b0;">(public)</div><div style="margin-left:10px;color:#6a9955;">ヘッダー + フッター</div><div style="color:#4ec9b0;margin-top:8px;">(auth)</div><div style="margin-left:10px;color:#6a9955;">シンプル（ロゴのみ）</div><div style="color:#4ec9b0;margin-top:8px;">(app)</div><div style="margin-left:10px;color:#6a9955;">サイドバー + ヘッダー</div></div>`}
		/>
	</section>

	<!-- ナビゲーション -->
	<div class="flex justify-between pt-6 border-t border-gray-200 dark:border-gray-700">
		<a href="/sveltekit/state" class="inline-flex items-center gap-2 px-4 py-2 rounded-lg border border-gray-300 dark:border-gray-600 hover:bg-gray-100 dark:hover:bg-gray-800 transition-colors">
			<svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
				<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 19l-7-7 7-7" />
			</svg>
			前へ：状態管理
		</a>
		<a href="/sveltekit/api" class="inline-flex items-center gap-2 px-4 py-2 rounded-lg bg-primary-600 text-white hover:bg-primary-700 transition-colors">
			次へ：APIエンドポイント
			<svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
				<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 5l7 7-7 7" />
			</svg>
		</a>
	</div>
</article>
