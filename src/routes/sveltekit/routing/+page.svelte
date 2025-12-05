<script>
	import CodePreview from '$lib/components/CodePreview.svelte';
</script>

<svelte:head>
	<title>SvelteKit ルーティング | さとまたラボ</title>
</svelte:head>

<article>
	<h1 class="text-3xl font-bold mb-2">ルーティング</h1>
	<p class="text-lg text-gray-600 dark:text-gray-400 mb-8">
		URLに応じて表示するページを切り替える仕組み
	</p>

	<!-- ルーティングとは何か？ -->
	<section class="mb-10">
		<h2 id="what-is" class="text-xl font-bold mb-4">ルーティングとは？</h2>

		<div class="p-6 rounded-xl bg-blue-50 dark:bg-blue-900/20 border border-blue-200 dark:border-blue-800 mb-6">
			<p class="text-blue-800 dark:text-blue-200 mb-4">
				<strong>日常での例え：</strong>マンションの部屋番号のようなもの
			</p>
			<div class="grid grid-cols-1 md:grid-cols-2 gap-4 text-sm">
				<div class="p-3 bg-white dark:bg-gray-800 rounded-lg">
					<div class="font-semibold text-blue-700 dark:text-blue-300">マンション</div>
					<p class="text-gray-600 dark:text-gray-400">
						101号室 → 田中さんの部屋<br>
						102号室 → 佐藤さんの部屋<br>
						201号室 → 山田さんの部屋
					</p>
				</div>
				<div class="p-3 bg-white dark:bg-gray-800 rounded-lg">
					<div class="font-semibold text-blue-700 dark:text-blue-300">Webサイト</div>
					<p class="text-gray-600 dark:text-gray-400">
						/home → トップページ<br>
						/about → 会社概要ページ<br>
						/contact → 問い合わせページ
					</p>
				</div>
			</div>
		</div>

		<div class="prose dark:prose-invert max-w-none mb-6">
			<p>
				<strong>ルーティング</strong>とは、「このURLにアクセスしたら、このページを表示する」という
				<strong>URLとページの対応付け</strong>のことです。
			</p>
		</div>

		<div class="p-4 rounded-lg bg-amber-50 dark:bg-amber-900/20 border border-amber-200 dark:border-amber-800 mb-6">
			<p class="font-semibold text-amber-800 dark:text-amber-200">なぜルーティングが必要？</p>
			<p class="text-sm text-amber-700 dark:text-amber-300 mt-2">
				ユーザーがブラウザのアドレスバーに <code class="bg-amber-200 dark:bg-amber-800 px-1 rounded">/about</code> と入力したら
				「会社概要」ページを表示し、<code class="bg-amber-200 dark:bg-amber-800 px-1 rounded">/contact</code> なら
				「問い合わせ」ページを表示する。<br>
				この「振り分け」を自動でやってくれるのがルーティングシステムです。
			</p>
		</div>
	</section>

	<!-- 基本のルーティング -->
	<section class="mb-10">
		<h2 id="basic" class="text-xl font-bold mb-4">SvelteKitのルーティング方式</h2>

		<div class="p-4 rounded-lg bg-green-50 dark:bg-green-900/20 border border-green-200 dark:border-green-800 mb-6">
			<p class="font-semibold text-green-800 dark:text-green-200">SvelteKitの便利なところ</p>
			<p class="text-sm text-green-700 dark:text-green-300 mt-2">
				<strong>フォルダを作るだけでURLが自動生成</strong>されます。<br>
				「このURLにはこのページ」という設定ファイルを書く必要がありません。
			</p>
		</div>

		<CodePreview
			title="フォルダ構造 = URL"
			description="src/routes/以下にフォルダを作ると、そのままURLになる"
			language="plaintext"
			code={`src/routes/
│
├── +page.svelte          →  https://example.com/
│                              （トップページ）
│
├── about/
│   └── +page.svelte      →  https://example.com/about
│                              （会社概要ページ）
│
├── blog/
│   └── +page.svelte      →  https://example.com/blog
│                              （ブログ一覧ページ）
│
└── contact/
    └── +page.svelte      →  https://example.com/contact
                               （問い合わせページ）`}
			previewHtml={`<div style="font-family:system-ui;padding:12px;background:#f9fafb;border-radius:8px;">
<p style="font-size:14px;margin-bottom:8px;"><strong>やること：</strong></p>
<p style="font-size:13px;color:#374151;">1. aboutフォルダを作る</p>
<p style="font-size:13px;color:#374151;">2. その中に+page.svelteを作る</p>
<p style="font-size:13px;color:#22c55e;margin-top:8px;">→ /about にアクセスできるようになる！</p>
</div>`}
		/>

		<div class="p-4 rounded-lg bg-gray-100 dark:bg-gray-800 mb-6">
			<p class="text-sm text-gray-700 dark:text-gray-300">
				<strong>+page.svelte とは？</strong><br>
				「このフォルダにアクセスした時に表示するページ」を定義するファイルです。<br>
				ファイル名の「+」は「SvelteKitの特別なファイル」という意味。必ずこの名前にします。
			</p>
		</div>
	</section>

	<!-- 動的ルーティング -->
	<section class="mb-10">
		<h2 id="dynamic" class="text-xl font-bold mb-4">動的ルーティング</h2>

		<div class="p-6 rounded-xl bg-blue-50 dark:bg-blue-900/20 border border-blue-200 dark:border-blue-800 mb-6">
			<p class="font-semibold text-blue-800 dark:text-blue-200 mb-3">問題：ブログ記事が100個あったら？</p>
			<div class="text-sm text-blue-700 dark:text-blue-300 space-y-2">
				<p>記事ごとにフォルダを作ると大変です：</p>
				<code class="block bg-white dark:bg-gray-800 p-2 rounded text-xs">
					/blog/article-1/+page.svelte<br>
					/blog/article-2/+page.svelte<br>
					/blog/article-3/+page.svelte<br>
					... 100個作る？
				</code>
				<p class="mt-3">
					<strong>解決策：</strong>「どんな記事名が来ても同じページを使う」仕組み = <strong>動的ルーティング</strong>
				</p>
			</div>
		</div>

		<div class="p-4 rounded-lg bg-amber-50 dark:bg-amber-900/20 border border-amber-200 dark:border-amber-800 mb-6">
			<p class="font-semibold text-amber-800 dark:text-amber-200">[param] とは？</p>
			<p class="text-sm text-amber-700 dark:text-amber-300 mt-2">
				<code class="bg-amber-200 dark:bg-amber-800 px-1 rounded">[slug]</code> のように角括弧で囲んだフォルダ名は
				「ここには何でも入る」という意味になります。<br>
				<strong>param</strong> = parameter（パラメータ）の略で、「変わる部分」「変数」という意味です。
			</p>
		</div>

		<CodePreview
			title="[slug] で動的なURLに対応"
			description="1つのファイルで無限のURLに対応できる"
			language="svelte"
			code={`<!-- ファイルの場所 -->
<!-- src/routes/blog/[slug]/+page.svelte -->
<!--                 ↑ ここが「何でも入る部分」 -->

<script>
  // dataの中にURLの情報が入っている
  let { data } = $props();
</script>

<!-- URLによって表示が変わる -->
<h1>記事: {data.slug}</h1>

<!--
  /blog/hello-world にアクセス
  → data.slug = "hello-world"

  /blog/my-first-post にアクセス
  → data.slug = "my-first-post"

  どんなURLでも同じファイルで対応！
-->`}
			previewHtml={`<div style="font-family:system-ui;padding:12px;background:#f9fafb;border-radius:8px;">
<p style="font-size:14px;font-weight:bold;margin-bottom:12px;">アクセス例：</p>
<div style="font-size:13px;margin-bottom:8px;">
<span style="color:#6366f1;">/blog/hello</span> → slug = "hello"
</div>
<div style="font-size:13px;margin-bottom:8px;">
<span style="color:#6366f1;">/blog/my-post</span> → slug = "my-post"
</div>
<div style="font-size:13px;">
<span style="color:#6366f1;">/blog/anything</span> → slug = "anything"
</div>
</div>`}
		/>

		<div class="p-4 rounded-lg bg-gray-100 dark:bg-gray-800 mb-6">
			<p class="text-sm text-gray-700 dark:text-gray-300">
				<strong>slugって何？</strong><br>
				URLに使う、記事を識別するための文字列です。例：<code class="bg-gray-200 dark:bg-gray-700 px-1 rounded">my-first-blog-post</code><br>
				名前は何でもOK（idやpostIdなど）。[slug]が慣例的によく使われます。
			</p>
		</div>

		<CodePreview
			title="URLから値を取得して使う"
			description="サーバー側でパラメータを受け取る"
			language="typescript"
			code={`// src/routes/blog/[slug]/+page.server.ts
// ↑ サーバーで実行されるファイル

// load関数 = ページを表示する前に実行される処理
export async function load({ params }) {
  // params.slug にURLの[slug]部分が入っている
  //
  // 例: /blog/hello-world にアクセスした場合
  //     params.slug = "hello-world"

  // この値を使ってデータベースから記事を取得
  const post = await getPostFromDatabase(params.slug);

  // ページに渡すデータを返す
  return {
    slug: params.slug,
    post: post
  };
}`}
			previewHtml={`<div style="font-family:system-ui;padding:12px;background:#f9fafb;border-radius:8px;">
<p style="font-size:14px;font-weight:bold;margin-bottom:8px;">流れ：</p>
<p style="font-size:13px;">1. ユーザーが /blog/hello にアクセス</p>
<p style="font-size:13px;">2. params.slug = "hello" で取得</p>
<p style="font-size:13px;">3. DBから"hello"の記事を探す</p>
<p style="font-size:13px;">4. 記事データをページに渡す</p>
</div>`}
		/>
	</section>

	<!-- ナビゲーション -->
	<section class="mb-10">
		<h2 id="navigation" class="text-xl font-bold mb-4">ページ間の移動</h2>

		<div class="prose dark:prose-invert max-w-none mb-6">
			<p>
				ユーザーがページを移動する方法は2つあります：
			</p>
		</div>

		<div class="grid grid-cols-1 md:grid-cols-2 gap-4 mb-6">
			<div class="p-4 rounded-lg bg-gray-100 dark:bg-gray-800">
				<h3 class="font-semibold text-gray-800 dark:text-gray-200 mb-2">1. リンクをクリック</h3>
				<p class="text-sm text-gray-600 dark:text-gray-400">
					普通の<code class="bg-gray-200 dark:bg-gray-700 px-1 rounded">&lt;a&gt;</code>タグ。
					ユーザーが自分でクリックして移動。
				</p>
			</div>
			<div class="p-4 rounded-lg bg-gray-100 dark:bg-gray-800">
				<h3 class="font-semibold text-gray-800 dark:text-gray-200 mb-2">2. プログラムで移動</h3>
				<p class="text-sm text-gray-600 dark:text-gray-400">
					ログイン成功後に自動でダッシュボードへ移動、など。
					コードで「次のページへ行け」と指示する。
				</p>
			</div>
		</div>

		<CodePreview
			title="ページ移動の2つの方法"
			description="リンクとプログラム的な遷移"
			language="svelte"
			code={`<script>
  // goto関数をインポート（プログラムで移動する用）
  import { goto } from '$app/navigation';

  async function handleLogin() {
    // ログイン処理を実行...
    const success = await login();

    if (success) {
      // ログイン成功！ダッシュボードへ自動で移動
      goto('/dashboard');
    }
  }
</script>

<!-- 方法1: 普通のリンク（ユーザーがクリック） -->
<a href="/">ホームへ</a>
<a href="/about">会社概要</a>

<!-- 方法2: ボタンを押したらプログラムで移動 -->
<button onclick={handleLogin}>
  ログイン
</button>`}
			previewHtml={`<div style="display:flex;gap:12px;flex-wrap:wrap;padding:12px;background:#f9fafb;border-radius:8px;">
<a href="#" style="color:#f97316;text-decoration:underline;">ホームへ</a>
<a href="#" style="color:#f97316;text-decoration:underline;">会社概要</a>
<button style="background:#f97316;color:white;padding:8px 16px;border:none;border-radius:4px;cursor:pointer;">ログイン</button>
</div>`}
		/>
	</section>

	<!-- 特殊ファイルの説明 -->
	<section class="mb-10">
		<h2 id="special-files" class="text-xl font-bold mb-4">SvelteKitの特別なファイル</h2>

		<div class="prose dark:prose-invert max-w-none mb-6">
			<p>
				SvelteKitでは、ファイル名に意味があります。<br>
				「+」で始まるファイルは特別な役割を持っています。
			</p>
		</div>

		<div class="space-y-3">
			<div class="p-4 rounded-lg bg-gray-100 dark:bg-gray-800">
				<code class="text-orange-600 dark:text-orange-400 font-bold">+page.svelte</code>
				<p class="text-sm text-gray-600 dark:text-gray-400 mt-1">
					<strong>ページの見た目</strong>を定義。HTMLを書くファイル。
				</p>
			</div>
			<div class="p-4 rounded-lg bg-gray-100 dark:bg-gray-800">
				<code class="text-orange-600 dark:text-orange-400 font-bold">+page.server.ts</code>
				<p class="text-sm text-gray-600 dark:text-gray-400 mt-1">
					<strong>サーバーでデータを取得</strong>する処理。DBアクセスなど。ブラウザには送られない安全なコード。
				</p>
			</div>
			<div class="p-4 rounded-lg bg-gray-100 dark:bg-gray-800">
				<code class="text-orange-600 dark:text-orange-400 font-bold">+layout.svelte</code>
				<p class="text-sm text-gray-600 dark:text-gray-400 mt-1">
					<strong>共通の枠組み</strong>（ヘッダー、サイドバーなど）。このフォルダ以下のすべてのページに適用される。
				</p>
			</div>
			<div class="p-4 rounded-lg bg-gray-100 dark:bg-gray-800">
				<code class="text-orange-600 dark:text-orange-400 font-bold">+error.svelte</code>
				<p class="text-sm text-gray-600 dark:text-gray-400 mt-1">
					<strong>エラーが起きた時</strong>に表示するページ。404や500エラー時に使われる。
				</p>
			</div>
		</div>
	</section>

	<!-- まとめ -->
	<section class="mb-10">
		<h2 id="summary" class="text-xl font-bold mb-4">まとめ</h2>

		<div class="grid grid-cols-1 md:grid-cols-2 gap-4">
			<div class="p-4 rounded-lg bg-green-50 dark:bg-green-900/20 border border-green-200 dark:border-green-800">
				<h3 class="font-semibold text-green-800 dark:text-green-200 mb-2">覚えておくこと</h3>
				<ul class="text-sm text-green-700 dark:text-green-300 space-y-1">
					<li>• フォルダを作る = URLができる</li>
					<li>• [param] = 動的に変わる部分</li>
					<li>• +page.svelte = ページの見た目</li>
					<li>• +page.server.ts = データ取得</li>
				</ul>
			</div>
			<div class="p-4 rounded-lg bg-blue-50 dark:bg-blue-900/20 border border-blue-200 dark:border-blue-800">
				<h3 class="font-semibold text-blue-800 dark:text-blue-200 mb-2">よくある使い方</h3>
				<ul class="text-sm text-blue-700 dark:text-blue-300 space-y-1">
					<li>• /blog/[slug] → 記事詳細</li>
					<li>• /users/[id] → ユーザープロフィール</li>
					<li>• /products/[productId] → 商品詳細</li>
				</ul>
			</div>
		</div>
	</section>

	<div class="flex justify-between pt-6 border-t border-gray-200 dark:border-gray-700">
		<a href="/sveltekit/setup" class="inline-flex items-center gap-2 px-4 py-2 rounded-lg border border-gray-300 dark:border-gray-600 hover:bg-gray-100 dark:hover:bg-gray-800 transition-colors">
			<svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
				<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 19l-7-7 7-7" />
			</svg>
			前へ：Tailwind導入
		</a>
		<a href="/sveltekit/loading" class="inline-flex items-center gap-2 px-4 py-2 rounded-lg bg-primary-600 text-white hover:bg-primary-700 transition-colors">
			次へ：データ読み込み
			<svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
				<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 5l7 7-7 7" />
			</svg>
		</a>
	</div>
</article>
