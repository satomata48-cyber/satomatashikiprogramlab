<script>
	import CodePreview from '$lib/components/CodePreview.svelte';
</script>

<svelte:head>
	<title>Tailwind ユーティリティ | さとまたラボ</title>
</svelte:head>

<article>
	<h1 class="text-3xl font-bold mb-2">ユーティリティクラス</h1>
	<p class="text-lg text-gray-600 dark:text-gray-400 mb-8">
		よく使うユーティリティクラスを覚えよう
	</p>

	<section class="mb-10">
		<h2 id="spacing" class="text-xl font-bold mb-4">スペーシング</h2>

		<CodePreview
			title="padding と margin"
			description="p-, m- で余白を指定"
			language="html"
			code={`<!-- padding -->
<div class="p-4">全方向 1rem</div>
<div class="px-4">左右 1rem</div>
<div class="py-2">上下 0.5rem</div>
<div class="pt-8">上だけ 2rem</div>

<!-- margin -->
<div class="m-4">全方向 1rem</div>
<div class="mx-auto">左右auto（中央寄せ）</div>
<div class="mt-8">上だけ 2rem</div>
<div class="-mt-4">負のmargin</div>`}
			previewHtml={`<div style="display:flex;flex-direction:column;gap:8px;"><div style="padding:16px;background:#dbeafe;border-radius:4px;">p-4 (padding: 1rem)</div><div style="padding:8px 16px;background:#dcfce7;border-radius:4px;">px-4 py-2</div><div style="width:150px;margin:0 auto;padding:8px;background:#fef3c7;border-radius:4px;text-align:center;">mx-auto</div></div>`}
		/>

		<div class="p-4 rounded-lg bg-gray-100 dark:bg-gray-800 mb-4">
			<h3 class="font-semibold mb-2">スペーシングの値</h3>
			<div class="grid grid-cols-4 gap-2 text-sm font-mono">
				<div>0 = 0</div>
				<div>1 = 0.25rem</div>
				<div>2 = 0.5rem</div>
				<div>3 = 0.75rem</div>
				<div>4 = 1rem</div>
				<div>6 = 1.5rem</div>
				<div>8 = 2rem</div>
				<div>12 = 3rem</div>
			</div>
		</div>
	</section>

	<section class="mb-10">
		<h2 id="sizing" class="text-xl font-bold mb-4">サイズ</h2>

		<CodePreview
			title="width と height"
			description="w-, h- でサイズ指定"
			language="html"
			code={`<!-- 固定幅 -->
<div class="w-64">256px</div>
<div class="w-1/2">50%</div>
<div class="w-full">100%</div>

<!-- 高さ -->
<div class="h-screen">画面高さ</div>
<div class="h-full">親要素の100%</div>

<!-- 最大・最小 -->
<div class="max-w-md">最大448px</div>
<div class="min-h-screen">最小画面高さ</div>`}
			previewHtml={`<div style="display:flex;flex-direction:column;gap:8px;"><div style="width:256px;padding:8px;background:#dbeafe;border-radius:4px;">w-64 (256px)</div><div style="width:50%;padding:8px;background:#dcfce7;border-radius:4px;">w-1/2 (50%)</div><div style="width:100%;padding:8px;background:#fef3c7;border-radius:4px;">w-full (100%)</div></div>`}
		/>
	</section>

	<section class="mb-10">
		<h2 id="typography" class="text-xl font-bold mb-4">タイポグラフィ</h2>

		<CodePreview
			title="テキスト関連"
			description="フォントサイズ、太さ、配置"
			language="html"
			code={`<!-- サイズ -->
<p class="text-xs">極小</p>
<p class="text-sm">小</p>
<p class="text-base">基準</p>
<p class="text-lg">大</p>
<p class="text-xl">特大</p>
<p class="text-2xl">2倍</p>

<!-- 太さ -->
<p class="font-light">細い</p>
<p class="font-normal">通常</p>
<p class="font-medium">中太</p>
<p class="font-semibold">やや太い</p>
<p class="font-bold">太い</p>

<!-- 配置 -->
<p class="text-left">左揃え</p>
<p class="text-center">中央</p>
<p class="text-right">右揃え</p>`}
			previewHtml={`<div style="display:flex;flex-direction:column;gap:4px;"><p style="font-size:12px;">text-xs (12px)</p><p style="font-size:14px;">text-sm (14px)</p><p style="font-size:16px;">text-base (16px)</p><p style="font-size:18px;">text-lg (18px)</p><p style="font-size:20px;">text-xl (20px)</p><p style="font-size:24px;font-weight:bold;">text-2xl font-bold</p></div>`}
		/>
	</section>

	<section class="mb-10">
		<h2 id="colors" class="text-xl font-bold mb-4">色</h2>

		<CodePreview
			title="テキスト色と背景色"
			description="text-, bg- で色を指定"
			language="html"
			code={`<!-- テキスト色 -->
<p class="text-gray-500">グレー</p>
<p class="text-red-500">赤</p>
<p class="text-blue-500">青</p>
<p class="text-green-500">緑</p>

<!-- 背景色 -->
<div class="bg-gray-100">薄いグレー背景</div>
<div class="bg-blue-500">青背景</div>

<!-- 透明度付き -->
<div class="bg-black/50">50%透明の黒</div>`}
			previewHtml={`<div style="display:flex;flex-wrap:wrap;gap:8px;"><span style="color:#6b7280;">text-gray-500</span><span style="color:#ef4444;">text-red-500</span><span style="color:#3b82f6;">text-blue-500</span><span style="color:#22c55e;">text-green-500</span></div><div style="display:flex;gap:8px;margin-top:8px;"><div style="padding:8px;background:#f3f4f6;border-radius:4px;">bg-gray-100</div><div style="padding:8px;background:#3b82f6;color:white;border-radius:4px;">bg-blue-500</div></div>`}
		/>

		<div class="p-4 rounded-lg bg-gray-100 dark:bg-gray-800">
			<h3 class="font-semibold mb-2">色の濃さ</h3>
			<div class="flex gap-1">
				{#each [50, 100, 200, 300, 400, 500, 600, 700, 800, 900] as shade}
					<div
						class="w-8 h-8 rounded text-xs flex items-center justify-center"
						style="background-color: rgb({shade < 500 ? 255 - shade/2 : 255 - shade/3}, {shade < 500 ? 255 - shade/2 : 255 - shade/3}, {255 - shade/4})"
					>
						{shade}
					</div>
				{/each}
			</div>
			<p class="text-sm text-gray-600 dark:text-gray-400 mt-2">50(薄い) → 900(濃い)</p>
		</div>
	</section>

	<section class="mb-10">
		<h2 id="borders" class="text-xl font-bold mb-4">ボーダー</h2>

		<CodePreview
			title="枠線と角丸"
			description="border, rounded"
			language="html"
			code={`<!-- 枠線 -->
<div class="border">1pxの枠線</div>
<div class="border-2">2pxの枠線</div>
<div class="border-b">下線のみ</div>
<div class="border-gray-300">グレーの枠線</div>

<!-- 角丸 -->
<div class="rounded">少し丸い</div>
<div class="rounded-lg">もっと丸い</div>
<div class="rounded-full">完全に丸い</div>

<!-- 組み合わせ -->
<div class="border-2 border-blue-500 rounded-lg">
  青い枠線、角丸
</div>`}
			previewHtml={`<div style="display:flex;flex-wrap:wrap;gap:12px;"><div style="padding:12px;border:1px solid #d1d5db;border-radius:4px;">rounded</div><div style="padding:12px;border:1px solid #d1d5db;border-radius:8px;">rounded-lg</div><div style="padding:12px;border:1px solid #d1d5db;border-radius:9999px;">rounded-full</div><div style="padding:12px;border:2px solid #3b82f6;border-radius:8px;">border-blue-500</div></div>`}
		/>
	</section>

	<section class="mb-10">
		<h2 id="shadows" class="text-xl font-bold mb-4">シャドウ</h2>

		<CodePreview
			title="ボックスシャドウ"
			description="shadow-* でシャドウを追加"
			language="html"
			code={`<div class="shadow-sm">小さい影</div>
<div class="shadow">通常の影</div>
<div class="shadow-md">中くらい</div>
<div class="shadow-lg">大きい</div>
<div class="shadow-xl">特大</div>
<div class="shadow-2xl">超特大</div>
<div class="shadow-none">影なし</div>`}
			previewHtml={`<div style="display:flex;flex-wrap:wrap;gap:16px;"><div style="padding:16px;background:white;border-radius:8px;box-shadow:0 1px 2px rgba(0,0,0,0.05);">shadow-sm</div><div style="padding:16px;background:white;border-radius:8px;box-shadow:0 1px 3px rgba(0,0,0,0.1);">shadow</div><div style="padding:16px;background:white;border-radius:8px;box-shadow:0 4px 6px rgba(0,0,0,0.1);">shadow-md</div><div style="padding:16px;background:white;border-radius:8px;box-shadow:0 10px 15px rgba(0,0,0,0.1);">shadow-lg</div></div>`}
		/>
	</section>

	<section class="mb-10">
		<h2 id="display" class="text-xl font-bold mb-4">表示・非表示</h2>

		<CodePreview
			title="display プロパティ"
			description="block, flex, grid, hidden"
			language="html"
			code={`<div class="block">ブロック</div>
<div class="inline">インライン</div>
<div class="inline-block">インラインブロック</div>
<div class="flex">Flexbox</div>
<div class="grid">Grid</div>
<div class="hidden">非表示</div>

<!-- レスポンシブで切り替え -->
<div class="hidden md:block">
  768px以上で表示
</div>
<div class="block md:hidden">
  768px未満で表示
</div>`}
			previewHtml={`<div style="display:flex;flex-direction:column;gap:8px;"><div style="display:flex;gap:8px;background:#f3f4f6;padding:8px;border-radius:4px;"><span style="background:#3b82f6;color:white;padding:4px 8px;border-radius:4px;">flex item</span><span style="background:#3b82f6;color:white;padding:4px 8px;border-radius:4px;">flex item</span></div><div style="display:grid;grid-template-columns:repeat(3,1fr);gap:8px;"><div style="background:#22c55e;color:white;padding:8px;border-radius:4px;text-align:center;">grid</div><div style="background:#22c55e;color:white;padding:8px;border-radius:4px;text-align:center;">grid</div><div style="background:#22c55e;color:white;padding:8px;border-radius:4px;text-align:center;">grid</div></div></div>`}
		/>
	</section>

	<div class="flex justify-between pt-6 border-t border-gray-200 dark:border-gray-700">
		<a href="/tailwind/intro" class="inline-flex items-center gap-2 px-4 py-2 rounded-lg border border-gray-300 dark:border-gray-600 hover:bg-gray-100 dark:hover:bg-gray-800 transition-colors">
			<svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
				<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 19l-7-7 7-7" />
			</svg>
			前へ：はじめに
		</a>
		<a href="/tailwind/responsive" class="inline-flex items-center gap-2 px-4 py-2 rounded-lg bg-primary-600 text-white hover:bg-primary-700 transition-colors">
			次へ：レスポンシブ
			<svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
				<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 5l7 7-7 7" />
			</svg>
		</a>
	</div>
</article>
