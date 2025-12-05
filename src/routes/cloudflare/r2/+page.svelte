<script>
	import CodePreview from '$lib/components/CodePreview.svelte';
	import FeatureCard from '$lib/components/FeatureCard.svelte';

	const features = [
		{ icon: '📦', title: 'S3互換', description: 'AWS S3のAPIと互換性あり', tag: 'API' },
		{ icon: '💰', title: '低コスト', description: 'エグレス料金が無料', tag: '料金' },
		{ icon: '🌍', title: 'グローバル', description: '世界中に自動分散', tag: 'パフォーマンス' },
		{ icon: '🔒', title: 'セキュア', description: '署名付きURL対応', tag: 'セキュリティ' }
	];
</script>

<svelte:head>
	<title>Cloudflare R2 | さとまたラボ</title>
</svelte:head>

<article>
	<h1 class="text-3xl font-bold mb-2">R2 ストレージ</h1>
	<p class="text-lg text-gray-600 dark:text-gray-400 mb-8">
		S3互換のオブジェクトストレージ（エグレス料金無料）
	</p>

	<!-- R2とは -->
	<section class="mb-10">
		<h2 id="what-is" class="text-xl font-bold mb-4">R2とは？</h2>

		<div class="p-6 rounded-xl bg-orange-50 dark:bg-orange-900/20 border border-orange-200 dark:border-orange-800 mb-6">
			<p class="text-orange-800 dark:text-orange-200 mb-4">
				<strong>一言で言うと：</strong>「AWS S3 のような、でもエグレス料金が無料のストレージ」
			</p>
			<p class="text-sm text-orange-700 dark:text-orange-300">
				画像、動画、PDF、バックアップなど、あらゆるファイルを保存できます。
				S3互換なので、既存のツールやライブラリがそのまま使えます。
			</p>
		</div>
	</section>

	<!-- 特徴 -->
	<section class="mb-10">
		<h2 id="features" class="text-xl font-bold mb-4">R2の特徴</h2>
		<div class="grid grid-cols-1 md:grid-cols-2 gap-3">
			{#each features as feature}
				<FeatureCard {...feature} />
			{/each}
		</div>

		<div class="mt-4 p-4 rounded-lg bg-green-50 dark:bg-green-900/20 border border-green-200 dark:border-green-800">
			<p class="font-semibold text-green-800 dark:text-green-200 mb-2">エグレス料金とは？</p>
			<p class="text-sm text-green-700 dark:text-green-300">
				「データを外に出すときにかかる料金」のこと。AWS S3では、ファイルをダウンロードするたびに料金がかかります。
				R2はこれが<strong>完全無料</strong>なので、画像配信などに最適です。
			</p>
		</div>
	</section>

	<!-- 料金 -->
	<section class="mb-10">
		<h2 id="pricing" class="text-xl font-bold mb-4">料金</h2>

		<div class="grid md:grid-cols-2 gap-4">
			<div class="p-4 rounded-lg bg-gray-50 dark:bg-gray-800 border border-gray-200 dark:border-gray-700">
				<h3 class="font-bold text-lg mb-2">無料枠</h3>
				<ul class="text-sm text-gray-600 dark:text-gray-400 space-y-1">
					<li>・ストレージ: 10GB/月</li>
					<li>・Class A操作: 100万回/月</li>
					<li>・Class B操作: 1000万回/月</li>
					<li>・エグレス: <strong>無料</strong></li>
				</ul>
			</div>
			<div class="p-4 rounded-lg bg-orange-50 dark:bg-orange-900/20 border border-orange-200 dark:border-orange-800">
				<h3 class="font-bold text-lg mb-2">有料プラン</h3>
				<ul class="text-sm text-gray-600 dark:text-gray-400 space-y-1">
					<li>・ストレージ: $0.015/GB/月</li>
					<li>・Class A: $4.50/100万回</li>
					<li>・Class B: $0.36/100万回</li>
					<li>・エグレス: <strong>無料</strong></li>
				</ul>
			</div>
		</div>
	</section>

	<!-- セットアップ -->
	<section class="mb-10">
		<h2 id="setup" class="text-xl font-bold mb-4">セットアップ</h2>

		<CodePreview
			title="R2バケットを作成"
			description="Wrangler CLIで作成"
			language="bash"
			code={`# R2バケットを作成
wrangler r2 bucket create my-bucket

# バケット一覧を確認
wrangler r2 bucket list`}
		/>

		<CodePreview
			title="wrangler.json に追加"
			description="バインディング設定"
			language="json"
			code={`{
  "r2_buckets": [
    {
      "binding": "BUCKET",
      "bucket_name": "my-bucket"
    }
  ]
}`}
		/>

		<CodePreview
			title="src/app.d.ts"
			description="型定義"
			language="typescript"
			code={`declare global {
  namespace App {
    interface Platform {
      env: {
        DB: D1Database;
        BUCKET: R2Bucket;  // R2を追加
      };
    }
  }
}

export {};`}
		/>
	</section>

	<!-- 使用例 -->
	<section class="mb-10">
		<h2 id="usage" class="text-xl font-bold mb-4">SvelteKitでの使用例</h2>

		<CodePreview
			title="ファイルアップロード"
			description="+server.ts"
			language="typescript"
			code={`// src/routes/api/upload/+server.ts
import type { RequestHandler } from './$types';

export const POST: RequestHandler = async ({ request, platform }) => {
  const bucket = platform?.env?.BUCKET;
  if (!bucket) return new Response('R2 not available', { status: 500 });

  const formData = await request.formData();
  const file = formData.get('file') as File;

  // ユニークなキーを生成
  const key = \`uploads/\${Date.now()}-\${file.name}\`;

  // R2にアップロード
  await bucket.put(key, file.stream(), {
    httpMetadata: {
      contentType: file.type
    }
  });

  return Response.json({ key });
};`}
		/>

		<CodePreview
			title="ファイル取得"
			description="ダウンロード"
			language="typescript"
			code={`// src/routes/api/files/[...key]/+server.ts
import type { RequestHandler } from './$types';

export const GET: RequestHandler = async ({ params, platform }) => {
  const bucket = platform?.env?.BUCKET;
  if (!bucket) return new Response('R2 not available', { status: 500 });

  const object = await bucket.get(params.key);

  if (!object) {
    return new Response('Not Found', { status: 404 });
  }

  return new Response(object.body, {
    headers: {
      'Content-Type': object.httpMetadata?.contentType || 'application/octet-stream'
    }
  });
};`}
		/>
	</section>

	<!-- 今後の予定 -->
	<section class="mb-10">
		<div class="p-6 rounded-xl bg-blue-50 dark:bg-blue-900/20 border border-blue-200 dark:border-blue-800">
			<p class="font-semibold text-blue-800 dark:text-blue-200 mb-2">このページは追加予定</p>
			<p class="text-sm text-blue-700 dark:text-blue-300">
				R2の詳細な使い方（署名付きURL、公開設定、Workersとの連携など）は
				今後追加していきます。
			</p>
		</div>
	</section>

	<!-- ナビゲーション -->
	<div class="flex justify-between pt-6 border-t border-gray-200 dark:border-gray-700">
		<a href="/cloudflare/d1-sveltekit" class="inline-flex items-center gap-2 px-4 py-2 rounded-lg border border-gray-300 dark:border-gray-600 hover:bg-gray-100 dark:hover:bg-gray-800 transition-colors">
			<svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
				<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 19l-7-7 7-7" />
			</svg>
			前へ：D1 SvelteKit連携
		</a>
		<a href="/cloudflare/pages" class="inline-flex items-center gap-2 px-4 py-2 rounded-lg bg-primary-600 text-white hover:bg-primary-700 transition-colors">
			次へ：Pages デプロイ
			<svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
				<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 5l7 7-7 7" />
			</svg>
		</a>
	</div>
</article>
