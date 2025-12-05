<script>
	import CodePreview from '$lib/components/CodePreview.svelte';
</script>

<svelte:head>
	<title>Next.js ルーティング | さとまたラボ</title>
</svelte:head>

<article>
	<h1 class="text-3xl font-bold mb-2">ルーティング</h1>
	<p class="text-lg text-gray-600 dark:text-gray-400 mb-8">
		App Routerのファイルベースルーティング
	</p>

	<section class="mb-10">
		<h2 id="basic" class="text-xl font-bold mb-4">基本のルーティング</h2>

		<CodePreview
			title="フォルダ = URL"
			description="app/以下のフォルダ構造がURLになる"
			language="plaintext"
			code={`app/
├── page.tsx          →  /
├── about/
│   └── page.tsx      →  /about
├── blog/
│   └── page.tsx      →  /blog
└── contact/
    └── page.tsx      →  /contact`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div>フォルダ作成 → URL自動生成</div><div style="color:#6a9955;">// 設定ファイル不要！</div></div>`}
		/>
	</section>

	<section class="mb-10">
		<h2 id="dynamic" class="text-xl font-bold mb-4">動的ルーティング</h2>

		<CodePreview
			title="[param] で動的セグメント"
			description="パラメータを含むURL"
			language="typescript"
			code={`// app/blog/[slug]/page.tsx
interface Props {
  params: { slug: string }
}

export default function BlogPost({ params }: Props) {
  // /blog/hello-world → params.slug = "hello-world"
  // /blog/nextjs-tutorial → params.slug = "nextjs-tutorial"

  return <h1>記事: {params.slug}</h1>;
}`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div>/blog/<span style="color:#4ec9b0;">[slug]</span>/page.tsx</div><div style="margin-top:8px;">/blog/hello → slug = "hello"</div><div>/blog/world → slug = "world"</div></div>`}
		/>

		<CodePreview
			title="複数のパラメータ"
			description="ネストした動的セグメント"
			language="typescript"
			code={`// app/shop/[category]/[product]/page.tsx
interface Props {
  params: {
    category: string;
    product: string;
  }
}

export default function ProductPage({ params }: Props) {
  // /shop/electronics/iphone
  // → category = "electronics", product = "iphone"

  return (
    <div>
      <p>カテゴリ: {params.category}</p>
      <p>商品: {params.product}</p>
    </div>
  );
}`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div>/shop/[category]/[product]</div><div style="margin-top:8px;color:#6a9955;">// /shop/clothes/shirt</div><div style="color:#6a9955;">// category="clothes", product="shirt"</div></div>`}
		/>

		<CodePreview
			title="[...slug] キャッチオール"
			description="複数のセグメントをまとめてキャッチ"
			language="typescript"
			code={`// app/docs/[...slug]/page.tsx
interface Props {
  params: { slug: string[] }
}

export default function DocsPage({ params }: Props) {
  // /docs/getting-started
  // → slug = ["getting-started"]

  // /docs/api/reference/auth
  // → slug = ["api", "reference", "auth"]

  return <p>パス: {params.slug.join("/")}</p>;
}`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div>/docs/<span style="color:#4ec9b0;">[...slug]</span>/page.tsx</div><div style="margin-top:8px;color:#6a9955;">// /docs/a/b/c → ["a", "b", "c"]</div></div>`}
		/>
	</section>

	<section class="mb-10">
		<h2 id="groups" class="text-xl font-bold mb-4">ルートグループ</h2>

		<CodePreview
			title="(folder) でグループ化"
			description="URLに影響せずにフォルダを整理"
			language="plaintext"
			code={`app/
├── (marketing)/
│   ├── about/page.tsx    →  /about
│   └── contact/page.tsx  →  /contact
├── (shop)/
│   ├── products/page.tsx →  /products
│   └── cart/page.tsx     →  /cart
└── (auth)/
    ├── login/page.tsx    →  /login
    └── signup/page.tsx   →  /signup`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div style="color:#6a9955;">// (marketing) はURLに含まれない</div><div>/about ← (marketing)/about</div><div>/login ← (auth)/login</div></div>`}
		/>
	</section>

	<section class="mb-10">
		<h2 id="navigation" class="text-xl font-bold mb-4">ナビゲーション</h2>

		<CodePreview
			title="Link コンポーネント"
			description="クライアントサイドナビゲーション"
			language="typescript"
			code={`import Link from 'next/link';

export default function Navigation() {
  return (
    <nav>
      <Link href="/">ホーム</Link>
      <Link href="/about">概要</Link>
      <Link href="/blog/hello-world">記事</Link>

      {/* 動的パラメータ */}
      <Link href={\`/blog/\${slug}\`}>動的リンク</Link>

      {/* スクロール位置を維持しない */}
      <Link href="/page" scroll={false}>リンク</Link>
    </nav>
  );
}`}
			previewHtml={`<nav style="display:flex;gap:16px;padding:12px;background:#f3f4f6;border-radius:4px;"><a href="#" style="color:#3b82f6;text-decoration:none;">ホーム</a><a href="#" style="color:#3b82f6;text-decoration:none;">概要</a><a href="#" style="color:#3b82f6;text-decoration:none;">ブログ</a></nav>`}
		/>

		<CodePreview
			title="useRouter (プログラム的遷移)"
			description="ボタンクリック等での遷移"
			language="typescript"
			code={`'use client';

import { useRouter } from 'next/navigation';

export default function LoginButton() {
  const router = useRouter();

  const handleLogin = async () => {
    // ログイン処理...

    // 成功したらダッシュボードへ
    router.push('/dashboard');

    // 履歴を置き換え（戻るボタンで戻れない）
    router.replace('/dashboard');

    // 前のページに戻る
    router.back();

    // ページをリロード
    router.refresh();
  };

  return <button onClick={handleLogin}>ログイン</button>;
}`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div>router.<span style="color:#dcdcaa;">push</span>('/path') <span style="color:#6a9955;">// 遷移</span></div><div>router.<span style="color:#dcdcaa;">replace</span>('/path') <span style="color:#6a9955;">// 置き換え</span></div><div>router.<span style="color:#dcdcaa;">back</span>() <span style="color:#6a9955;">// 戻る</span></div></div>`}
		/>
	</section>

	<section class="mb-10">
		<h2 id="special-files" class="text-xl font-bold mb-4">特殊ファイル</h2>

		<div class="grid grid-cols-1 md:grid-cols-2 gap-4">
			<div class="p-4 rounded-lg bg-gray-100 dark:bg-gray-800">
				<code class="text-blue-600 dark:text-blue-400">page.tsx</code>
				<p class="text-sm text-gray-600 dark:text-gray-400 mt-1">ルートのUIを定義</p>
			</div>
			<div class="p-4 rounded-lg bg-gray-100 dark:bg-gray-800">
				<code class="text-blue-600 dark:text-blue-400">layout.tsx</code>
				<p class="text-sm text-gray-600 dark:text-gray-400 mt-1">共有レイアウト</p>
			</div>
			<div class="p-4 rounded-lg bg-gray-100 dark:bg-gray-800">
				<code class="text-blue-600 dark:text-blue-400">loading.tsx</code>
				<p class="text-sm text-gray-600 dark:text-gray-400 mt-1">ローディングUI</p>
			</div>
			<div class="p-4 rounded-lg bg-gray-100 dark:bg-gray-800">
				<code class="text-blue-600 dark:text-blue-400">error.tsx</code>
				<p class="text-sm text-gray-600 dark:text-gray-400 mt-1">エラーUI</p>
			</div>
			<div class="p-4 rounded-lg bg-gray-100 dark:bg-gray-800">
				<code class="text-blue-600 dark:text-blue-400">not-found.tsx</code>
				<p class="text-sm text-gray-600 dark:text-gray-400 mt-1">404ページ</p>
			</div>
			<div class="p-4 rounded-lg bg-gray-100 dark:bg-gray-800">
				<code class="text-blue-600 dark:text-blue-400">template.tsx</code>
				<p class="text-sm text-gray-600 dark:text-gray-400 mt-1">再レンダリングするレイアウト</p>
			</div>
		</div>
	</section>

	<div class="flex justify-between pt-6 border-t border-gray-200 dark:border-gray-700">
		<a href="/nextjs/intro" class="inline-flex items-center gap-2 px-4 py-2 rounded-lg border border-gray-300 dark:border-gray-600 hover:bg-gray-100 dark:hover:bg-gray-800 transition-colors">
			<svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
				<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 19l-7-7 7-7" />
			</svg>
			前へ：はじめに
		</a>
		<a href="/nextjs/data-fetching" class="inline-flex items-center gap-2 px-4 py-2 rounded-lg bg-primary-600 text-white hover:bg-primary-700 transition-colors">
			次へ：データ取得
			<svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
				<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 5l7 7-7 7" />
			</svg>
		</a>
	</div>
</article>
