<script>
	import CodePreview from '$lib/components/CodePreview.svelte';
</script>

<svelte:head>
	<title>Tailwind レスポンシブ | さとまたラボ</title>
</svelte:head>

<article>
	<h1 class="text-3xl font-bold mb-2">レスポンシブデザイン</h1>
	<p class="text-lg text-gray-600 dark:text-gray-400 mb-8">
		画面サイズに応じたスタイルを適用する
	</p>

	<section class="mb-10">
		<h2 id="breakpoints" class="text-xl font-bold mb-4">ブレークポイント</h2>

		<div class="overflow-x-auto">
			<table class="w-full text-sm">
				<thead>
					<tr class="border-b border-gray-200 dark:border-gray-700">
						<th class="text-left py-2 px-4">プレフィックス</th>
						<th class="text-left py-2 px-4">最小幅</th>
						<th class="text-left py-2 px-4">デバイス</th>
					</tr>
				</thead>
				<tbody>
					<tr class="border-b border-gray-200 dark:border-gray-700">
						<td class="py-2 px-4 font-mono text-cyan-600">sm:</td>
						<td class="py-2 px-4">640px</td>
						<td class="py-2 px-4">スマホ（横向き）</td>
					</tr>
					<tr class="border-b border-gray-200 dark:border-gray-700">
						<td class="py-2 px-4 font-mono text-cyan-600">md:</td>
						<td class="py-2 px-4">768px</td>
						<td class="py-2 px-4">タブレット</td>
					</tr>
					<tr class="border-b border-gray-200 dark:border-gray-700">
						<td class="py-2 px-4 font-mono text-cyan-600">lg:</td>
						<td class="py-2 px-4">1024px</td>
						<td class="py-2 px-4">ノートPC</td>
					</tr>
					<tr class="border-b border-gray-200 dark:border-gray-700">
						<td class="py-2 px-4 font-mono text-cyan-600">xl:</td>
						<td class="py-2 px-4">1280px</td>
						<td class="py-2 px-4">デスクトップ</td>
					</tr>
					<tr>
						<td class="py-2 px-4 font-mono text-cyan-600">2xl:</td>
						<td class="py-2 px-4">1536px</td>
						<td class="py-2 px-4">大画面</td>
					</tr>
				</tbody>
			</table>
		</div>
	</section>

	<section class="mb-10">
		<h2 id="mobile-first" class="text-xl font-bold mb-4">モバイルファースト</h2>

		<div class="p-4 rounded-lg bg-blue-50 dark:bg-blue-900/20 border border-blue-200 dark:border-blue-800 mb-4">
			<p class="text-blue-800 dark:text-blue-200">
				<strong>重要：</strong>プレフィックスなしのクラスは全サイズに適用。
				プレフィックス付きは「その幅以上」に適用されます。
			</p>
		</div>

		<CodePreview
			title="基本的な使い方"
			description="小さい画面から順に指定"
			language="html"
			code={`<!-- モバイル: 1列、タブレット: 2列、PC: 3列 -->
<div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-4">
  <div>Item 1</div>
  <div>Item 2</div>
  <div>Item 3</div>
</div>

<!-- 解説 -->
<!-- grid-cols-1: 全サイズでデフォルト -->
<!-- md:grid-cols-2: 768px以上で2列 -->
<!-- lg:grid-cols-3: 1024px以上で3列 -->`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div>モバイル → <span style="color:#4ec9b0;">1列</span></div><div>768px〜 → <span style="color:#4ec9b0;">2列</span></div><div>1024px〜 → <span style="color:#4ec9b0;">3列</span></div></div>`}
		/>
	</section>

	<section class="mb-10">
		<h2 id="examples" class="text-xl font-bold mb-4">実践例</h2>

		<CodePreview
			title="レスポンシブなカードグリッド"
			description="画面幅に応じて列数を変更"
			language="html"
			code={`<div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 xl:grid-cols-4 gap-6">
  <div class="p-6 bg-white rounded-lg shadow">
    カード1
  </div>
  <div class="p-6 bg-white rounded-lg shadow">
    カード2
  </div>
  <!-- ... -->
</div>`}
			previewHtml={`<div style="display:grid;grid-template-columns:repeat(3,1fr);gap:12px;"><div style="padding:16px;background:white;border-radius:8px;box-shadow:0 1px 3px rgba(0,0,0,0.1);">カード1</div><div style="padding:16px;background:white;border-radius:8px;box-shadow:0 1px 3px rgba(0,0,0,0.1);">カード2</div><div style="padding:16px;background:white;border-radius:8px;box-shadow:0 1px 3px rgba(0,0,0,0.1);">カード3</div></div>`}
		/>

		<CodePreview
			title="レスポンシブなナビゲーション"
			description="モバイルでハンバーガーメニュー"
			language="html"
			code={`<nav class="flex items-center justify-between p-4">
  <div class="text-xl font-bold">Logo</div>

  <!-- モバイル: 表示 -->
  <button class="md:hidden">
    <svg class="w-6 h-6"><!-- ハンバーガーアイコン --></svg>
  </button>

  <!-- デスクトップ: 表示 -->
  <div class="hidden md:flex gap-6">
    <a href="/">Home</a>
    <a href="/about">About</a>
    <a href="/contact">Contact</a>
  </div>
</nav>`}
			previewHtml={`<nav style="display:flex;align-items:center;justify-content:space-between;padding:12px 16px;background:#1f2937;border-radius:8px;"><div style="font-weight:bold;color:white;">Logo</div><div style="display:flex;gap:24px;"><a style="color:#9ca3af;">Home</a><a style="color:#9ca3af;">About</a><a style="color:#9ca3af;">Contact</a></div></nav>`}
		/>

		<CodePreview
			title="レスポンシブなテキスト"
			description="画面サイズでフォントサイズを変更"
			language="html"
			code={`<h1 class="text-2xl sm:text-3xl md:text-4xl lg:text-5xl font-bold">
  レスポンシブな見出し
</h1>

<p class="text-sm md:text-base lg:text-lg">
  本文テキスト
</p>`}
			previewHtml={`<div><h1 style="font-size:36px;font-weight:bold;margin-bottom:8px;">レスポンシブな見出し</h1><p style="font-size:16px;color:#6b7280;">本文テキスト（画面幅で大きくなる）</p></div>`}
		/>

		<CodePreview
			title="レスポンシブなスペーシング"
			description="画面サイズでpaddingを変更"
			language="html"
			code={`<!-- モバイルで小さく、PCで大きく -->
<div class="p-4 md:p-8 lg:p-12">
  コンテンツ
</div>

<!-- コンテナ幅 -->
<div class="max-w-sm md:max-w-md lg:max-w-lg xl:max-w-xl mx-auto">
  中央寄せコンテナ
</div>`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div>モバイル → <span style="color:#4ec9b0;">p-4 (16px)</span></div><div>md → <span style="color:#4ec9b0;">p-8 (32px)</span></div><div>lg → <span style="color:#4ec9b0;">p-12 (48px)</span></div></div>`}
		/>
	</section>

	<section class="mb-10">
		<h2 id="visibility" class="text-xl font-bold mb-4">表示・非表示の切り替え</h2>

		<CodePreview
			title="hidden と block"
			description="画面サイズで表示を切り替え"
			language="html"
			code={`<!-- モバイルのみ表示 -->
<div class="block md:hidden">
  モバイル用コンテンツ
</div>

<!-- タブレット以上で表示 -->
<div class="hidden md:block">
  PC用コンテンツ
</div>

<!-- 特定の範囲だけ表示 -->
<div class="hidden sm:block lg:hidden">
  640px〜1024px で表示
</div>`}
			previewHtml={`<div style="display:flex;flex-direction:column;gap:8px;"><div style="padding:12px;background:#fef3c7;border-radius:4px;font-size:14px;"><span style="color:#92400e;">📱</span> block md:hidden (モバイルのみ)</div><div style="padding:12px;background:#dbeafe;border-radius:4px;font-size:14px;"><span style="color:#1e40af;">💻</span> hidden md:block (タブレット以上)</div></div>`}
		/>
	</section>

	<section class="mb-10">
		<h2 id="flex-direction" class="text-xl font-bold mb-4">Flexboxのレスポンシブ</h2>

		<CodePreview
			title="縦並び→横並び"
			description="モバイルで縦、PCで横"
			language="html"
			code={`<div class="flex flex-col md:flex-row gap-4">
  <div class="flex-1">サイドバー</div>
  <div class="flex-1">メインコンテンツ</div>
</div>

<!-- 順序の変更 -->
<div class="flex flex-col-reverse md:flex-row">
  <div>後ろ（モバイル）/ 左（PC）</div>
  <div>前（モバイル）/ 右（PC）</div>
</div>`}
			previewHtml={`<div style="display:flex;gap:16px;"><div style="flex:1;padding:16px;background:#dbeafe;border-radius:4px;text-align:center;">サイドバー</div><div style="flex:2;padding:16px;background:#dcfce7;border-radius:4px;text-align:center;">メインコンテンツ</div></div>`}
		/>
	</section>

	<div class="flex justify-between pt-6 border-t border-gray-200 dark:border-gray-700">
		<a href="/tailwind/utilities" class="inline-flex items-center gap-2 px-4 py-2 rounded-lg border border-gray-300 dark:border-gray-600 hover:bg-gray-100 dark:hover:bg-gray-800 transition-colors">
			<svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
				<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 19l-7-7 7-7" />
			</svg>
			前へ：ユーティリティ
		</a>
		<a href="/tailwind/layouts" class="inline-flex items-center gap-2 px-4 py-2 rounded-lg bg-primary-600 text-white hover:bg-primary-700 transition-colors">
			次へ：モダンレイアウト
			<svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
				<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 5l7 7-7 7" />
			</svg>
		</a>
	</div>
</article>
