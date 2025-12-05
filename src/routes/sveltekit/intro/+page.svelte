<script>
	import CodePreview from '$lib/components/CodePreview.svelte';
	import FeatureCard from '$lib/components/FeatureCard.svelte';

	const features = [
		{ icon: '⚡', title: '高速パフォーマンス', description: 'コンパイル時に最適化、小さなバンドル', tag: '特徴' },
		{ icon: '📁', title: 'ファイルベースルーティング', description: 'routes/フォルダがそのままURL', tag: '基本' },
		{ icon: '📝', title: 'シンプルな構文', description: '学習コストが低く、直感的', tag: '特徴' },
		{ icon: '🔄', title: 'リアクティビティ', description: '$stateで状態管理が簡単', tag: 'Svelte 5' },
		{ icon: '📦', title: 'load関数', description: 'サーバーでデータ取得', tag: '重要' },
		{ icon: '📋', title: 'Form Actions', description: 'フォーム処理が簡単', tag: '便利' }
	];
</script>

<svelte:head>
	<title>SvelteKit はじめに | さとまたラボ</title>
</svelte:head>

<article>
	<h1 class="text-3xl font-bold mb-2">SvelteKit</h1>
	<p class="text-lg text-gray-600 dark:text-gray-400 mb-8">
		シンプルで高速なWebアプリケーションフレームワーク
	</p>

	<!-- SvelteKitとは -->
	<section class="mb-10">
		<h2 id="what-is" class="text-xl font-bold mb-4">SvelteKitとは？</h2>

		<div class="p-6 rounded-xl bg-blue-50 dark:bg-blue-900/20 border border-blue-200 dark:border-blue-800 mb-6">
			<p class="text-blue-800 dark:text-blue-200 mb-4">
				<strong>日常での例え：</strong>「家具付きマンション」
			</p>
			<div class="grid grid-cols-1 md:grid-cols-2 gap-4 text-sm">
				<div class="p-3 bg-white dark:bg-gray-800 rounded-lg">
					<div class="font-semibold text-blue-700 dark:text-blue-300 mb-2">素のJavaScript = 空き地</div>
					<p class="text-gray-600 dark:text-gray-400">
						自由だけど、家を建てる道具も<br>
						材料も全部自分で用意が必要
					</p>
				</div>
				<div class="p-3 bg-white dark:bg-gray-800 rounded-lg">
					<div class="font-semibold text-blue-700 dark:text-blue-300 mb-2">SvelteKit = 家具付きマンション</div>
					<p class="text-gray-600 dark:text-gray-400">
						ルーティング、データ取得、ビルド設定...<br>
						必要なものが最初から揃っている
					</p>
				</div>
			</div>
		</div>

		<div class="p-4 rounded-lg bg-amber-50 dark:bg-amber-900/20 border border-amber-200 dark:border-amber-800 mb-6">
			<p class="font-semibold text-amber-800 dark:text-amber-200">「フレームワーク」とは？なぜ使う？</p>
			<div class="text-sm text-amber-700 dark:text-amber-300 mt-2">
				<p class="mb-2"><strong>フレームワーク</strong>= Webアプリを作るための「土台」や「骨組み」</p>
				<p class="mb-2"><strong>フレームワークなしで作ると：</strong></p>
				<ul class="list-disc list-inside space-y-1 mb-3">
					<li>ページ遷移の仕組みを自作する必要がある</li>
					<li>ビルド設定（Webpack等）を自分で書く必要がある</li>
					<li>SEO対策、パフォーマンス最適化も全部自分で</li>
				</ul>
				<p><strong>SvelteKitなら：</strong>これらが最初から用意されている！コードを書くことに集中できる</p>
			</div>
		</div>

		<div class="p-4 rounded-lg bg-gray-100 dark:bg-gray-800 mb-6">
			<p class="font-semibold text-gray-800 dark:text-gray-200 mb-2">SvelteとSvelteKitの違い</p>
			<div class="text-sm text-gray-700 dark:text-gray-300">
				<p><strong>Svelte</strong>：UIコンポーネントを作るためのライブラリ</p>
				<p><strong>SvelteKit</strong>：Svelteを使ったアプリを作るためのフレームワーク（ルーティング、ビルド等含む）</p>
				<p class="mt-2 text-gray-500 dark:text-gray-400">例えるなら：Svelte = レンガ、SvelteKit = レンガで家を建てる設計図と道具セット</p>
			</div>
		</div>
	</section>

	<!-- できること一覧 -->
	<section class="mb-10">
		<h2 id="features" class="text-xl font-bold mb-4">SvelteKitでできること</h2>
		<div class="grid grid-cols-1 md:grid-cols-2 gap-3">
			{#each features as feature}
				<FeatureCard {...feature} />
			{/each}
		</div>
	</section>

	<!-- コード例 -->
	<section class="mb-10">
		<h2 id="examples" class="text-xl font-bold mb-4">コード例</h2>

		<CodePreview
			title="プロジェクト作成"
			description="npx sv createで開始"
			language="bash"
			code={`# プロジェクト作成
npx sv create my-app

# 開発サーバー起動
cd my-app
npm install
npm run dev`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div style="color:#6a9955;">✓ Project created</div><div style="color:#569cd6;">➜ Local: http://localhost:5173</div></div>`}
		/>

		<CodePreview
			title="基本的なページ"
			description="Svelteコンポーネントの構造"
			language="svelte"
			code={`<!-- routes/+page.svelte -->
<script>
  let count = $state(0);

  function increment() {
    count++;
  }
</script>

<h1>Welcome to SvelteKit</h1>
<p>カウント: {count}</p>
<button onclick={increment}>+1</button>

<style>
  h1 { color: #ff3e00; }
  button {
    padding: 8px 16px;
    background: #ff3e00;
    color: white;
    border: none;
    border-radius: 4px;
  }
</style>`}
			previewHtml={`<div style="padding:16px;"><h1 style="color:#ff3e00;font-size:24px;margin-bottom:8px;">Welcome to SvelteKit</h1><p style="margin-bottom:8px;">カウント: 0</p><button style="padding:8px 16px;background:#ff3e00;color:white;border:none;border-radius:4px;cursor:pointer;">+1</button></div>`}
		/>

		<div class="mt-4 p-4 rounded-lg bg-gray-50 dark:bg-gray-800/50 border border-gray-200 dark:border-gray-700">
			<p class="font-semibold text-gray-800 dark:text-gray-200 mb-3">コード解説：Svelteファイルの3つの部分</p>
			<div class="text-sm text-gray-700 dark:text-gray-300 space-y-3">
				<div class="p-3 bg-blue-50 dark:bg-blue-900/20 rounded-lg">
					<p class="font-medium text-blue-700 dark:text-blue-300 mb-1">① &lt;script&gt; - JavaScript（ロジック）</p>
					<p><code class="bg-blue-100 dark:bg-blue-800 px-1 rounded">let count = $state(0)</code>：変数を作成（初期値0）</p>
					<p><code class="bg-blue-100 dark:bg-blue-800 px-1 rounded">function increment()</code>：ボタンクリック時に呼ばれる関数</p>
				</div>
				<div class="p-3 bg-green-50 dark:bg-green-900/20 rounded-lg">
					<p class="font-medium text-green-700 dark:text-green-300 mb-1">② HTML部分 - 画面表示</p>
					<p><code class="bg-green-100 dark:bg-green-800 px-1 rounded">{'{count}'}</code>：変数の値を表示（変数が変わると自動更新）</p>
					<p><code class="bg-green-100 dark:bg-green-800 px-1 rounded">onclick={'{increment}'}</code>：クリック時にincrement関数を実行</p>
				</div>
				<div class="p-3 bg-purple-50 dark:bg-purple-900/20 rounded-lg">
					<p class="font-medium text-purple-700 dark:text-purple-300 mb-1">③ &lt;style&gt; - CSS（見た目）</p>
					<p>このコンポーネント専用のスタイル。他のページには影響しません。</p>
				</div>
			</div>
		</div>

		<CodePreview
			title="リアクティビティ（Svelte 5）"
			description="$stateと$derivedで状態管理"
			language="svelte"
			code={`<script>
  // リアクティブな状態
  let count = $state(0);
  let name = $state('');

  // 派生値（countが変わると自動更新）
  let doubled = $derived(count * 2);

  // エフェクト（依存値が変わると実行）
  $effect(() => {
    console.log('Count changed:', count);
  });
</script>

<input bind:value={name} placeholder="名前">
<p>こんにちは、{name || 'ゲスト'}さん</p>
<p>Count: {count}, Doubled: {doubled}</p>`}
			previewHtml={`<div style="padding:16px;"><input style="padding:8px;border:1px solid #d1d5db;border-radius:4px;margin-bottom:8px;width:200px;" placeholder="名前"><p style="margin-bottom:4px;">こんにちは、ゲストさん</p><p>Count: 0, Doubled: 0</p></div>`}
		/>

		<div class="mt-4 p-4 rounded-lg bg-gray-50 dark:bg-gray-800/50 border border-gray-200 dark:border-gray-700">
			<p class="font-semibold text-gray-800 dark:text-gray-200 mb-3">コード解説：Svelte 5の「Runes」</p>
			<div class="text-sm text-gray-700 dark:text-gray-300 space-y-3">
				<div>
					<p class="font-medium text-orange-600 dark:text-orange-400 mb-1">$state - 変更を追跡する変数</p>
					<div class="bg-gray-100 dark:bg-gray-800 p-2 rounded text-xs font-mono mb-1">let count = $state(0);</div>
					<p>この変数が変わると、使っている場所すべてが自動で再描画されます。</p>
				</div>
				<div>
					<p class="font-medium text-orange-600 dark:text-orange-400 mb-1">$derived - 他の値から計算される値</p>
					<div class="bg-gray-100 dark:bg-gray-800 p-2 rounded text-xs font-mono mb-1">let doubled = $derived(count * 2);</div>
					<p><code>count</code>が1になったら、<code>doubled</code>は自動的に2になります。手動で更新する必要なし！</p>
				</div>
				<div>
					<p class="font-medium text-orange-600 dark:text-orange-400 mb-1">bind:value - 双方向バインディング</p>
					<div class="bg-gray-100 dark:bg-gray-800 p-2 rounded text-xs font-mono mb-1">&lt;input bind:value={'{name}'}&gt;</div>
					<p>入力欄に文字を打つと<code>name</code>変数が自動更新。<code>name</code>を変えると入力欄の内容も変わります。</p>
				</div>
				<div>
					<p class="font-medium text-orange-600 dark:text-orange-400 mb-1">{'{name || "ゲスト"}'} - 条件付き表示</p>
					<p><code>name</code>が空（未入力）の時は「ゲスト」を表示。入力があればその名前を表示します。</p>
				</div>
			</div>
		</div>

		<CodePreview
			title="データ取得（load関数）"
			description="+page.server.tsでサーバーサイド取得"
			language="typescript"
			code={`// routes/posts/+page.server.ts
export async function load() {
  const res = await fetch('https://api.example.com/posts');
  const posts = await res.json();

  return {
    posts  // ページコンポーネントで使える
  };
}

// routes/posts/+page.svelte
<script>
  let { data } = $props();
</script>

{#each data.posts as post}
  <article>
    <h2>{post.title}</h2>
  </article>
{/each}`}
			previewHtml={`<div style="padding:16px;"><article style="padding:12px;border:1px solid #e5e7eb;border-radius:8px;margin-bottom:8px;"><h2 style="font-weight:bold;">記事タイトル1</h2></article><article style="padding:12px;border:1px solid #e5e7eb;border-radius:8px;"><h2 style="font-weight:bold;">記事タイトル2</h2></article></div>`}
		/>

		<div class="mt-4 p-4 rounded-lg bg-gray-50 dark:bg-gray-800/50 border border-gray-200 dark:border-gray-700">
			<p class="font-semibold text-gray-800 dark:text-gray-200 mb-3">コード解説：サーバーとページの連携</p>
			<div class="text-sm text-gray-700 dark:text-gray-300 space-y-3">
				<div class="p-3 bg-cyan-50 dark:bg-cyan-900/20 rounded-lg">
					<p class="font-medium text-cyan-700 dark:text-cyan-300 mb-2">ステップ1：サーバー側でデータ取得（+page.server.ts）</p>
					<div class="space-y-1">
						<p><code class="bg-cyan-100 dark:bg-cyan-800 px-1 rounded">export async function load()</code>：ページが開かれる前に実行される</p>
						<p><code class="bg-cyan-100 dark:bg-cyan-800 px-1 rounded">await fetch(...)</code>：APIからデータを取得（サーバー側で実行）</p>
						<p><code class="bg-cyan-100 dark:bg-cyan-800 px-1 rounded">return {'{posts}'}</code>：取得したデータをページに渡す</p>
					</div>
				</div>
				<div class="p-3 bg-emerald-50 dark:bg-emerald-900/20 rounded-lg">
					<p class="font-medium text-emerald-700 dark:text-emerald-300 mb-2">ステップ2：ページ側でデータ受け取り（+page.svelte）</p>
					<div class="space-y-1">
						<p><code class="bg-emerald-100 dark:bg-emerald-800 px-1 rounded">let {'{data}'} = $props()</code>：load関数が返したデータを受け取る</p>
						<p><code class="bg-emerald-100 dark:bg-emerald-800 px-1 rounded">data.posts</code>：load関数で return したpostsにアクセス</p>
					</div>
				</div>
				<div class="pt-2 border-t border-gray-200 dark:border-gray-600">
					<p class="font-medium text-gray-600 dark:text-gray-400 mb-1">処理の流れ</p>
					<p>1. ユーザーが /posts にアクセス → 2. load関数がサーバーで実行 → 3. APIからデータ取得 → 4. ページに渡される → 5. 画面表示</p>
				</div>
			</div>
		</div>

		<CodePreview
			title="Form Actions"
			description="サーバーサイドでフォーム処理"
			language="svelte"
			code={`// routes/login/+page.server.ts
export const actions = {
  default: async ({ request }) => {
    const data = await request.formData();
    const email = data.get('email');
    const password = data.get('password');

    // 認証処理...

    return { success: true };
  }
};

// routes/login/+page.svelte
<form method="POST">
  <input name="email" type="email" required>
  <input name="password" type="password" required>
  <button type="submit">ログイン</button>
</form>`}
			previewHtml={`<form style="padding:16px;display:flex;flex-direction:column;gap:8px;max-width:250px;"><input style="padding:8px;border:1px solid #d1d5db;border-radius:4px;" placeholder="メールアドレス"><input style="padding:8px;border:1px solid #d1d5db;border-radius:4px;" type="password" placeholder="パスワード"><button style="padding:8px 16px;background:#ff3e00;color:white;border:none;border-radius:4px;cursor:pointer;">ログイン</button></form>`}
		/>

		<CodePreview
			title="レイアウト"
			description="+layout.svelteで共通UI"
			language="svelte"
			code={`<!-- routes/+layout.svelte -->
<script>
  let { children } = $props();
</script>

<header>
  <nav>
    <a href="/">Home</a>
    <a href="/about">About</a>
  </nav>
</header>

<main>
  {@render children()}
</main>

<footer>
  © 2024 My App
</footer>`}
			previewHtml={`<div style="border:1px solid #e5e7eb;border-radius:8px;overflow:hidden;"><header style="background:#f3f4f6;padding:8px 16px;border-bottom:1px solid #e5e7eb;"><a href="/" style="margin-right:16px;color:#ff3e00;">Home</a><a href="/about" style="color:#ff3e00;">About</a></header><main style="padding:16px;min-height:60px;">ページ内容</main><footer style="background:#f3f4f6;padding:8px 16px;text-align:center;border-top:1px solid #e5e7eb;font-size:12px;">© 2024 My App</footer></div>`}
		/>

		<CodePreview
			title="条件分岐とループ"
			description="Svelteのテンプレート構文"
			language="svelte"
			code={`<script>
  let items = $state(['りんご', 'バナナ', 'オレンジ']);
  let show = $state(true);
</script>

<!-- 条件分岐 -->
{#if show}
  <p>表示中</p>
{:else}
  <p>非表示</p>
{/if}

<!-- ループ -->
<ul>
  {#each items as item, index}
    <li>{index + 1}. {item}</li>
  {/each}
</ul>`}
			previewHtml={`<div style="padding:16px;"><p style="margin-bottom:8px;">表示中</p><ul style="list-style:none;padding:0;"><li>1. りんご</li><li>2. バナナ</li><li>3. オレンジ</li></ul></div>`}
		/>

		<div class="mt-4 p-4 rounded-lg bg-gray-50 dark:bg-gray-800/50 border border-gray-200 dark:border-gray-700">
			<p class="font-semibold text-gray-800 dark:text-gray-200 mb-3">コード解説：どのように動作するか</p>
			<div class="text-sm text-gray-700 dark:text-gray-300 space-y-4">
				<div>
					<p class="font-medium text-purple-600 dark:text-purple-400 mb-1">① 変数の準備（&lt;script&gt;内）</p>
					<div class="bg-gray-100 dark:bg-gray-800 p-2 rounded text-xs font-mono mb-2">
						let items = $state(['りんご', 'バナナ', 'オレンジ']);
					</div>
					<p><code class="bg-gray-200 dark:bg-gray-700 px-1 rounded">$state([...])</code> で配列を作成。これにより、配列が変更されると自動的に画面も更新されます。</p>
				</div>
				<div>
					<p class="font-medium text-purple-600 dark:text-purple-400 mb-1">② 条件分岐（{'{#if}'} 〜 {'{/if}'}）</p>
					<div class="bg-gray-100 dark:bg-gray-800 p-2 rounded text-xs font-mono mb-2">
						{'{#if show}'}<br>
						&nbsp;&nbsp;&lt;p&gt;表示中&lt;/p&gt; ← showがtrueの時に表示<br>
						{'{:else}'}<br>
						&nbsp;&nbsp;&lt;p&gt;非表示&lt;/p&gt; ← showがfalseの時に表示<br>
						{'{/if}'}
					</div>
					<p><code class="bg-gray-200 dark:bg-gray-700 px-1 rounded">show = true</code> なので「表示中」が表示されています。</p>
				</div>
				<div>
					<p class="font-medium text-purple-600 dark:text-purple-400 mb-1">③ ループ（{'{#each}'} 〜 {'{/each}'}）</p>
					<div class="bg-gray-100 dark:bg-gray-800 p-2 rounded text-xs font-mono mb-2">
						{'{#each items as item, index}'}<br>
						&nbsp;&nbsp;&lt;li&gt;{'{index + 1}'}. {'{item}'}&lt;/li&gt;<br>
						{'{/each}'}
					</div>
					<p class="mb-2"><code class="bg-gray-200 dark:bg-gray-700 px-1 rounded">items</code> の各要素を順番に処理：</p>
					<ul class="list-disc list-inside space-y-1 ml-2">
						<li><code>item</code>：現在の要素（「りんご」「バナナ」「オレンジ」）</li>
						<li><code>index</code>：順番（0, 1, 2）→ +1して「1, 2, 3」として表示</li>
					</ul>
				</div>
				<div class="pt-2 border-t border-gray-200 dark:border-gray-600">
					<p class="font-medium text-green-600 dark:text-green-400 mb-1">結果の組み立て</p>
					<p>配列を1つずつ処理して、<code>&lt;li&gt;1. りんご&lt;/li&gt;</code>、<code>&lt;li&gt;2. バナナ&lt;/li&gt;</code>、<code>&lt;li&gt;3. オレンジ&lt;/li&gt;</code> が順番に生成されます。</p>
				</div>
			</div>
		</div>
	</section>

	<!-- ディレクトリ構造 -->
	<section class="mb-10">
		<h2 id="structure" class="text-xl font-bold mb-4">ディレクトリ構造</h2>

		<div class="rounded-xl border border-gray-200 dark:border-gray-700 overflow-hidden bg-gray-900 p-4">
			<pre class="text-gray-100 text-sm"><code>{`my-app/
├── src/
│   ├── routes/
│   │   ├── +layout.svelte    # 共通レイアウト
│   │   ├── +page.svelte      # トップページ (/)
│   │   ├── about/
│   │   │   └── +page.svelte  # /about
│   │   └── blog/
│   │       ├── +page.svelte  # /blog
│   │       └── [slug]/
│   │           └── +page.svelte # /blog/:slug
│   ├── lib/
│   │   └── components/       # 再利用コンポーネント
│   └── app.html
├── static/                   # 静的ファイル
└── package.json`}</code></pre>
		</div>
	</section>

	<!-- ナビゲーション -->
	<div class="flex justify-between pt-6 border-t border-gray-200 dark:border-gray-700">
		<a href="/nextjs/intro" class="inline-flex items-center gap-2 px-4 py-2 rounded-lg border border-gray-300 dark:border-gray-600 hover:bg-gray-100 dark:hover:bg-gray-800 transition-colors">
			<svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
				<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 19l-7-7 7-7" />
			</svg>
			前へ：Next.js
		</a>
		<a href="/sveltekit/setup" class="inline-flex items-center gap-2 px-4 py-2 rounded-lg bg-primary-600 text-white hover:bg-primary-700 transition-colors">
			次へ：Tailwind導入
			<svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
				<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 5l7 7-7 7" />
			</svg>
		</a>
	</div>
</article>
