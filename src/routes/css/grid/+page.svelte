<script>
	import CodePreview from '$lib/components/CodePreview.svelte';
</script>

<svelte:head>
	<title>CSS Grid | さとまたラボ</title>
</svelte:head>

<article>
	<h1 class="text-3xl font-bold mb-2">CSS Grid</h1>
	<p class="text-lg text-gray-600 dark:text-gray-400 mb-8">
		強力な2次元レイアウトシステム
	</p>

	<!-- CSS Gridとは -->
	<section class="mb-10">
		<h2 id="what-is" class="text-xl font-bold mb-4">CSS Gridとは？</h2>

		<div class="p-6 rounded-xl bg-blue-50 dark:bg-blue-900/20 border border-blue-200 dark:border-blue-800 mb-6">
			<p class="text-blue-800 dark:text-blue-200 mb-4">
				<strong>日常での例え：</strong>Excel（スプレッドシート）
			</p>
			<div class="text-sm text-blue-700 dark:text-blue-300 space-y-2">
				<p>Excelのように「行」と「列」でマス目を作り、そこに要素を配置する仕組みです。</p>
				<p>「このセルは2列分使う」「この領域をヘッダーにする」といった指定が簡単にできます。</p>
			</div>
		</div>

		<div class="p-4 rounded-lg bg-amber-50 dark:bg-amber-900/20 border border-amber-200 dark:border-amber-800 mb-6">
			<p class="font-semibold text-amber-800 dark:text-amber-200">なぜCSS Gridが必要？</p>
			<div class="text-sm text-amber-700 dark:text-amber-300 mt-2">
				<p class="mb-2"><strong>Flexboxだけでは難しいこと：</strong></p>
				<ul class="list-disc list-inside space-y-1 mb-3">
					<li>「3列×2行」のような格子状レイアウト</li>
					<li>「ヘッダーは横幅いっぱい、サイドバーは左側」のような複雑な配置</li>
					<li>要素を特定のセルにピンポイントで配置</li>
				</ul>
				<p><strong>CSS Grid</strong>は「ページ全体の骨組み」を作るのに最適です。</p>
			</div>
		</div>

		<div class="p-4 rounded-lg bg-gray-100 dark:bg-gray-800 mb-6">
			<p class="font-semibold text-gray-800 dark:text-gray-200 mb-2">「2次元レイアウト」とは？</p>
			<p class="text-sm text-gray-700 dark:text-gray-300">
				<strong>横と縦の両方向</strong>を同時に制御すること。<br>
				Flexboxは「横だけ」または「縦だけ」だが、Gridは「両方同時に」制御できる。
			</p>
		</div>
	</section>

	<section class="mb-10">
		<h2 id="basic" class="text-xl font-bold mb-4">基本の使い方</h2>

		<CodePreview
			title="display: grid"
			description="列数を指定してグリッドを作成"
			language="css"
			code={`.container {
  display: grid;
  grid-template-columns: 1fr 1fr 1fr; /* 3等分 */
  gap: 10px;
}`}
			previewHtml={`<div style="display:grid;grid-template-columns:1fr 1fr 1fr;gap:10px;"><div style="padding:20px;background:#3b82f6;color:white;border-radius:4px;text-align:center;">1</div><div style="padding:20px;background:#3b82f6;color:white;border-radius:4px;text-align:center;">2</div><div style="padding:20px;background:#3b82f6;color:white;border-radius:4px;text-align:center;">3</div><div style="padding:20px;background:#3b82f6;color:white;border-radius:4px;text-align:center;">4</div><div style="padding:20px;background:#3b82f6;color:white;border-radius:4px;text-align:center;">5</div><div style="padding:20px;background:#3b82f6;color:white;border-radius:4px;text-align:center;">6</div></div>`}
		/>
	</section>

	<section class="mb-10">
		<h2 id="columns" class="text-xl font-bold mb-4">grid-template-columns</h2>

		<div class="p-4 rounded-lg bg-blue-50 dark:bg-blue-900/20 border border-blue-200 dark:border-blue-800 mb-6">
			<p class="font-semibold text-blue-800 dark:text-blue-200 mb-2">「fr」単位とは？</p>
			<p class="text-sm text-blue-700 dark:text-blue-300 mb-3">
				<strong>fr = fraction（分数・比率）</strong>の略。余ったスペースを「比率」で分ける単位です。
			</p>
			<div class="text-sm text-blue-700 dark:text-blue-300">
				<code class="bg-blue-200 dark:bg-blue-800 px-1 rounded">1fr 1fr 1fr</code> → 3等分<br>
				<code class="bg-blue-200 dark:bg-blue-800 px-1 rounded">1fr 2fr 1fr</code> → 真ん中が2倍の幅<br>
				<code class="bg-blue-200 dark:bg-blue-800 px-1 rounded">200px 1fr</code> → 左は200px固定、残りは右が全部取る
			</div>
		</div>

		<CodePreview
			title="列の定義方法"
			description="px, fr, auto, repeat() など"
			language="css"
			code={`/* 固定幅 */
grid-template-columns: 200px 200px 200px;

/* fr単位（比率） */
grid-template-columns: 1fr 2fr 1fr;

/* repeat() で繰り返し */
grid-template-columns: repeat(3, 1fr);

/* auto で内容に合わせる */
grid-template-columns: auto 1fr auto;

/* minmax() で最小・最大 */
grid-template-columns: repeat(3, minmax(100px, 1fr));`}
			previewHtml={`<div style="display:flex;flex-direction:column;gap:12px;"><div><div style="font-size:12px;margin-bottom:4px;">1fr 2fr 1fr</div><div style="display:grid;grid-template-columns:1fr 2fr 1fr;gap:4px;"><div style="padding:8px;background:#3b82f6;color:white;border-radius:4px;text-align:center;font-size:12px;">1fr</div><div style="padding:8px;background:#8b5cf6;color:white;border-radius:4px;text-align:center;font-size:12px;">2fr</div><div style="padding:8px;background:#3b82f6;color:white;border-radius:4px;text-align:center;font-size:12px;">1fr</div></div></div><div><div style="font-size:12px;margin-bottom:4px;">repeat(4, 1fr)</div><div style="display:grid;grid-template-columns:repeat(4,1fr);gap:4px;"><div style="padding:8px;background:#22c55e;color:white;border-radius:4px;text-align:center;font-size:12px;">1</div><div style="padding:8px;background:#22c55e;color:white;border-radius:4px;text-align:center;font-size:12px;">2</div><div style="padding:8px;background:#22c55e;color:white;border-radius:4px;text-align:center;font-size:12px;">3</div><div style="padding:8px;background:#22c55e;color:white;border-radius:4px;text-align:center;font-size:12px;">4</div></div></div></div>`}
		/>
	</section>

	<section class="mb-10">
		<h2 id="rows" class="text-xl font-bold mb-4">grid-template-rows</h2>

		<CodePreview
			title="行の定義"
			description="列と同じ書き方で行を指定"
			language="css"
			code={`.container {
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  grid-template-rows: 100px 200px 100px;
  gap: 10px;
}

/* 自動生成される行の高さ */
.container {
  grid-auto-rows: minmax(100px, auto);
}`}
			previewHtml={`<div style="display:grid;grid-template-columns:repeat(2,1fr);grid-template-rows:60px 100px 60px;gap:8px;"><div style="background:#3b82f6;color:white;border-radius:4px;display:flex;align-items:center;justify-content:center;">1</div><div style="background:#3b82f6;color:white;border-radius:4px;display:flex;align-items:center;justify-content:center;">2</div><div style="background:#8b5cf6;color:white;border-radius:4px;display:flex;align-items:center;justify-content:center;">3</div><div style="background:#8b5cf6;color:white;border-radius:4px;display:flex;align-items:center;justify-content:center;">4</div><div style="background:#3b82f6;color:white;border-radius:4px;display:flex;align-items:center;justify-content:center;">5</div><div style="background:#3b82f6;color:white;border-radius:4px;display:flex;align-items:center;justify-content:center;">6</div></div>`}
		/>
	</section>

	<section class="mb-10">
		<h2 id="span" class="text-xl font-bold mb-4">グリッド線を使った配置</h2>

		<CodePreview
			title="grid-column / grid-row"
			description="複数のセルにまたがる配置"
			language="css"
			code={`.container {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 10px;
}

/* 列1から3まで（2列分） */
.wide {
  grid-column: 1 / 3;
}

/* span で指定 */
.wide2 {
  grid-column: span 2;
}

/* 行も同様 */
.tall {
  grid-row: span 2;
}`}
			previewHtml={`<div style="display:grid;grid-template-columns:repeat(3,1fr);gap:8px;"><div style="grid-column:span 2;padding:16px;background:#ec4899;color:white;border-radius:4px;text-align:center;">span 2</div><div style="padding:16px;background:#3b82f6;color:white;border-radius:4px;text-align:center;">3</div><div style="padding:16px;background:#3b82f6;color:white;border-radius:4px;text-align:center;">4</div><div style="padding:16px;background:#3b82f6;color:white;border-radius:4px;text-align:center;">5</div><div style="padding:16px;background:#3b82f6;color:white;border-radius:4px;text-align:center;">6</div></div>`}
		/>
	</section>

	<section class="mb-10">
		<h2 id="areas" class="text-xl font-bold mb-4">grid-template-areas</h2>

		<div class="p-4 rounded-lg bg-blue-50 dark:bg-blue-900/20 border border-blue-200 dark:border-blue-800 mb-6">
			<p class="font-semibold text-blue-800 dark:text-blue-200 mb-2">grid-template-areasとは？</p>
			<p class="text-sm text-blue-700 dark:text-blue-300 mb-3">
				グリッドの各領域に<strong>名前</strong>を付けて、視覚的にレイアウトを定義する方法です。
			</p>
			<p class="text-sm text-blue-700 dark:text-blue-300">
				<strong>コードを見るだけでレイアウトが分かる</strong>のが大きなメリット！<br>
				複雑なページ構造（ヘッダー、サイドバー、メイン、フッター）に最適。
			</p>
		</div>

		<CodePreview
			title="名前でレイアウト定義"
			description="視覚的にレイアウトを指定"
			language="css"
			code={`.container {
  display: grid;
  grid-template-columns: 200px 1fr;
  grid-template-rows: auto 1fr auto;
  grid-template-areas:
    "header header"
    "sidebar main"
    "footer footer";
  gap: 10px;
}

.header  { grid-area: header; }
.sidebar { grid-area: sidebar; }
.main    { grid-area: main; }
.footer  { grid-area: footer; }`}
			previewHtml={`<div style="display:grid;grid-template-columns:80px 1fr;grid-template-rows:40px 80px 40px;grid-template-areas:'header header' 'sidebar main' 'footer footer';gap:8px;font-size:12px;"><div style="grid-area:header;background:#3b82f6;color:white;border-radius:4px;display:flex;align-items:center;justify-content:center;">header</div><div style="grid-area:sidebar;background:#22c55e;color:white;border-radius:4px;display:flex;align-items:center;justify-content:center;">sidebar</div><div style="grid-area:main;background:#8b5cf6;color:white;border-radius:4px;display:flex;align-items:center;justify-content:center;">main</div><div style="grid-area:footer;background:#6b7280;color:white;border-radius:4px;display:flex;align-items:center;justify-content:center;">footer</div></div>`}
		/>
	</section>

	<section class="mb-10">
		<h2 id="align" class="text-xl font-bold mb-4">配置の制御</h2>

		<CodePreview
			title="justify-items / align-items"
			description="セル内のアイテム配置"
			language="css"
			code={`.container {
  display: grid;
  grid-template-columns: repeat(3, 1fr);

  /* セル内の水平位置 */
  justify-items: start | end | center | stretch;

  /* セル内の垂直位置 */
  align-items: start | end | center | stretch;

  /* 一括指定 */
  place-items: center; /* align justify */
}`}
			previewHtml={`<div style="display:grid;grid-template-columns:repeat(3,1fr);gap:8px;justify-items:center;align-items:center;"><div style="padding:12px;background:#3b82f6;color:white;border-radius:4px;font-size:12px;">center</div><div style="padding:12px;background:#3b82f6;color:white;border-radius:4px;font-size:12px;">center</div><div style="padding:12px;background:#3b82f6;color:white;border-radius:4px;font-size:12px;">center</div></div>`}
		/>
	</section>

	<section class="mb-10">
		<h2 id="responsive" class="text-xl font-bold mb-4">レスポンシブGrid</h2>

		<div class="p-4 rounded-lg bg-blue-50 dark:bg-blue-900/20 border border-blue-200 dark:border-blue-800 mb-6">
			<p class="font-semibold text-blue-800 dark:text-blue-200 mb-2">「レスポンシブ」とは？</p>
			<p class="text-sm text-blue-700 dark:text-blue-300 mb-3">
				画面サイズに応じて<strong>自動的にレイアウトが変わる</strong>こと。<br>
				PC、タブレット、スマホで同じサイトを見ても、見やすく表示される。
			</p>
			<p class="font-semibold text-blue-800 dark:text-blue-200 mb-2">auto-fit と minmax() の組み合わせ</p>
			<p class="text-sm text-blue-700 dark:text-blue-300">
				<code class="bg-blue-200 dark:bg-blue-800 px-1 rounded">repeat(auto-fit, minmax(200px, 1fr))</code><br>
				→ 「最小200px、最大は均等に」で自動的に列数が決まる！
			</p>
		</div>

		<CodePreview
			title="auto-fit / auto-fill"
			description="自動で列数を調整"
			language="css"
			code={`/* 最小200px、最大1fr で自動配置 */
.container {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
  gap: 20px;
}

/* auto-fill: 空の列も作る */
/* auto-fit: 空の列を潰す */`}
			previewHtml={`<div style="display:grid;grid-template-columns:repeat(auto-fit,minmax(80px,1fr));gap:8px;"><div style="padding:16px;background:#3b82f6;color:white;border-radius:4px;text-align:center;font-size:12px;">Item</div><div style="padding:16px;background:#3b82f6;color:white;border-radius:4px;text-align:center;font-size:12px;">Item</div><div style="padding:16px;background:#3b82f6;color:white;border-radius:4px;text-align:center;font-size:12px;">Item</div><div style="padding:16px;background:#3b82f6;color:white;border-radius:4px;text-align:center;font-size:12px;">Item</div></div>`}
		/>
	</section>

	<section class="mb-10">
		<h2 id="vs-flex" class="text-xl font-bold mb-4">Flexbox vs Grid</h2>

		<div class="grid grid-cols-1 md:grid-cols-2 gap-4">
			<div class="p-4 rounded-lg bg-blue-50 dark:bg-blue-900/20 border border-blue-200 dark:border-blue-800">
				<h3 class="font-semibold text-blue-800 dark:text-blue-200 mb-2">Flexbox</h3>
				<ul class="text-sm text-blue-700 dark:text-blue-300 space-y-1">
					<li>• 1次元（横 or 縦）レイアウト</li>
					<li>• コンテンツ主導の配置</li>
					<li>• ナビ、ボタングループに最適</li>
				</ul>
			</div>
			<div class="p-4 rounded-lg bg-green-50 dark:bg-green-900/20 border border-green-200 dark:border-green-800">
				<h3 class="font-semibold text-green-800 dark:text-green-200 mb-2">Grid</h3>
				<ul class="text-sm text-green-700 dark:text-green-300 space-y-1">
					<li>• 2次元（横と縦）レイアウト</li>
					<li>• レイアウト主導の配置</li>
					<li>• ページ構造、カードリストに最適</li>
				</ul>
			</div>
		</div>
	</section>

	<div class="flex justify-between pt-6 border-t border-gray-200 dark:border-gray-700">
		<a href="/css/flexbox" class="inline-flex items-center gap-2 px-4 py-2 rounded-lg border border-gray-300 dark:border-gray-600 hover:bg-gray-100 dark:hover:bg-gray-800 transition-colors">
			<svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
				<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 19l-7-7 7-7" />
			</svg>
			前へ：Flexbox
		</a>
		<a href="/js/variables" class="inline-flex items-center gap-2 px-4 py-2 rounded-lg bg-primary-600 text-white hover:bg-primary-700 transition-colors">
			次へ：JavaScript
			<svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
				<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 5l7 7-7 7" />
			</svg>
		</a>
	</div>
</article>
