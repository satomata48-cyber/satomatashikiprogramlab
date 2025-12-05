<script>
	import CodePreview from '$lib/components/CodePreview.svelte';
</script>

<svelte:head>
	<title>CSS Flexbox | さとまたラボ</title>
</svelte:head>

<article>
	<h1 class="text-3xl font-bold mb-2">Flexbox</h1>
	<p class="text-lg text-gray-600 dark:text-gray-400 mb-8">
		柔軟な1次元レイアウトを実現するCSS
	</p>

	<!-- Flexboxとは -->
	<section class="mb-10">
		<h2 id="what-is" class="text-xl font-bold mb-4">Flexboxとは？</h2>

		<div class="p-6 rounded-xl bg-blue-50 dark:bg-blue-900/20 border border-blue-200 dark:border-blue-800 mb-6">
			<p class="text-blue-800 dark:text-blue-200 mb-4">
				<strong>日常での例え：</strong>本棚の本
			</p>
			<div class="text-sm text-blue-700 dark:text-blue-300 space-y-2">
				<p>本棚に本を並べる時、左から詰めたり、中央に寄せたり、均等に並べたりしますよね。</p>
				<p>Flexboxは「要素をどう並べるか」を簡単に指定できる仕組みです。</p>
			</div>
		</div>

		<div class="p-4 rounded-lg bg-amber-50 dark:bg-amber-900/20 border border-amber-200 dark:border-amber-800 mb-6">
			<p class="font-semibold text-amber-800 dark:text-amber-200">なぜFlexboxが必要？</p>
			<div class="text-sm text-amber-700 dark:text-amber-300 mt-2">
				<p class="mb-2"><strong>昔の方法（float）の問題点：</strong></p>
				<ul class="list-disc list-inside space-y-1 mb-3">
					<li>横並びにするだけで複雑なコードが必要</li>
					<li>「中央寄せ」「均等配置」が難しい</li>
					<li>高さを揃えるのが大変</li>
				</ul>
				<p><strong>Flexboxなら：</strong><code class="bg-amber-200 dark:bg-amber-800 px-1 rounded">display: flex</code> の1行で横並び完成！</p>
			</div>
		</div>

		<div class="p-4 rounded-lg bg-gray-100 dark:bg-gray-800 mb-6">
			<p class="font-semibold text-gray-800 dark:text-gray-200 mb-2">「1次元レイアウト」とは？</p>
			<p class="text-sm text-gray-700 dark:text-gray-300">
				<strong>横（行）</strong>か<strong>縦（列）</strong>の<strong>一方向</strong>に並べること。<br>
				両方向（格子状）に並べたい場合は「CSS Grid」を使います。
			</p>
		</div>
	</section>

	<section class="mb-10">
		<h2 id="basic" class="text-xl font-bold mb-4">基本の使い方</h2>

		<CodePreview
			title="display: flex"
			description="親要素に指定するだけで子要素が横並び"
			language="css"
			code={`.container {
  display: flex;
}

.item {
  padding: 20px;
  background: #3b82f6;
  color: white;
}`}
			previewHtml={`<div style="display:flex;gap:8px;"><div style="padding:20px;background:#3b82f6;color:white;border-radius:4px;">Item 1</div><div style="padding:20px;background:#3b82f6;color:white;border-radius:4px;">Item 2</div><div style="padding:20px;background:#3b82f6;color:white;border-radius:4px;">Item 3</div></div>`}
		/>
	</section>

	<section class="mb-10">
		<h2 id="direction" class="text-xl font-bold mb-4">flex-direction（並ぶ方向）</h2>

		<CodePreview
			title="row / column"
			description="横並び or 縦並び"
			language="css"
			code={`/* 横並び（デフォルト） */
.row { flex-direction: row; }

/* 横並び（逆順） */
.row-reverse { flex-direction: row-reverse; }

/* 縦並び */
.column { flex-direction: column; }

/* 縦並び（逆順） */
.column-reverse { flex-direction: column-reverse; }`}
			previewHtml={`<div style="display:flex;gap:16px;"><div><div style="font-size:12px;margin-bottom:4px;">row</div><div style="display:flex;flex-direction:row;gap:4px;"><div style="padding:8px;background:#3b82f6;color:white;border-radius:4px;font-size:12px;">1</div><div style="padding:8px;background:#3b82f6;color:white;border-radius:4px;font-size:12px;">2</div><div style="padding:8px;background:#3b82f6;color:white;border-radius:4px;font-size:12px;">3</div></div></div><div><div style="font-size:12px;margin-bottom:4px;">column</div><div style="display:flex;flex-direction:column;gap:4px;"><div style="padding:8px;background:#22c55e;color:white;border-radius:4px;font-size:12px;">1</div><div style="padding:8px;background:#22c55e;color:white;border-radius:4px;font-size:12px;">2</div><div style="padding:8px;background:#22c55e;color:white;border-radius:4px;font-size:12px;">3</div></div></div></div>`}
		/>
	</section>

	<section class="mb-10">
		<h2 id="justify" class="text-xl font-bold mb-4">justify-content（主軸の配置）</h2>

		<div class="p-4 rounded-lg bg-blue-50 dark:bg-blue-900/20 border border-blue-200 dark:border-blue-800 mb-6">
			<p class="font-semibold text-blue-800 dark:text-blue-200 mb-2">「主軸」とは？</p>
			<p class="text-sm text-blue-700 dark:text-blue-300">
				要素が並ぶ方向のこと。<br>
				<strong>横並び（row）</strong>の場合 → 主軸は<strong>横方向</strong>（左右の配置を制御）<br>
				<strong>縦並び（column）</strong>の場合 → 主軸は<strong>縦方向</strong>（上下の配置を制御）
			</p>
		</div>

		<CodePreview
			title="主軸方向の配置"
			description="横並びなら左右、縦並びなら上下の配置"
			language="css"
			code={`.container {
  display: flex;
  justify-content: flex-start;   /* 左寄せ（デフォルト）*/
  justify-content: flex-end;     /* 右寄せ */
  justify-content: center;       /* 中央 */
  justify-content: space-between;/* 両端に配置、間は均等 */
  justify-content: space-around; /* 各要素の周りに均等な余白 */
  justify-content: space-evenly; /* すべての間隔が均等 */
}`}
			previewHtml={`<div style="display:flex;flex-direction:column;gap:12px;"><div><div style="font-size:12px;margin-bottom:4px;">flex-start</div><div style="display:flex;justify-content:flex-start;gap:4px;background:#f3f4f6;padding:8px;border-radius:4px;"><div style="padding:8px;background:#3b82f6;color:white;border-radius:4px;font-size:12px;">1</div><div style="padding:8px;background:#3b82f6;color:white;border-radius:4px;font-size:12px;">2</div><div style="padding:8px;background:#3b82f6;color:white;border-radius:4px;font-size:12px;">3</div></div></div><div><div style="font-size:12px;margin-bottom:4px;">center</div><div style="display:flex;justify-content:center;gap:4px;background:#f3f4f6;padding:8px;border-radius:4px;"><div style="padding:8px;background:#8b5cf6;color:white;border-radius:4px;font-size:12px;">1</div><div style="padding:8px;background:#8b5cf6;color:white;border-radius:4px;font-size:12px;">2</div><div style="padding:8px;background:#8b5cf6;color:white;border-radius:4px;font-size:12px;">3</div></div></div><div><div style="font-size:12px;margin-bottom:4px;">space-between</div><div style="display:flex;justify-content:space-between;background:#f3f4f6;padding:8px;border-radius:4px;"><div style="padding:8px;background:#22c55e;color:white;border-radius:4px;font-size:12px;">1</div><div style="padding:8px;background:#22c55e;color:white;border-radius:4px;font-size:12px;">2</div><div style="padding:8px;background:#22c55e;color:white;border-radius:4px;font-size:12px;">3</div></div></div></div>`}
		/>
	</section>

	<section class="mb-10">
		<h2 id="align" class="text-xl font-bold mb-4">align-items（交差軸の配置）</h2>

		<div class="p-4 rounded-lg bg-blue-50 dark:bg-blue-900/20 border border-blue-200 dark:border-blue-800 mb-6">
			<p class="font-semibold text-blue-800 dark:text-blue-200 mb-2">「交差軸」とは？</p>
			<p class="text-sm text-blue-700 dark:text-blue-300">
				主軸と<strong>直交する</strong>方向のこと。<br>
				<strong>横並び（row）</strong>の場合 → 交差軸は<strong>縦方向</strong>（上下の配置を制御）<br>
				<strong>縦並び（column）</strong>の場合 → 交差軸は<strong>横方向</strong>（左右の配置を制御）
			</p>
		</div>

		<CodePreview
			title="交差軸方向の配置"
			description="横並びなら上下の配置"
			language="css"
			code={`.container {
  display: flex;
  height: 150px;
  align-items: stretch;    /* 高さを伸ばす（デフォルト）*/
  align-items: flex-start; /* 上揃え */
  align-items: flex-end;   /* 下揃え */
  align-items: center;     /* 中央揃え */
  align-items: baseline;   /* テキストのベースライン揃え */
}`}
			previewHtml={`<div style="display:flex;gap:16px;"><div><div style="font-size:12px;margin-bottom:4px;">flex-start</div><div style="display:flex;align-items:flex-start;gap:4px;background:#f3f4f6;padding:8px;border-radius:4px;height:80px;"><div style="padding:8px;background:#3b82f6;color:white;border-radius:4px;font-size:12px;">1</div><div style="padding:16px 8px;background:#3b82f6;color:white;border-radius:4px;font-size:12px;">2</div></div></div><div><div style="font-size:12px;margin-bottom:4px;">center</div><div style="display:flex;align-items:center;gap:4px;background:#f3f4f6;padding:8px;border-radius:4px;height:80px;"><div style="padding:8px;background:#8b5cf6;color:white;border-radius:4px;font-size:12px;">1</div><div style="padding:16px 8px;background:#8b5cf6;color:white;border-radius:4px;font-size:12px;">2</div></div></div><div><div style="font-size:12px;margin-bottom:4px;">flex-end</div><div style="display:flex;align-items:flex-end;gap:4px;background:#f3f4f6;padding:8px;border-radius:4px;height:80px;"><div style="padding:8px;background:#22c55e;color:white;border-radius:4px;font-size:12px;">1</div><div style="padding:16px 8px;background:#22c55e;color:white;border-radius:4px;font-size:12px;">2</div></div></div></div>`}
		/>
	</section>

	<section class="mb-10">
		<h2 id="gap" class="text-xl font-bold mb-4">gap（要素間の余白）</h2>

		<CodePreview
			title="gapプロパティ"
			description="子要素間の余白を一括指定"
			language="css"
			code={`.container {
  display: flex;
  gap: 20px;           /* 縦横同じ */
  gap: 10px 20px;      /* 縦 横 */
  row-gap: 10px;       /* 縦だけ */
  column-gap: 20px;    /* 横だけ */
}`}
			previewHtml={`<div style="display:flex;gap:20px;flex-wrap:wrap;background:#f3f4f6;padding:12px;border-radius:4px;"><div style="padding:16px;background:#3b82f6;color:white;border-radius:4px;">gap: 20px</div><div style="padding:16px;background:#3b82f6;color:white;border-radius:4px;">Item</div><div style="padding:16px;background:#3b82f6;color:white;border-radius:4px;">Item</div></div>`}
		/>
	</section>

	<section class="mb-10">
		<h2 id="wrap" class="text-xl font-bold mb-4">flex-wrap（折り返し）</h2>

		<CodePreview
			title="折り返しの制御"
			description="収まらない場合の振る舞い"
			language="css"
			code={`.container {
  display: flex;
  flex-wrap: nowrap;   /* 折り返さない（デフォルト）*/
  flex-wrap: wrap;     /* 折り返す */
  flex-wrap: wrap-reverse; /* 逆方向に折り返す */
}`}
			previewHtml={`<div style="display:flex;flex-wrap:wrap;gap:8px;background:#f3f4f6;padding:12px;border-radius:4px;max-width:200px;"><div style="padding:12px;background:#3b82f6;color:white;border-radius:4px;font-size:12px;">Item 1</div><div style="padding:12px;background:#3b82f6;color:white;border-radius:4px;font-size:12px;">Item 2</div><div style="padding:12px;background:#3b82f6;color:white;border-radius:4px;font-size:12px;">Item 3</div><div style="padding:12px;background:#3b82f6;color:white;border-radius:4px;font-size:12px;">Item 4</div></div>`}
		/>
	</section>

	<section class="mb-10">
		<h2 id="item" class="text-xl font-bold mb-4">子要素のプロパティ</h2>

		<div class="p-4 rounded-lg bg-blue-50 dark:bg-blue-900/20 border border-blue-200 dark:border-blue-800 mb-6">
			<p class="font-semibold text-blue-800 dark:text-blue-200 mb-2">flex-grow / flex-shrink / flex-basis って何？</p>
			<div class="text-sm text-blue-700 dark:text-blue-300 space-y-2">
				<p><strong>flex-grow（伸びる比率）</strong>：余ったスペースをどれだけ取るか（0=伸びない）</p>
				<p><strong>flex-shrink（縮む比率）</strong>：スペースが足りない時どれだけ縮むか（1=縮む）</p>
				<p><strong>flex-basis（基準サイズ）</strong>：伸縮前の初期サイズ</p>
			</div>
		</div>

		<CodePreview
			title="flex-grow / flex-shrink / flex-basis"
			description="子要素の伸縮を制御"
			language="css"
			code={`.item {
  flex-grow: 0;    /* 余白を埋めて伸びる比率（0=伸びない）*/
  flex-shrink: 1;  /* 縮む比率（1=縮む）*/
  flex-basis: auto;/* 基準サイズ */
}

/* 一括指定（grow shrink basis）*/
.item { flex: 0 1 auto; }  /* デフォルト */
.item { flex: 1; }         /* 均等に伸びる */
.item { flex: none; }      /* 伸縮しない */`}
			previewHtml={`<div style="display:flex;gap:8px;background:#f3f4f6;padding:12px;border-radius:4px;"><div style="flex:1;padding:12px;background:#3b82f6;color:white;border-radius:4px;text-align:center;font-size:12px;">flex: 1</div><div style="flex:2;padding:12px;background:#8b5cf6;color:white;border-radius:4px;text-align:center;font-size:12px;">flex: 2</div><div style="flex:1;padding:12px;background:#3b82f6;color:white;border-radius:4px;text-align:center;font-size:12px;">flex: 1</div></div>`}
		/>

		<CodePreview
			title="align-self"
			description="個別の交差軸配置"
			language="css"
			code={`.container {
  display: flex;
  align-items: flex-start;
}

.special {
  align-self: center; /* この要素だけ中央 */
}`}
			previewHtml={`<div style="display:flex;align-items:flex-start;gap:8px;background:#f3f4f6;padding:12px;border-radius:4px;height:100px;"><div style="padding:12px;background:#3b82f6;color:white;border-radius:4px;font-size:12px;">通常</div><div style="align-self:center;padding:12px;background:#ec4899;color:white;border-radius:4px;font-size:12px;">align-self: center</div><div style="padding:12px;background:#3b82f6;color:white;border-radius:4px;font-size:12px;">通常</div></div>`}
		/>
	</section>

	<section class="mb-10">
		<h2 id="patterns" class="text-xl font-bold mb-4">よく使うパターン</h2>

		<CodePreview
			title="完全中央配置"
			description="縦横中央に配置"
			language="css"
			code={`.center {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 200px;
}`}
			previewHtml={`<div style="display:flex;justify-content:center;align-items:center;height:120px;background:#f3f4f6;border-radius:4px;"><div style="padding:16px;background:#3b82f6;color:white;border-radius:4px;">中央配置</div></div>`}
		/>

		<CodePreview
			title="ヘッダーレイアウト"
			description="ロゴ左、ナビ右"
			language="css"
			code={`header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 0 20px;
}`}
			previewHtml={`<header style="display:flex;justify-content:space-between;align-items:center;padding:12px 20px;background:#1f2937;border-radius:4px;"><div style="font-weight:bold;color:white;">Logo</div><nav style="display:flex;gap:16px;"><a style="color:#9ca3af;">Home</a><a style="color:#9ca3af;">About</a><a style="color:#9ca3af;">Contact</a></nav></header>`}
		/>
	</section>

	<div class="flex justify-between pt-6 border-t border-gray-200 dark:border-gray-700">
		<a href="/css/box-model" class="inline-flex items-center gap-2 px-4 py-2 rounded-lg border border-gray-300 dark:border-gray-600 hover:bg-gray-100 dark:hover:bg-gray-800 transition-colors">
			<svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
				<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 19l-7-7 7-7" />
			</svg>
			前へ：ボックスモデル
		</a>
		<a href="/css/grid" class="inline-flex items-center gap-2 px-4 py-2 rounded-lg bg-primary-600 text-white hover:bg-primary-700 transition-colors">
			次へ：Grid
			<svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
				<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 5l7 7-7 7" />
			</svg>
		</a>
	</div>
</article>
