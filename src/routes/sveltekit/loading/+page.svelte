<script>
	import CodePreview from '$lib/components/CodePreview.svelte';
</script>

<svelte:head>
	<title>SvelteKit データ読み込み | さとまたラボ</title>
</svelte:head>

<article>
	<h1 class="text-3xl font-bold mb-2">データ読み込み</h1>
	<p class="text-lg text-gray-600 dark:text-gray-400 mb-8">
		load関数でページにデータを渡す
	</p>

	<!-- load関数とは -->
	<section class="mb-10">
		<h2 id="what-is" class="text-xl font-bold mb-4">load関数とは？</h2>

		<div class="p-6 rounded-xl bg-blue-50 dark:bg-blue-900/20 border border-blue-200 dark:border-blue-800 mb-6">
			<p class="text-blue-800 dark:text-blue-200 mb-4">
				<strong>日常での例え：</strong>レストランのキッチン
			</p>
			<div class="text-sm text-blue-700 dark:text-blue-300 space-y-2">
				<p>お客さん（ブラウザ）が「このページください」と注文</p>
				<p>キッチン（load関数）が裏で材料（データ）を準備</p>
				<p>準備できたら、盛り付けて（ページに渡して）提供</p>
			</div>
		</div>

		<div class="p-4 rounded-lg bg-amber-50 dark:bg-amber-900/20 border border-amber-200 dark:border-amber-800 mb-6">
			<p class="font-semibold text-amber-800 dark:text-amber-200">なぜload関数が必要？</p>
			<div class="text-sm text-amber-700 dark:text-amber-300 mt-2">
				<p class="mb-2"><strong>ページを表示する前にデータが必要な時</strong>に使います：</p>
				<ul class="list-disc list-inside space-y-1 mb-3">
					<li>ブログ記事一覧をデータベースから取得</li>
					<li>ログイン中のユーザー情報をチェック</li>
					<li>外部APIからデータを取得</li>
				</ul>
				<p><strong>メリット</strong>：サーバーで実行されるので、APIキーやDB接続が安全！</p>
			</div>
		</div>
	</section>

	<section class="mb-10">
		<h2 id="server-load" class="text-xl font-bold mb-4">サーバーサイドload</h2>

		<CodePreview
			title="+page.server.ts"
			description="サーバー上でデータを取得"
			language="typescript"
			code={`// src/routes/posts/+page.server.ts
export async function load() {
  const posts = await db.post.findMany();

  return {
    posts
  };
}

// +page.svelte で使う
// let { data } = $props();
// data.posts でアクセス`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div style="color:#6a9955;">// サーバーでのみ実行</div><div style="color:#6a9955;">// - DBに直接アクセス可能</div><div style="color:#6a9955;">// - APIキーが漏れない</div></div>`}
		/>

		<CodePreview
			title="ページでデータを受け取る"
			description="$propsでdataを取得"
			language="svelte"
			code={`<!-- src/routes/posts/+page.svelte -->
<script>
  let { data } = $props();
</script>

<h1>投稿一覧</h1>
<ul>
  {#each data.posts as post}
    <li>{post.title}</li>
  {/each}
</ul>`}
			previewHtml={`<div><h1 style="font-size:20px;font-weight:bold;margin-bottom:8px;">投稿一覧</h1><ul style="list-style:disc;margin-left:20px;"><li>投稿タイトル1</li><li>投稿タイトル2</li><li>投稿タイトル3</li></ul></div>`}
		/>
	</section>

	<section class="mb-10">
		<h2 id="params" class="text-xl font-bold mb-4">パラメータとURL情報</h2>

		<CodePreview
			title="load関数の引数"
			description="params, url, cookies など"
			language="typescript"
			code={`// src/routes/blog/[slug]/+page.server.ts
export async function load({ params, url, cookies }) {
  // URLパラメータ
  const { slug } = params;

  // クエリパラメータ
  const page = url.searchParams.get('page') || '1';

  // Cookie
  const token = cookies.get('session');

  const post = await getPost(slug);

  return { post, page };
}`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div><span style="color:#9cdcfe;">params</span>.slug <span style="color:#6a9955;">// URLパラメータ</span></div><div><span style="color:#9cdcfe;">url</span>.searchParams <span style="color:#6a9955;">// クエリ</span></div><div><span style="color:#9cdcfe;">cookies</span>.get() <span style="color:#6a9955;">// Cookie</span></div></div>`}
		/>
	</section>

	<section class="mb-10">
		<h2 id="universal-load" class="text-xl font-bold mb-4">ユニバーサルload</h2>

		<CodePreview
			title="+page.ts"
			description="サーバーとクライアント両方で実行"
			language="typescript"
			code={`// src/routes/posts/+page.ts
export async function load({ fetch }) {
  // fetchはSvelteKitが提供する特別な関数
  // サーバーでもクライアントでも動作する
  const response = await fetch('/api/posts');
  const posts = await response.json();

  return { posts };
}

// +page.server.ts との違い:
// - サーバーとクライアント両方で実行可能
// - DB直接アクセスはできない
// - ナビゲーション時はクライアントで実行`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div style="color:#6a9955;">// +page.server.ts → サーバーのみ</div><div style="color:#6a9955;">// +page.ts → サーバー & クライアント</div></div>`}
		/>
	</section>

	<section class="mb-10">
		<h2 id="layout-load" class="text-xl font-bold mb-4">レイアウトでのデータ読み込み</h2>

		<CodePreview
			title="+layout.server.ts"
			description="子ルート全体で共有するデータ"
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

{#if data.user}
  <p>ようこそ、{data.user.name}さん</p>
{/if}

{@render children()}`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div style="color:#6a9955;">// レイアウトのloadは</div><div style="color:#6a9955;">// 子ページ全てで使える</div></div>`}
		/>
	</section>

	<section class="mb-10">
		<h2 id="error" class="text-xl font-bold mb-4">エラーハンドリング</h2>

		<CodePreview
			title="error関数"
			description="エラーをスローしてエラーページを表示"
			language="typescript"
			code={`// src/routes/blog/[slug]/+page.server.ts
import { error } from '@sveltejs/kit';

export async function load({ params }) {
  const post = await getPost(params.slug);

  if (!post) {
    error(404, {
      message: '記事が見つかりません'
    });
  }

  return { post };
}

// +error.svelte でエラーを表示`}
			previewHtml={`<div style="padding:16px;background:#fef2f2;border:1px solid #fecaca;border-radius:8px;"><h2 style="color:#dc2626;font-weight:bold;margin-bottom:8px;">404</h2><p style="color:#7f1d1d;font-size:14px;">記事が見つかりません</p></div>`}
		/>

		<CodePreview
			title="+error.svelte"
			description="エラーページの定義"
			language="svelte"
			code={`<!-- src/routes/+error.svelte -->
<script>
  import { page } from '$app/stores';
</script>

<h1>{$page.status}</h1>
<p>{$page.error?.message}</p>

<a href="/">ホームに戻る</a>`}
			previewHtml={`<div style="text-align:center;padding:24px;"><h1 style="font-size:48px;font-weight:bold;color:#dc2626;">404</h1><p style="color:#6b7280;margin-bottom:16px;">ページが見つかりません</p><a href="#" style="color:#3b82f6;text-decoration:underline;">ホームに戻る</a></div>`}
		/>
	</section>

	<section class="mb-10">
		<h2 id="redirect" class="text-xl font-bold mb-4">リダイレクト</h2>

		<CodePreview
			title="redirect関数"
			description="別ページへリダイレクト"
			language="typescript"
			code={`// src/routes/dashboard/+page.server.ts
import { redirect } from '@sveltejs/kit';

export async function load({ cookies }) {
  const session = cookies.get('session');

  if (!session) {
    // 未ログインならログインページへ
    redirect(303, '/login');
  }

  const user = await getUser(session);
  return { user };
}`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div><span style="color:#dcdcaa;">redirect</span>(303, '/login')</div><div style="color:#6a9955;">// 303: See Other（POST後のリダイレクト）</div><div style="color:#6a9955;">// 307: Temporary Redirect</div></div>`}
		/>
	</section>

	<div class="flex justify-between pt-6 border-t border-gray-200 dark:border-gray-700">
		<a href="/sveltekit/routing" class="inline-flex items-center gap-2 px-4 py-2 rounded-lg border border-gray-300 dark:border-gray-600 hover:bg-gray-100 dark:hover:bg-gray-800 transition-colors">
			<svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
				<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 19l-7-7 7-7" />
			</svg>
			前へ：ルーティング
		</a>
		<a href="/sveltekit/forms" class="inline-flex items-center gap-2 px-4 py-2 rounded-lg bg-primary-600 text-white hover:bg-primary-700 transition-colors">
			次へ：フォームアクション
			<svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
				<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 5l7 7-7 7" />
			</svg>
		</a>
	</div>
</article>
