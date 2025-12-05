<script>
	import CodePreview from '$lib/components/CodePreview.svelte';
	import FeatureCard from '$lib/components/FeatureCard.svelte';

	const features = [
		{ icon: '📁', title: 'ファイルベースルーティング', description: 'フォルダ構造がそのままURLに', tag: '特徴' },
		{ icon: '⚡', title: 'SSR/SSG', description: 'サーバーサイドレンダリングと静的生成', tag: '重要' },
		{ icon: '🔌', title: 'API Routes', description: 'バックエンドAPIを同じプロジェクトで', tag: '便利' },
		{ icon: '🖼️', title: '画像最適化', description: 'next/imageで自動最適化', tag: '便利' },
		{ icon: '🚀', title: '自動コード分割', description: '必要なコードだけ読み込み', tag: '性能' },
		{ icon: '🔄', title: 'Server Components', description: 'サーバーで実行されるコンポーネント', tag: 'App Router' }
	];
</script>

<svelte:head>
	<title>Next.js はじめに | さとまたラボ</title>
</svelte:head>

<article>
	<h1 class="text-3xl font-bold mb-2">Next.js</h1>
	<p class="text-lg text-gray-600 dark:text-gray-400 mb-8">
		Reactベースの本格的なWebアプリケーションフレームワーク
	</p>

	<!-- Next.jsとは -->
	<section class="mb-10">
		<h2 id="what-is" class="text-xl font-bold mb-4">Next.jsとは？</h2>

		<div class="p-6 rounded-xl bg-blue-50 dark:bg-blue-900/20 border border-blue-200 dark:border-blue-800 mb-6">
			<p class="text-blue-800 dark:text-blue-200 mb-4">
				<strong>日常での例え：</strong>Reactの「フル装備版」
			</p>
			<div class="grid grid-cols-1 md:grid-cols-2 gap-4 text-sm">
				<div class="p-3 bg-white dark:bg-gray-800 rounded-lg">
					<div class="font-semibold text-blue-700 dark:text-blue-300 mb-2">React単体 = エンジンだけ</div>
					<p class="text-gray-600 dark:text-gray-400">
						UIを作る力はあるが、<br>
						ルーティングや最適化は別途必要
					</p>
				</div>
				<div class="p-3 bg-white dark:bg-gray-800 rounded-lg">
					<div class="font-semibold text-blue-700 dark:text-blue-300 mb-2">Next.js = 完成した車</div>
					<p class="text-gray-600 dark:text-gray-400">
						React + ルーティング + 最適化 +<br>
						サーバー機能がセットになっている
					</p>
				</div>
			</div>
		</div>

		<div class="p-4 rounded-lg bg-amber-50 dark:bg-amber-900/20 border border-amber-200 dark:border-amber-800 mb-6">
			<p class="font-semibold text-amber-800 dark:text-amber-200">なぜNext.jsを使う？Reactだけじゃダメ？</p>
			<div class="text-sm text-amber-700 dark:text-amber-300 mt-2">
				<p class="mb-2"><strong>Reactだけで作ると：</strong></p>
				<ul class="list-disc list-inside space-y-1 mb-3">
					<li>ルーティング（ページ遷移）を別のライブラリで追加する必要がある</li>
					<li>SEO対策が難しい（検索エンジンに内容が見えない）</li>
					<li>初期表示が遅くなりがち</li>
				</ul>
				<p><strong>Next.jsなら：</strong>これらを解決！特にSSR（サーバーサイドレンダリング）でSEOとパフォーマンスを両立</p>
			</div>
		</div>

		<div class="p-4 rounded-lg bg-gray-100 dark:bg-gray-800 mb-6">
			<p class="font-semibold text-gray-800 dark:text-gray-200 mb-2">重要な用語</p>
			<div class="text-sm text-gray-700 dark:text-gray-300 space-y-2">
				<p><strong>SSR（Server Side Rendering）</strong>：サーバーでHTMLを生成してから送る → SEOに強い、初期表示が速い</p>
				<p><strong>SSG（Static Site Generation）</strong>：ビルド時にHTMLを生成 → 最速、ブログに最適</p>
				<p><strong>App Router</strong>：Next.js 13以降の新しいルーティング方式。appフォルダを使う</p>
			</div>
		</div>
	</section>

	<!-- できること一覧 -->
	<section class="mb-10">
		<h2 id="features" class="text-xl font-bold mb-4">Next.jsでできること</h2>
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
			description="create-next-appで開始"
			language="bash"
			code={`# プロジェクト作成
npx create-next-app@latest my-app

# 開発サーバー起動
cd my-app
npm run dev`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div style="color:#6a9955;">✓ Ready in 2.1s</div><div style="color:#569cd6;">➜ Local: http://localhost:3000</div></div>`}
		/>

		<CodePreview
			title="ページコンポーネント（App Router）"
			description="app/page.tsx がトップページ"
			language="typescript"
			code={`// app/page.tsx
export default function HomePage() {
  return (
    <main>
      <h1>Welcome to Next.js!</h1>
      <p>This is the home page.</p>
    </main>
  );
}`}
			previewHtml={`<div style="padding:16px;"><h1 style="font-size:24px;font-weight:bold;margin-bottom:8px;">Welcome to Next.js!</h1><p style="color:#6b7280;">This is the home page.</p></div>`}
		/>

		<CodePreview
			title="動的ルーティング"
			description="[id]でパラメータを受け取る"
			language="typescript"
			code={`// app/blog/[slug]/page.tsx
interface Props {
  params: { slug: string }
}

export default function BlogPost({ params }: Props) {
  return (
    <article>
      <h1>記事: {params.slug}</h1>
    </article>
  );
}

// /blog/hello-world → params.slug = "hello-world"`}
			previewHtml={`<div style="padding:16px;background:#f9fafb;border-radius:8px;"><div style="font-size:12px;color:#6b7280;margin-bottom:4px;">URL: /blog/hello-world</div><h1 style="font-size:20px;font-weight:bold;">記事: hello-world</h1></div>`}
		/>

		<CodePreview
			title="データ取得（Server Component）"
			description="サーバーで直接データ取得"
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
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div style="color:#6a9955;">// Server Componentなので</div><div style="color:#6a9955;">// クライアントにAPIキーが漏れない</div></div>`}
		/>

		<CodePreview
			title="API Routes"
			description="app/api/でAPIエンドポイント作成"
			language="typescript"
			code={`// app/api/hello/route.ts
import { NextResponse } from 'next/server';

export async function GET() {
  return NextResponse.json({
    message: 'Hello from API!'
  });
}

export async function POST(request: Request) {
  const body = await request.json();
  return NextResponse.json({ received: body });
}`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div>GET /api/hello</div><div style="color:#ce9178;">&#123;"message": "Hello from API!"&#125;</div></div>`}
		/>

		<CodePreview
			title="Client Component"
			description="'use client'でインタラクティブに"
			language="typescript"
			code={`// components/Counter.tsx
'use client';

import { useState } from 'react';

export default function Counter() {
  const [count, setCount] = useState(0);

  return (
    <button onClick={() => setCount(count + 1)}>
      Count: {count}
    </button>
  );
}`}
			previewHtml={`<div style="padding:12px;"><button style="padding:8px 16px;background:#3b82f6;color:white;border:none;border-radius:4px;cursor:pointer;">Count: 0 (クリックで増加)</button></div>`}
		/>

		<CodePreview
			title="Layoutコンポーネント"
			description="共通レイアウトを定義"
			language="typescript"
			code={`// app/layout.tsx
export default function RootLayout({
  children,
}: {
  children: React.ReactNode;
}) {
  return (
    <html lang="ja">
      <body>
        <header>ヘッダー</header>
        <main>{children}</main>
        <footer>フッター</footer>
      </body>
    </html>
  );
}`}
			previewHtml={`<div style="border:1px solid #e5e7eb;border-radius:8px;overflow:hidden;"><div style="background:#f3f4f6;padding:8px;text-align:center;border-bottom:1px solid #e5e7eb;">ヘッダー</div><div style="padding:16px;text-align:center;min-height:60px;">ページ内容</div><div style="background:#f3f4f6;padding:8px;text-align:center;border-top:1px solid #e5e7eb;">フッター</div></div>`}
		/>
	</section>

	<!-- ディレクトリ構造 -->
	<section class="mb-10">
		<h2 id="structure" class="text-xl font-bold mb-4">App Routerのディレクトリ構造</h2>

		<div class="rounded-xl border border-gray-200 dark:border-gray-700 overflow-hidden bg-gray-900 p-4">
			<pre class="text-gray-100 text-sm"><code>{`my-app/
├── app/
│   ├── layout.tsx      # ルートレイアウト
│   ├── page.tsx        # トップページ (/)
│   ├── about/
│   │   └── page.tsx    # /about
│   ├── blog/
│   │   ├── page.tsx    # /blog
│   │   └── [slug]/
│   │       └── page.tsx # /blog/:slug
│   └── api/
│       └── hello/
│           └── route.ts # API: /api/hello
├── components/
├── public/
└── package.json`}</code></pre>
		</div>
	</section>

	<!-- ナビゲーション -->
	<div class="flex justify-between pt-6 border-t border-gray-200 dark:border-gray-700">
		<a href="/ts/generics" class="inline-flex items-center gap-2 px-4 py-2 rounded-lg border border-gray-300 dark:border-gray-600 hover:bg-gray-100 dark:hover:bg-gray-800 transition-colors">
			<svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
				<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 19l-7-7 7-7" />
			</svg>
			前へ：ジェネリクス
		</a>
		<a href="/nextjs/routing" class="inline-flex items-center gap-2 px-4 py-2 rounded-lg bg-primary-600 text-white hover:bg-primary-700 transition-colors">
			次へ：ルーティング
			<svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
				<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 5l7 7-7 7" />
			</svg>
		</a>
	</div>
</article>
