<script>
	import CodePreview from '$lib/components/CodePreview.svelte';
</script>

<svelte:head>
	<title>CSS ボックスモデル | さとまたラボ</title>
</svelte:head>

<article>
	<h1 class="text-3xl font-bold mb-2">ボックスモデル</h1>
	<p class="text-lg text-gray-600 dark:text-gray-400 mb-8">
		すべてのHTML要素を囲む「箱」の仕組みを理解する
	</p>

	<section class="mb-10">
		<h2 id="overview" class="text-xl font-bold mb-4">ボックスモデルとは</h2>

		<div class="p-6 rounded-xl bg-blue-50 dark:bg-blue-900/20 border border-blue-200 dark:border-blue-800 mb-6">
			<p class="text-blue-800 dark:text-blue-200 mb-4">
				<strong>日常での例え：</strong>プレゼントの箱
			</p>
			<div class="text-sm text-blue-700 dark:text-blue-300 space-y-2">
				<p><strong>content（内容）</strong>= プレゼント本体</p>
				<p><strong>padding（内側の余白）</strong>= 緩衝材（プチプチ）</p>
				<p><strong>border（枠線）</strong>= 箱の厚み</p>
				<p><strong>margin（外側の余白）</strong>= 箱と箱の間隔</p>
			</div>
		</div>

		<div class="p-4 rounded-lg bg-amber-50 dark:bg-amber-900/20 border border-amber-200 dark:border-amber-800 mb-6">
			<p class="font-semibold text-amber-800 dark:text-amber-200">なぜボックスモデルを理解する必要がある？</p>
			<p class="text-sm text-amber-700 dark:text-amber-300 mt-2">
				CSSでは<strong>すべての要素が「箱」</strong>として扱われます。<br>
				文字、画像、ボタン...すべてが箱。この箱の仕組みを理解しないと、<br>
				「なぜ要素が思った位置にならないのか」が分からなくなります。
			</p>
		</div>

		<div class="p-6 rounded-xl bg-gray-100 dark:bg-gray-800 mb-4">
			<div class="max-w-md mx-auto">
				<!-- ボックスモデル図解 -->
				<div class="bg-orange-200 dark:bg-orange-900 p-4 rounded text-center text-sm">
					<div class="text-orange-800 dark:text-orange-200 mb-1">margin（外側の余白）</div>
					<div class="bg-yellow-200 dark:bg-yellow-900 p-4 rounded">
						<div class="text-yellow-800 dark:text-yellow-200 mb-1">border（枠線）</div>
						<div class="bg-green-200 dark:bg-green-900 p-4 rounded">
							<div class="text-green-800 dark:text-green-200 mb-1">padding（内側の余白）</div>
							<div class="bg-blue-200 dark:bg-blue-900 p-4 rounded">
								<div class="text-blue-800 dark:text-blue-200">content（内容）</div>
							</div>
						</div>
					</div>
				</div>
			</div>
		</div>
	</section>

	<section class="mb-10">
		<h2 id="content" class="text-xl font-bold mb-4">Content（内容）</h2>

		<CodePreview
			title="width と height"
			description="内容エリアのサイズを指定"
			language="css"
			code={`.box {
  width: 200px;
  height: 100px;
  background: lightblue;
}

/* 最大・最小サイズ */
.responsive {
  width: 100%;
  max-width: 500px;
  min-height: 200px;
}`}
			previewHtml={`<div style="width:200px;height:100px;background:lightblue;display:flex;align-items:center;justify-content:center;">200px × 100px</div>`}
		/>
	</section>

	<section class="mb-10">
		<h2 id="padding" class="text-xl font-bold mb-4">Padding（内側の余白）</h2>

		<CodePreview
			title="padding の指定方法"
			description="内容と枠線の間の余白"
			language="css"
			code={`/* 全方向同じ値 */
.box1 { padding: 20px; }

/* 上下 | 左右 */
.box2 { padding: 10px 20px; }

/* 上 | 左右 | 下 */
.box3 { padding: 10px 20px 30px; }

/* 上 | 右 | 下 | 左（時計回り） */
.box4 { padding: 10px 20px 30px 40px; }

/* 個別指定 */
.box5 {
  padding-top: 10px;
  padding-right: 20px;
  padding-bottom: 30px;
  padding-left: 40px;
}`}
			previewHtml={`<div style="display:flex;gap:12px;flex-wrap:wrap;"><div style="padding:20px;background:#dbeafe;border:2px dashed #3b82f6;">padding: 20px</div><div style="padding:10px 30px;background:#dcfce7;border:2px dashed #22c55e;">padding: 10px 30px</div></div>`}
		/>
	</section>

	<section class="mb-10">
		<h2 id="border" class="text-xl font-bold mb-4">Border（枠線）</h2>

		<CodePreview
			title="border の指定方法"
			description="太さ、スタイル、色を指定"
			language="css"
			code={`/* 一括指定 */
.box1 {
  border: 2px solid black;
}

/* 個別指定 */
.box2 {
  border-width: 2px;
  border-style: solid;
  border-color: red;
}

/* 片側だけ */
.box3 {
  border-bottom: 3px solid blue;
}

/* 角丸 */
.box4 {
  border: 1px solid gray;
  border-radius: 10px;
}`}
			previewHtml={`<div style="display:flex;gap:12px;flex-wrap:wrap;"><div style="padding:12px;border:2px solid black;">solid</div><div style="padding:12px;border:2px dashed #3b82f6;">dashed</div><div style="padding:12px;border:2px dotted #22c55e;">dotted</div><div style="padding:12px;border:2px solid #6b7280;border-radius:10px;">border-radius</div></div>`}
		/>

		<CodePreview
			title="border-style の種類"
			description="様々な枠線スタイル"
			language="css"
			code={`border-style: solid;   /* 実線 */
border-style: dashed;  /* 破線 */
border-style: dotted;  /* 点線 */
border-style: double;  /* 二重線 */
border-style: groove;  /* 溝 */
border-style: ridge;   /* 尾根 */
border-style: inset;   /* 内側 */
border-style: outset;  /* 外側 */
border-style: none;    /* なし */`}
			previewHtml={`<div style="display:grid;grid-template-columns:repeat(3,1fr);gap:8px;font-size:12px;"><div style="padding:8px;border:3px solid #333;text-align:center;">solid</div><div style="padding:8px;border:3px dashed #333;text-align:center;">dashed</div><div style="padding:8px;border:3px dotted #333;text-align:center;">dotted</div><div style="padding:8px;border:4px double #333;text-align:center;">double</div><div style="padding:8px;border:4px groove #888;text-align:center;">groove</div><div style="padding:8px;border:4px ridge #888;text-align:center;">ridge</div></div>`}
		/>
	</section>

	<section class="mb-10">
		<h2 id="margin" class="text-xl font-bold mb-4">Margin（外側の余白）</h2>

		<CodePreview
			title="margin の指定方法"
			description="要素間の余白"
			language="css"
			code={`/* paddingと同じ記法 */
.box1 { margin: 20px; }
.box2 { margin: 10px 20px; }

/* 中央寄せ */
.center {
  width: 200px;
  margin: 0 auto;
}

/* 負のマージン */
.overlap {
  margin-top: -20px;
}`}
			previewHtml={`<div style="background:#f3f4f6;padding:20px;"><div style="width:150px;margin:0 auto;padding:12px;background:#3b82f6;color:white;text-align:center;border-radius:4px;">margin: 0 auto<br>(中央寄せ)</div></div>`}
		/>

		<div class="p-4 rounded-lg bg-amber-50 dark:bg-amber-900/20 border border-amber-200 dark:border-amber-800 mb-4">
			<p class="font-semibold text-amber-800 dark:text-amber-200">マージンの相殺に注意</p>
			<p class="text-sm text-amber-700 dark:text-amber-300 mt-1">
				縦方向で隣接する要素のmarginは、大きい方の値だけが適用されます（相殺）
			</p>
		</div>
	</section>

	<section class="mb-10">
		<h2 id="box-sizing" class="text-xl font-bold mb-4">box-sizing</h2>

		<div class="p-4 rounded-lg bg-blue-50 dark:bg-blue-900/20 border border-blue-200 dark:border-blue-800 mb-6">
			<p class="font-semibold text-blue-800 dark:text-blue-200 mb-2">box-sizingとは？なぜ必要？</p>
			<p class="text-sm text-blue-700 dark:text-blue-300 mb-3">
				「幅200px」と指定した時、<strong>何を200pxにするか</strong>を決めるプロパティです。
			</p>
			<div class="text-sm text-blue-700 dark:text-blue-300">
				<strong>問題</strong>：width: 200px + padding: 20px + border: 5px = 実際の幅250px になってしまう！<br>
				<strong>解決</strong>：<code class="bg-blue-200 dark:bg-blue-800 px-1 rounded">box-sizing: border-box</code> で「全部込みで200px」にできる
			</div>
		</div>

		<CodePreview
			title="content-box vs border-box"
			description="幅の計算方法を変更"
			language="css"
			code={`/* デフォルト: content-box */
/* width = 内容のみ */
/* 実際の幅 = width + padding + border */
.content-box {
  box-sizing: content-box;
  width: 200px;
  padding: 20px;
  border: 5px solid;
  /* 実際の幅 = 200 + 40 + 10 = 250px */
}

/* 推奨: border-box */
/* width = 内容 + padding + border */
.border-box {
  box-sizing: border-box;
  width: 200px;
  padding: 20px;
  border: 5px solid;
  /* 実際の幅 = 200px（指定通り） */
}

/* 全要素に適用（推奨） */
*, *::before, *::after {
  box-sizing: border-box;
}`}
			previewHtml={`<div style="display:flex;flex-direction:column;gap:12px;"><div style="width:200px;"><div style="font-size:12px;margin-bottom:4px;">content-box (実際: 250px)</div><div style="box-sizing:content-box;width:200px;padding:20px;border:5px solid #ef4444;background:#fee2e2;">width: 200px</div></div><div style="width:200px;"><div style="font-size:12px;margin-bottom:4px;">border-box (実際: 200px)</div><div style="box-sizing:border-box;width:200px;padding:20px;border:5px solid #22c55e;background:#dcfce7;">width: 200px</div></div></div>`}
		/>
	</section>

	<section class="mb-10">
		<h2 id="display" class="text-xl font-bold mb-4">display プロパティ</h2>

		<div class="p-4 rounded-lg bg-blue-50 dark:bg-blue-900/20 border border-blue-200 dark:border-blue-800 mb-6">
			<p class="font-semibold text-blue-800 dark:text-blue-200 mb-2">displayとは？</p>
			<p class="text-sm text-blue-700 dark:text-blue-300 mb-3">
				要素が<strong>どのように表示されるか</strong>を決めるプロパティです。
			</p>
			<div class="text-sm text-blue-700 dark:text-blue-300">
				<strong>block</strong>：段ボール箱のように、縦に積み重なる（div, p, h1など）<br>
				<strong>inline</strong>：文章の中の単語のように、横に並ぶ（span, a, strongなど）<br>
				<strong>inline-block</strong>：横に並ぶけど、幅・高さを指定できる<br>
				<strong>none</strong>：完全に非表示（画面から消える）
			</div>
		</div>

		<CodePreview
			title="表示モードの変更"
			description="block, inline, inline-block, none"
			language="css"
			code={`/* ブロック要素に変換 */
span { display: block; }

/* インライン要素に変換 */
div { display: inline; }

/* インラインだけど幅・高さ指定可能 */
.badge {
  display: inline-block;
  width: 100px;
  padding: 5px;
}

/* 非表示 */
.hidden { display: none; }`}
			previewHtml={`<div style="display:flex;flex-direction:column;gap:8px;"><div><span style="display:inline-block;padding:4px 8px;background:#dbeafe;margin-right:4px;">inline</span><span style="display:inline-block;padding:4px 8px;background:#dbeafe;">inline</span></div><div style="display:flex;gap:4px;"><div style="display:inline-block;width:80px;padding:8px;background:#dcfce7;text-align:center;font-size:12px;">inline-block</div><div style="display:inline-block;width:80px;padding:8px;background:#dcfce7;text-align:center;font-size:12px;">inline-block</div></div></div>`}
		/>
	</section>

	<div class="flex justify-between pt-6 border-t border-gray-200 dark:border-gray-700">
		<a href="/css/selectors" class="inline-flex items-center gap-2 px-4 py-2 rounded-lg border border-gray-300 dark:border-gray-600 hover:bg-gray-100 dark:hover:bg-gray-800 transition-colors">
			<svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
				<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 19l-7-7 7-7" />
			</svg>
			前へ：セレクタ
		</a>
		<a href="/css/flexbox" class="inline-flex items-center gap-2 px-4 py-2 rounded-lg bg-primary-600 text-white hover:bg-primary-700 transition-colors">
			次へ：Flexbox
			<svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
				<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 5l7 7-7 7" />
			</svg>
		</a>
	</div>
</article>
