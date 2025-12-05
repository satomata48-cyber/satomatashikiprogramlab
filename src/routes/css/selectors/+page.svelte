<script>
	import CodePreview from '$lib/components/CodePreview.svelte';
	import CodeExplain from '$lib/components/CodeExplain.svelte';
	import FeatureCard from '$lib/components/FeatureCard.svelte';

	const features = [
		{ icon: '🎨', title: 'スタイリング', description: '色、フォント、サイズなどを指定', tag: '基本' },
		{ icon: '📐', title: 'レイアウト', description: 'Flexbox、Gridで配置を制御', tag: '重要' },
		{ icon: '📱', title: 'レスポンシブ', description: '画面サイズに応じたデザイン', tag: '重要' },
		{ icon: '✨', title: 'アニメーション', description: '動きのあるエフェクトを追加', tag: '応用' },
		{ icon: '🔲', title: 'ボックスモデル', description: 'margin、padding、borderの制御', tag: '基本' },
		{ icon: '🎭', title: '疑似クラス', description: 'hover、focusなどの状態スタイル', tag: '基本' }
	];
</script>

<svelte:head>
	<title>CSS セレクタ | さとまたラボ</title>
</svelte:head>

<article>
	<h1 class="text-3xl font-bold mb-2">CSS</h1>
	<p class="text-lg text-gray-600 dark:text-gray-400 mb-8">
		Webページの見た目を装飾するスタイルシート言語
	</p>

	<!-- できること一覧 -->
	<section class="mb-10">
		<h2 id="features" class="text-xl font-bold mb-4">CSSでできること</h2>
		<div class="grid grid-cols-1 md:grid-cols-2 gap-3">
			{#each features as feature}
				<FeatureCard {...feature} />
			{/each}
		</div>
	</section>

	<!-- CSSとは -->
	<section class="mb-10">
		<h2 id="what-is" class="text-xl font-bold mb-4">CSSとは何か？</h2>

		<div class="p-6 rounded-xl bg-blue-50 dark:bg-blue-900/20 border border-blue-200 dark:border-blue-800 mb-6">
			<p class="text-blue-800 dark:text-blue-200 mb-4">
				<strong>日常での例え：</strong>家の「内装」
			</p>
			<div class="grid grid-cols-1 md:grid-cols-2 gap-4 text-sm">
				<div class="p-3 bg-white dark:bg-gray-800 rounded-lg">
					<div class="font-semibold text-blue-700 dark:text-blue-300 mb-2">HTML = 家の骨組み</div>
					<p class="text-gray-600 dark:text-gray-400">
						壁、床、窓の「位置」を決める<br>
						「ここにリビング、ここに寝室」
					</p>
				</div>
				<div class="p-3 bg-white dark:bg-gray-800 rounded-lg">
					<div class="font-semibold text-blue-700 dark:text-blue-300 mb-2">CSS = 内装・デザイン</div>
					<p class="text-gray-600 dark:text-gray-400">
						壁の色、床の材質、家具の配置<br>
						「白い壁、木目の床、ソファはここ」
					</p>
				</div>
			</div>
		</div>

		<div class="prose dark:prose-invert max-w-none mb-6">
			<p>
				<strong>CSS（Cascading Style Sheets）</strong>は、HTMLで作った構造に「見た目」を付ける言語です。
				色、サイズ、配置、アニメーションなど、表示に関するすべてを制御します。
			</p>
		</div>

		<div class="p-4 rounded-lg bg-amber-50 dark:bg-amber-900/20 border border-amber-200 dark:border-amber-800 mb-6">
			<p class="font-semibold text-amber-800 dark:text-amber-200">なぜHTMLとCSSを分ける？</p>
			<p class="text-sm text-amber-700 dark:text-amber-300 mt-2">
				<strong>分業できる</strong>：構造を変えずにデザインだけ変更可能<br>
				<strong>再利用できる</strong>：同じCSSを複数ページで使い回せる<br>
				<strong>保守しやすい</strong>：「色を変えたい」→ CSSだけ修正すればOK
			</p>
		</div>

		<div class="grid grid-cols-1 md:grid-cols-2 gap-4 mb-6">
			<div class="p-4 rounded-lg bg-red-50 dark:bg-red-900/20 border border-red-200 dark:border-red-800">
				<h3 class="font-semibold text-red-800 dark:text-red-200 mb-2">HTMLだけの場合</h3>
				<div class="bg-white dark:bg-gray-900 p-3 rounded border">
					<h1>見出し</h1>
					<p>テキスト</p>
				</div>
				<p class="text-sm text-red-700 dark:text-red-300 mt-2">→ 素っ気ない表示</p>
			</div>
			<div class="p-4 rounded-lg bg-green-50 dark:bg-green-900/20 border border-green-200 dark:border-green-800">
				<h3 class="font-semibold text-green-800 dark:text-green-200 mb-2">CSS適用後</h3>
				<div class="bg-white dark:bg-gray-900 p-3 rounded border">
					<h1 style="color: #3b82f6; font-size: 20px; font-weight: bold;">見出し</h1>
					<p style="color: #6b7280; line-height: 1.6;">テキスト</p>
				</div>
				<p class="text-sm text-green-700 dark:text-green-300 mt-2">→ デザインが整う</p>
			</div>
		</div>
	</section>

	<!-- CSSの基本構文 -->
	<section class="mb-10">
		<h2 id="syntax" class="text-xl font-bold mb-4">CSSの基本構文</h2>

		<div class="p-6 rounded-xl bg-gray-100 dark:bg-gray-800 mb-6">
			<div class="text-center mb-4">
				<code class="text-lg bg-white dark:bg-gray-900 px-4 py-2 rounded-lg">
					<span class="text-purple-600 dark:text-purple-400">セレクタ</span>
					&#123;
					<span class="text-blue-600 dark:text-blue-400">プロパティ</span>:
					<span class="text-green-600 dark:text-green-400">値</span>;
					&#125;
				</code>
			</div>
			<div class="grid grid-cols-3 gap-4 text-center text-sm">
				<div>
					<div class="text-purple-600 dark:text-purple-400 font-semibold">セレクタ</div>
					<div class="text-gray-600 dark:text-gray-400">「どの要素に」</div>
				</div>
				<div>
					<div class="text-blue-600 dark:text-blue-400 font-semibold">プロパティ</div>
					<div class="text-gray-600 dark:text-gray-400">「何を」</div>
				</div>
				<div>
					<div class="text-green-600 dark:text-green-400 font-semibold">値</div>
					<div class="text-gray-600 dark:text-gray-400">「どうする」</div>
				</div>
			</div>
		</div>

		<CodeExplain
			title="CSSの書き方"
			language="css"
			code={`/* 要素セレクタ：すべてのp要素 */
p {
  color: blue;
  font-size: 16px;
}

/* クラスセレクタ：.が付いたクラス名 */
.highlight {
  background-color: yellow;
}

/* IDセレクタ：#が付いたID名 */
#header {
  height: 60px;
}`}
			explanations={[
				{ line: 1, code: '/* ... */', text: 'コメント。人間用のメモで、ブラウザには無視される' },
				{ line: 2, code: 'p', text: '要素セレクタ。すべての<p>タグにスタイルを適用' },
				{ line: 3, code: 'color: blue', text: '文字色を青に。colorは文字色を指定するプロパティ' },
				{ line: 4, code: 'font-size: 16px', text: '文字サイズを16ピクセルに' },
				{ line: 8, code: '.highlight', text: 'クラスセレクタ。class="highlight"が付いた要素に適用' },
				{ line: 13, code: '#header', text: 'IDセレクタ。id="header"が付いた要素に適用（ページで1つだけ）' },
			]}
		/>
	</section>

	<!-- セレクタの種類 -->
	<section class="mb-10">
		<h2 id="selectors" class="text-xl font-bold mb-4">セレクタの種類</h2>

		<div class="overflow-x-auto mb-6">
			<table class="w-full text-sm">
				<thead>
					<tr class="border-b border-gray-200 dark:border-gray-700">
						<th class="text-left py-2 px-4">セレクタ</th>
						<th class="text-left py-2 px-4">例</th>
						<th class="text-left py-2 px-4">意味</th>
					</tr>
				</thead>
				<tbody>
					<tr class="border-b border-gray-200 dark:border-gray-700">
						<td class="py-2 px-4 font-medium">要素</td>
						<td class="py-2 px-4 font-mono text-blue-600">p</td>
						<td class="py-2 px-4">すべての&lt;p&gt;要素</td>
					</tr>
					<tr class="border-b border-gray-200 dark:border-gray-700">
						<td class="py-2 px-4 font-medium">クラス</td>
						<td class="py-2 px-4 font-mono text-blue-600">.card</td>
						<td class="py-2 px-4">class="card"を持つ要素</td>
					</tr>
					<tr class="border-b border-gray-200 dark:border-gray-700">
						<td class="py-2 px-4 font-medium">ID</td>
						<td class="py-2 px-4 font-mono text-blue-600">#nav</td>
						<td class="py-2 px-4">id="nav"を持つ要素</td>
					</tr>
					<tr class="border-b border-gray-200 dark:border-gray-700">
						<td class="py-2 px-4 font-medium">子孫</td>
						<td class="py-2 px-4 font-mono text-blue-600">div p</td>
						<td class="py-2 px-4">div内のすべてのp</td>
					</tr>
					<tr class="border-b border-gray-200 dark:border-gray-700">
						<td class="py-2 px-4 font-medium">複数</td>
						<td class="py-2 px-4 font-mono text-blue-600">h1, h2</td>
						<td class="py-2 px-4">h1とh2の両方</td>
					</tr>
				</tbody>
			</table>
		</div>

		<div class="p-4 rounded-lg bg-amber-50 dark:bg-amber-900/20 border border-amber-200 dark:border-amber-800">
			<p class="font-semibold text-amber-800 dark:text-amber-200">💡 クラスとIDの使い分け</p>
			<p class="text-sm text-amber-700 dark:text-amber-300 mt-2">
				<strong>クラス（.）</strong>：同じスタイルを複数の要素に使いたい時<br>
				<strong>ID（#）</strong>：ページ内で1つだけの要素を指定したい時<br>
				→ 基本的にはクラスを使い、IDはJavaScriptとの連携時に使うことが多い
			</p>
		</div>
	</section>

	<!-- よく使うプロパティ -->
	<section class="mb-10">
		<h2 id="properties" class="text-xl font-bold mb-4">よく使うプロパティ</h2>

		<CodePreview
			title="色とフォント"
			description="テキストの見た目を変更"
			language="css"
			code={`.styled-text {
  color: #e91e63;           /* 文字色 */
  background-color: #f5f5f5; /* 背景色 */
  font-size: 20px;          /* 文字サイズ */
  font-weight: bold;        /* 太さ（bold/normal/数値） */
  font-family: sans-serif;  /* フォント種類 */
  text-align: center;       /* 揃え（left/center/right） */
  line-height: 1.6;         /* 行間（1.5〜1.8が読みやすい） */
}`}
			previewHtml={`<div style="color:#e91e63;background:#f5f5f5;font-size:20px;font-weight:bold;font-family:sans-serif;text-align:center;line-height:1.6;padding:16px;border-radius:8px;">スタイル適用済みテキスト</div>`}
		/>

		<div class="p-4 rounded-lg bg-gray-100 dark:bg-gray-800 mb-6">
			<p class="text-sm text-gray-700 dark:text-gray-300">
				<strong>色の指定方法</strong><br>
				・<code class="bg-gray-200 dark:bg-gray-700 px-1 rounded">red</code>, <code class="bg-gray-200 dark:bg-gray-700 px-1 rounded">blue</code>：色名（約140種類）<br>
				・<code class="bg-gray-200 dark:bg-gray-700 px-1 rounded">#ff0000</code>：16進数（#RRGGBB）<br>
				・<code class="bg-gray-200 dark:bg-gray-700 px-1 rounded">rgb(255, 0, 0)</code>：RGB値（0-255）<br>
				・<code class="bg-gray-200 dark:bg-gray-700 px-1 rounded">rgba(255, 0, 0, 0.5)</code>：RGB+透明度
			</p>
		</div>

		<CodePreview
			title="ボックスモデル"
			description="余白と枠線"
			language="css"
			code={`.box {
  /* 内側の余白（内容と枠線の間） */
  padding: 20px;

  /* 外側の余白（他の要素との間） */
  margin: 10px;

  /* 枠線（太さ スタイル 色） */
  border: 2px solid #333;

  /* 角丸 */
  border-radius: 8px;

  /* 横幅 */
  width: 200px;
}`}
			previewHtml={`<div style="padding:20px;margin:10px;border:2px solid #333;border-radius:8px;width:200px;background:#f3f4f6;">ボックス要素</div>`}
		/>

		<div class="p-4 rounded-lg bg-gray-100 dark:bg-gray-800 mb-6">
			<p class="text-sm text-gray-700 dark:text-gray-300">
				<strong>padding/marginの省略記法</strong><br>
				・<code class="bg-gray-200 dark:bg-gray-700 px-1 rounded">padding: 10px</code>：全方向10px<br>
				・<code class="bg-gray-200 dark:bg-gray-700 px-1 rounded">padding: 10px 20px</code>：上下10px、左右20px<br>
				・<code class="bg-gray-200 dark:bg-gray-700 px-1 rounded">padding: 10px 20px 30px 40px</code>：上 右 下 左（時計回り）
			</p>
		</div>
	</section>

	<!-- Flexbox -->
	<section class="mb-10">
		<h2 id="flexbox" class="text-xl font-bold mb-4">Flexbox（横並び）</h2>

		<div class="p-4 rounded-lg bg-blue-50 dark:bg-blue-900/20 border border-blue-200 dark:border-blue-800 mb-6">
			<p class="font-semibold text-blue-800 dark:text-blue-200 mb-2">Flexbox（フレックスボックス）とは？</p>
			<p class="text-sm text-blue-700 dark:text-blue-300 mb-3">
				要素を<strong>横並び</strong>や<strong>縦並び</strong>に配置するための仕組みです。
			</p>
			<p class="font-semibold text-blue-800 dark:text-blue-200 mb-2">なぜFlexboxが必要？</p>
			<p class="text-sm text-blue-700 dark:text-blue-300">
				<strong>昔の方法</strong>：floatやtableを使って無理やり横並びに → 複雑でバグの原因に<br>
				<strong>Flexbox</strong>：<code class="bg-blue-200 dark:bg-blue-800 px-1 rounded">display: flex</code>の1行で横並びに → シンプルで直感的
			</p>
		</div>

		<CodeExplain
			title="要素を横並びにする"
			language="css"
			code={`.container {
  display: flex;
  justify-content: center;
  align-items: center;
  gap: 10px;
}

.item {
  padding: 20px;
  background: #4f46e5;
  color: white;
}`}
			explanations={[
				{ line: 2, code: 'display: flex', text: 'この1行で子要素が横並びになる。Flexboxを有効化' },
				{ line: 3, code: 'justify-content: center', text: '主軸（横方向）の配置。centerで中央寄せ' },
				{ line: 4, code: 'align-items: center', text: '交差軸（縦方向）の配置。centerで上下中央' },
				{ line: 5, code: 'gap: 10px', text: '子要素間の余白。marginの代わりに使えて便利' },
			]}
		/>

		<CodePreview
			title="Flexboxの配置例"
			description="justify-contentの違い"
			language="css"
			code={`/* 左寄せ（デフォルト） */
.left { justify-content: flex-start; }

/* 中央 */
.center { justify-content: center; }

/* 右寄せ */
.right { justify-content: flex-end; }

/* 両端に配置 */
.between { justify-content: space-between; }`}
			previewHtml={`<div style="display:flex;flex-direction:column;gap:12px;"><div style="display:flex;justify-content:flex-start;gap:4px;background:#f3f4f6;padding:8px;border-radius:4px;"><span style="font-size:12px;color:#6b7280;width:80px;">flex-start</span><div style="padding:8px;background:#3b82f6;color:white;border-radius:4px;font-size:12px;">1</div><div style="padding:8px;background:#3b82f6;color:white;border-radius:4px;font-size:12px;">2</div></div><div style="display:flex;justify-content:center;gap:4px;background:#f3f4f6;padding:8px;border-radius:4px;"><div style="padding:8px;background:#8b5cf6;color:white;border-radius:4px;font-size:12px;">1</div><div style="padding:8px;background:#8b5cf6;color:white;border-radius:4px;font-size:12px;">2</div></div><div style="display:flex;justify-content:space-between;background:#f3f4f6;padding:8px;border-radius:4px;"><div style="padding:8px;background:#22c55e;color:white;border-radius:4px;font-size:12px;">1</div><div style="padding:8px;background:#22c55e;color:white;border-radius:4px;font-size:12px;">2</div></div></div>`}
		/>
	</section>

	<!-- hover -->
	<section class="mb-10">
		<h2 id="hover" class="text-xl font-bold mb-4">ホバーエフェクト</h2>

		<div class="p-4 rounded-lg bg-blue-50 dark:bg-blue-900/20 border border-blue-200 dark:border-blue-800 mb-6">
			<p class="font-semibold text-blue-800 dark:text-blue-200 mb-2">疑似クラス（ぎじクラス）とは？</p>
			<p class="text-sm text-blue-700 dark:text-blue-300 mb-3">
				要素の<strong>状態</strong>に応じてスタイルを変える仕組みです。<br>
				「マウスが乗った時」「クリック中」「入力欄にフォーカスした時」など。
			</p>
			<p class="font-semibold text-blue-800 dark:text-blue-200 mb-2">なぜ疑似クラスが必要？</p>
			<p class="text-sm text-blue-700 dark:text-blue-300">
				<strong>ユーザーへのフィードバック</strong>：ボタンにマウスを乗せた時に色が変わると「押せそう」と分かる<br>
				<strong>操作性の向上</strong>：今どこを操作しているか視覚的に分かりやすくなる
			</p>
		</div>

		<CodeExplain
			title="マウスを乗せた時のスタイル"
			language="css"
			code={`.button {
  padding: 12px 24px;
  background: #3b82f6;
  color: white;
  border: none;
  border-radius: 6px;
  cursor: pointer;
  transition: all 0.2s;
}

.button:hover {
  background: #2563eb;
  transform: translateY(-2px);
}`}
			explanations={[
				{ line: 8, code: 'transition: all 0.2s', text: 'すべての変化を0.2秒かけて滑らかにする。これがないとカクカク変わる' },
				{ line: 11, code: ':hover', text: '疑似クラス。マウスが乗っている時だけ適用されるスタイル' },
				{ line: 12, code: 'background: #2563eb', text: '少し暗い青に変更' },
				{ line: 13, code: 'translateY(-2px)', text: '上に2px移動。押せそうな感じを演出' },
			]}
		/>

		<div class="p-4 rounded-lg bg-gray-100 dark:bg-gray-800 mb-6">
			<p class="text-sm text-gray-700 dark:text-gray-300">
				<strong>他の疑似クラス</strong><br>
				・<code class="bg-gray-200 dark:bg-gray-700 px-1 rounded">:focus</code>：フォーカス時（入力欄をクリックした時など）<br>
				・<code class="bg-gray-200 dark:bg-gray-700 px-1 rounded">:active</code>：クリック中<br>
				・<code class="bg-gray-200 dark:bg-gray-700 px-1 rounded">:first-child</code>：最初の子要素<br>
				・<code class="bg-gray-200 dark:bg-gray-700 px-1 rounded">:nth-child(2)</code>：2番目の子要素
			</p>
		</div>
	</section>

	<!-- CSSの書き方 -->
	<section class="mb-10">
		<h2 id="how-to-write" class="text-xl font-bold mb-4">CSSの3つの書き方</h2>

		<div class="grid grid-cols-1 md:grid-cols-3 gap-4">
			<div class="p-4 rounded-lg bg-red-50 dark:bg-red-900/20 border border-red-200 dark:border-red-800">
				<h3 class="font-semibold text-red-800 dark:text-red-200 mb-2">❌ インライン</h3>
				<code class="text-xs">&lt;p style="color:red"&gt;</code>
				<p class="text-sm text-red-700 dark:text-red-300 mt-2">再利用できず非推奨</p>
			</div>
			<div class="p-4 rounded-lg bg-yellow-50 dark:bg-yellow-900/20 border border-yellow-200 dark:border-yellow-800">
				<h3 class="font-semibold text-yellow-800 dark:text-yellow-200 mb-2">△ 内部CSS</h3>
				<code class="text-xs">&lt;style&gt;タグ内</code>
				<p class="text-sm text-yellow-700 dark:text-yellow-300 mt-2">そのページでのみ有効</p>
			</div>
			<div class="p-4 rounded-lg bg-green-50 dark:bg-green-900/20 border border-green-200 dark:border-green-800">
				<h3 class="font-semibold text-green-800 dark:text-green-200 mb-2">✅ 外部CSS</h3>
				<code class="text-xs">.cssファイルをリンク</code>
				<p class="text-sm text-green-700 dark:text-green-300 mt-2">複数ページで共有可能</p>
			</div>
		</div>
	</section>

	<!-- ナビゲーション -->
	<div class="flex justify-between pt-6 border-t border-gray-200 dark:border-gray-700">
		<a href="/html/semantics" class="inline-flex items-center gap-2 px-4 py-2 rounded-lg border border-gray-300 dark:border-gray-600 hover:bg-gray-100 dark:hover:bg-gray-800 transition-colors">
			<svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
				<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 19l-7-7 7-7" />
			</svg>
			前へ：HTML
		</a>
		<a href="/css/box-model" class="inline-flex items-center gap-2 px-4 py-2 rounded-lg bg-primary-600 text-white hover:bg-primary-700 transition-colors">
			次へ：ボックスモデル
			<svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
				<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 5l7 7-7 7" />
			</svg>
		</a>
	</div>
</article>
