<script>
	import CodePreview from '$lib/components/CodePreview.svelte';
</script>

<svelte:head>
	<title>Next.js データ取得 | さとまたラボ</title>
</svelte:head>

<article>
	<h1 class="text-3xl font-bold mb-2">データ取得</h1>
	<p class="text-lg text-gray-600 dark:text-gray-400 mb-8">
		Server Componentsでのデータフェッチング
	</p>

	<section class="mb-10">
		<h2 id="server-fetch" class="text-xl font-bold mb-4">サーバーコンポーネントでのfetch</h2>

		<CodePreview
			title="async コンポーネント"
			description="サーバー上で直接データ取得"
			language="typescript"
			code={`// app/posts/page.tsx
async function getPosts() {
  const res = await fetch('https://api.example.com/posts');
  return res.json();
}

export default async function PostsPage() {
  const posts = await getPosts();

  return (
    <ul>
      {posts.map((post) => (
        <li key={post.id}>{post.title}</li>
      ))}
    </ul>
  );
}`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div style="color:#6a9955;">// Server Component なので</div><div style="color:#6a9955;">// - APIキーが漏れない</div><div style="color:#6a9955;">// - DBに直接アクセス可能</div><div style="color:#6a9955;">// - 初回表示が速い</div></div>`}
		/>
	</section>

	<section class="mb-10">
		<h2 id="caching" class="text-xl font-bold mb-4">キャッシュとrevalidate</h2>

		<CodePreview
			title="キャッシュの制御"
			description="データの鮮度を管理"
			language="typescript"
			code={`// デフォルト: キャッシュされる
const res = await fetch('https://...');

// キャッシュしない（毎回リクエスト）
const res = await fetch('https://...', {
  cache: 'no-store'
});

// 一定時間後に再検証
const res = await fetch('https://...', {
  next: { revalidate: 60 }  // 60秒後に再検証
});

// ページ全体のrevalidate
export const revalidate = 60;`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div><span style="color:#ce9178;">'force-cache'</span> <span style="color:#6a9955;">// キャッシュ優先</span></div><div><span style="color:#ce9178;">'no-store'</span> <span style="color:#6a9955;">// 常に新しいデータ</span></div><div><span style="color:#9cdcfe;">revalidate: 60</span> <span style="color:#6a9955;">// 60秒ごと更新</span></div></div>`}
		/>
	</section>

	<section class="mb-10">
		<h2 id="parallel" class="text-xl font-bold mb-4">並列データ取得</h2>

		<CodePreview
			title="Promise.all で高速化"
			description="複数のリクエストを同時実行"
			language="typescript"
			code={`// app/dashboard/page.tsx
async function getUser() {
  const res = await fetch('https://api.example.com/user');
  return res.json();
}

async function getPosts() {
  const res = await fetch('https://api.example.com/posts');
  return res.json();
}

export default async function Dashboard() {
  // 並列で取得（速い！）
  const [user, posts] = await Promise.all([
    getUser(),
    getPosts()
  ]);

  return (
    <div>
      <h1>{user.name}さんのダッシュボード</h1>
      <PostList posts={posts} />
    </div>
  );
}`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div style="color:#6a9955;">// 順番に取得: 2秒 + 2秒 = 4秒</div><div style="color:#6a9955;">// 並列で取得: max(2秒, 2秒) = 2秒</div></div>`}
		/>
	</section>

	<section class="mb-10">
		<h2 id="dynamic-params" class="text-xl font-bold mb-4">動的パラメータを使った取得</h2>

		<CodePreview
			title="paramsを使ったデータ取得"
			description="URLパラメータでAPIを呼び出す"
			language="typescript"
			code={`// app/blog/[slug]/page.tsx
interface Props {
  params: { slug: string }
}

async function getPost(slug: string) {
  const res = await fetch(
    \`https://api.example.com/posts/\${slug}\`
  );

  if (!res.ok) {
    notFound();  // 404ページを表示
  }

  return res.json();
}

export default async function BlogPost({ params }: Props) {
  const post = await getPost(params.slug);

  return (
    <article>
      <h1>{post.title}</h1>
      <p>{post.content}</p>
    </article>
  );
}`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div>/blog/hello-world</div><div style="color:#6a9955;">// → getPost("hello-world")</div><div style="color:#6a9955;">// → API: /posts/hello-world</div></div>`}
		/>
	</section>

	<section class="mb-10">
		<h2 id="loading" class="text-xl font-bold mb-4">ローディング状態</h2>

		<CodePreview
			title="loading.tsx"
			description="自動的にローディングUIを表示"
			language="typescript"
			code={`// app/posts/loading.tsx
export default function Loading() {
  return (
    <div className="animate-pulse">
      <div className="h-4 bg-gray-200 rounded w-3/4 mb-4"></div>
      <div className="h-4 bg-gray-200 rounded w-1/2 mb-4"></div>
      <div className="h-4 bg-gray-200 rounded w-5/6"></div>
    </div>
  );
}

// app/posts/page.tsx はそのまま
// データ取得中は自動的にloading.tsxが表示される`}
			previewHtml={`<div class="animate-pulse space-y-3"><div style="height:16px;background:#e5e7eb;border-radius:4px;width:75%;"></div><div style="height:16px;background:#e5e7eb;border-radius:4px;width:50%;"></div><div style="height:16px;background:#e5e7eb;border-radius:4px;width:83%;"></div></div>`}
		/>

		<CodePreview
			title="Suspenseで部分的にローディング"
			description="コンポーネント単位でローディングを制御"
			language="typescript"
			code={`import { Suspense } from 'react';

export default function Page() {
  return (
    <div>
      <h1>ダッシュボード</h1>

      {/* このコンポーネントだけローディング */}
      <Suspense fallback={<p>投稿を読み込み中...</p>}>
        <PostList />
      </Suspense>

      {/* これはすぐ表示される */}
      <Sidebar />
    </div>
  );
}`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div style="color:#6a9955;">// Suspenseで囲んだ部分だけ</div><div style="color:#6a9955;">// 待っている間 fallback を表示</div></div>`}
		/>
	</section>

	<section class="mb-10">
		<h2 id="error" class="text-xl font-bold mb-4">エラーハンドリング</h2>

		<CodePreview
			title="error.tsx"
			description="エラー時のフォールバックUI"
			language="typescript"
			code={`// app/posts/error.tsx
'use client';

interface Props {
  error: Error;
  reset: () => void;
}

export default function Error({ error, reset }: Props) {
  return (
    <div>
      <h2>エラーが発生しました</h2>
      <p>{error.message}</p>
      <button onClick={() => reset()}>
        もう一度試す
      </button>
    </div>
  );
}`}
			previewHtml={`<div style="padding:16px;background:#fef2f2;border:1px solid #fecaca;border-radius:8px;"><h2 style="color:#dc2626;font-weight:bold;margin-bottom:8px;">エラーが発生しました</h2><p style="color:#7f1d1d;font-size:14px;margin-bottom:12px;">データの取得に失敗しました</p><button style="padding:8px 16px;background:#dc2626;color:white;border:none;border-radius:4px;cursor:pointer;">もう一度試す</button></div>`}
		/>
	</section>

	<div class="flex justify-between pt-6 border-t border-gray-200 dark:border-gray-700">
		<a href="/nextjs/routing" class="inline-flex items-center gap-2 px-4 py-2 rounded-lg border border-gray-300 dark:border-gray-600 hover:bg-gray-100 dark:hover:bg-gray-800 transition-colors">
			<svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
				<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 19l-7-7 7-7" />
			</svg>
			前へ：ルーティング
		</a>
		<a href="/nextjs/api-routes" class="inline-flex items-center gap-2 px-4 py-2 rounded-lg bg-primary-600 text-white hover:bg-primary-700 transition-colors">
			次へ：API Routes
			<svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
				<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 5l7 7-7 7" />
			</svg>
		</a>
	</div>
</article>
