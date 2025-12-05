<script>
	import CodePreview from '$lib/components/CodePreview.svelte';
</script>

<svelte:head>
	<title>HTML 要素とタグ | さとまたラボ</title>
</svelte:head>

<article>
	<h1 class="text-3xl font-bold mb-2">要素とタグ</h1>
	<p class="text-lg text-gray-600 dark:text-gray-400 mb-8">
		HTMLの基本単位を理解しよう
	</p>

	<!-- 要素とタグの違い -->
	<section class="mb-10">
		<h2 id="difference" class="text-xl font-bold mb-4">「要素」と「タグ」の違い</h2>

		<div class="p-6 rounded-xl bg-blue-50 dark:bg-blue-900/20 border border-blue-200 dark:border-blue-800 mb-6">
			<p class="text-blue-800 dark:text-blue-200 mb-4">
				<strong>よくある混乱：</strong>「要素」と「タグ」は同じ意味？
			</p>
			<div class="grid grid-cols-1 md:grid-cols-2 gap-4 text-sm">
				<div class="p-3 bg-white dark:bg-gray-800 rounded-lg">
					<div class="font-semibold text-blue-700 dark:text-blue-300 mb-2">タグ（tag）</div>
					<p class="text-gray-600 dark:text-gray-400">
						<code class="bg-gray-100 dark:bg-gray-700 px-1 rounded">&lt;p&gt;</code> や
						<code class="bg-gray-100 dark:bg-gray-700 px-1 rounded">&lt;/p&gt;</code> のこと。<br>
						<strong>目印</strong>のようなもの。「ここから」「ここまで」を示す。
					</p>
				</div>
				<div class="p-3 bg-white dark:bg-gray-800 rounded-lg">
					<div class="font-semibold text-blue-700 dark:text-blue-300 mb-2">要素（element）</div>
					<p class="text-gray-600 dark:text-gray-400">
						開始タグ + 中身 + 終了タグ の<strong>全体</strong>。<br>
						<code class="bg-gray-100 dark:bg-gray-700 px-1 rounded">&lt;p&gt;こんにちは&lt;/p&gt;</code> 全部で1つの要素。
					</p>
				</div>
			</div>
		</div>

		<div class="p-4 rounded-lg bg-gray-100 dark:bg-gray-800 mb-6">
			<p class="text-center text-lg font-mono">
				<span class="text-blue-600 dark:text-blue-400">&lt;p&gt;</span>
				<span class="text-gray-800 dark:text-gray-200">こんにちは</span>
				<span class="text-red-600 dark:text-red-400">&lt;/p&gt;</span>
			</p>
			<div class="flex justify-center gap-8 mt-2 text-sm text-gray-600 dark:text-gray-400">
				<span class="text-blue-600 dark:text-blue-400">↑ 開始タグ</span>
				<span>↑ 内容</span>
				<span class="text-red-600 dark:text-red-400">↑ 終了タグ</span>
			</div>
			<p class="text-center mt-2 text-sm text-gray-600 dark:text-gray-400">
				← これ全体が「p要素」→
			</p>
		</div>
	</section>

	<!-- タグの基本構造 -->
	<section class="mb-10">
		<h2 id="structure" class="text-xl font-bold mb-4">タグの書き方</h2>

		<CodePreview
			title="基本のタグ"
			description="開始タグと終了タグで内容を挟む"
			language="html"
			code={`<!-- 基本の形：開始タグ → 内容 → 終了タグ -->
<p>これは段落です</p>

<!-- div: 「まとまり」を作る箱 -->
<div>これはdiv要素です</div>

<!-- span: 文章の一部を囲む -->
<span>これはspan要素です</span>`}
			previewHtml={`<div style="display:flex;flex-direction:column;gap:8px;">
<p style="margin:0;padding:8px;background:#f3f4f6;border-radius:4px;">これは段落です</p>
<div style="padding:8px;background:#e0f2fe;border-radius:4px;">これはdiv要素です</div>
<span style="padding:4px 8px;background:#fef3c7;border-radius:4px;">これはspan要素です</span>
</div>`}
		/>
	</section>

	<!-- 空要素 -->
	<section class="mb-10">
		<h2 id="empty" class="text-xl font-bold mb-4">終了タグがいらない要素</h2>

		<div class="p-4 rounded-lg bg-amber-50 dark:bg-amber-900/20 border border-amber-200 dark:border-amber-800 mb-6">
			<p class="font-semibold text-amber-800 dark:text-amber-200">なぜ終了タグがいらない？</p>
			<p class="text-sm text-amber-700 dark:text-amber-300 mt-2">
				「中身を挟む」必要がない要素は、終了タグが不要です。<br>
				例えば画像（img）は「画像を表示する」だけで、中にテキストを入れることはありません。
			</p>
		</div>

		<CodePreview
			title="空要素（からようそ）"
			description="開始タグだけで完結する"
			language="html"
			code={`<!-- img: 画像を表示（中に何も入れない） -->
<img src="image.jpg" alt="画像の説明">

<!-- br: 改行（強制的に次の行へ） -->
改行の<br>例です

<!-- hr: 水平線（区切り線） -->
<hr>

<!-- input: 入力欄（ユーザーが文字を入力） -->
<input type="text" placeholder="名前を入力">`}
			previewHtml={`<div style="display:flex;flex-direction:column;gap:12px;">
<div style="width:100px;height:60px;background:#e5e7eb;display:flex;align-items:center;justify-content:center;border-radius:4px;font-size:12px;color:#6b7280;">画像</div>
<p style="margin:0;">改行の<br>例です</p>
<hr style="border-top:1px solid #d1d5db;width:100%;margin:0;">
<input type="text" placeholder="名前を入力" style="padding:8px;border:1px solid #d1d5db;border-radius:4px;width:200px;">
</div>`}
		/>
	</section>

	<!-- ブロックとインライン -->
	<section class="mb-10">
		<h2 id="block-inline" class="text-xl font-bold mb-4">ブロック要素とインライン要素</h2>

		<div class="p-6 rounded-xl bg-blue-50 dark:bg-blue-900/20 border border-blue-200 dark:border-blue-800 mb-6">
			<p class="text-blue-800 dark:text-blue-200 mb-4">
				<strong>日常での例え：</strong>
			</p>
			<div class="grid grid-cols-1 md:grid-cols-2 gap-4 text-sm">
				<div class="p-3 bg-white dark:bg-gray-800 rounded-lg">
					<div class="font-semibold text-blue-700 dark:text-blue-300 mb-2">ブロック要素 = 段ボール箱</div>
					<p class="text-gray-600 dark:text-gray-400">
						1つ置くと、その下には別のものを置くしかない。<br>
						<strong>縦に積み重なる。</strong>
					</p>
				</div>
				<div class="p-3 bg-white dark:bg-gray-800 rounded-lg">
					<div class="font-semibold text-green-700 dark:text-green-300 mb-2">インライン要素 = 文字や単語</div>
					<p class="text-gray-600 dark:text-gray-400">
						文章の中で自然に並ぶ。<br>
						<strong>横に流れる。</strong>
					</p>
				</div>
			</div>
		</div>

		<div class="p-4 rounded-lg bg-amber-50 dark:bg-amber-900/20 border border-amber-200 dark:border-amber-800 mb-6">
			<p class="font-semibold text-amber-800 dark:text-amber-200">なぜこの区別が大事？</p>
			<p class="text-sm text-amber-700 dark:text-amber-300 mt-2">
				「横に並べたい」のに縦に並んでしまう、という問題を解決するため。<br>
				要素の種類を知っていれば、思い通りのレイアウトが作れます。
			</p>
		</div>

		<div class="grid grid-cols-1 md:grid-cols-2 gap-4 mb-6">
			<div class="p-4 rounded-lg bg-blue-50 dark:bg-blue-900/20 border border-blue-200 dark:border-blue-800">
				<h3 class="font-semibold text-blue-800 dark:text-blue-200 mb-2">ブロック要素の特徴</h3>
				<ul class="text-sm text-blue-700 dark:text-blue-300 space-y-1">
					<li>• 横幅いっぱいに広がる</li>
					<li>• 前後で改行される（縦に並ぶ）</li>
					<li>• 例: <code class="bg-blue-100 dark:bg-blue-800 px-1 rounded">div</code>, <code class="bg-blue-100 dark:bg-blue-800 px-1 rounded">p</code>, <code class="bg-blue-100 dark:bg-blue-800 px-1 rounded">h1</code>〜<code class="bg-blue-100 dark:bg-blue-800 px-1 rounded">h6</code>, <code class="bg-blue-100 dark:bg-blue-800 px-1 rounded">ul</code>, <code class="bg-blue-100 dark:bg-blue-800 px-1 rounded">li</code></li>
				</ul>
			</div>
			<div class="p-4 rounded-lg bg-green-50 dark:bg-green-900/20 border border-green-200 dark:border-green-800">
				<h3 class="font-semibold text-green-800 dark:text-green-200 mb-2">インライン要素の特徴</h3>
				<ul class="text-sm text-green-700 dark:text-green-300 space-y-1">
					<li>• 中身の分だけ幅を取る</li>
					<li>• 改行されない（横に並ぶ）</li>
					<li>• 例: <code class="bg-green-100 dark:bg-green-800 px-1 rounded">span</code>, <code class="bg-green-100 dark:bg-green-800 px-1 rounded">a</code>, <code class="bg-green-100 dark:bg-green-800 px-1 rounded">strong</code>, <code class="bg-green-100 dark:bg-green-800 px-1 rounded">em</code>, <code class="bg-green-100 dark:bg-green-800 px-1 rounded">img</code></li>
				</ul>
			</div>
		</div>

		<CodePreview
			title="ブロック要素の動き"
			description="それぞれが横幅いっぱいに広がり、縦に並ぶ"
			language="html"
			code={`<!-- divは横幅いっぱいに広がる -->
<!-- 次のdivはその下に配置される -->
<div style="background: lightblue; padding: 10px;">
  1つ目のdiv
</div>
<div style="background: lightgreen; padding: 10px;">
  2つ目のdiv（下に配置）
</div>`}
			previewHtml={`<div style="display:flex;flex-direction:column;gap:4px;">
<div style="background:lightblue;padding:10px;">1つ目のdiv</div>
<div style="background:lightgreen;padding:10px;">2つ目のdiv（下に配置）</div>
</div>`}
		/>

		<CodePreview
			title="インライン要素の動き"
			description="文章の中で自然に横に並ぶ"
			language="html"
			code={`<p>
  これは
  <span style="background: yellow;">黄色い部分</span>
  と
  <strong>太字の部分</strong>
  と
  <a href="#">リンク</a>
  の例です。すべて横に並びます。
</p>`}
			previewHtml={`<p style="margin:0;">これは<span style="background:yellow;">黄色い部分</span>と<strong>太字の部分</strong>と<a href="#" style="color:#3b82f6;">リンク</a>の例です。すべて横に並びます。</p>`}
		/>
	</section>

	<!-- 属性 -->
	<section class="mb-10">
		<h2 id="attributes" class="text-xl font-bold mb-4">属性（Attribute）</h2>

		<div class="p-6 rounded-xl bg-blue-50 dark:bg-blue-900/20 border border-blue-200 dark:border-blue-800 mb-6">
			<p class="text-blue-800 dark:text-blue-200 mb-3">
				<strong>属性とは？</strong>
			</p>
			<p class="text-sm text-blue-700 dark:text-blue-300">
				タグに<strong>追加情報</strong>を付けるもの。<br>
				例：リンクタグ <code class="bg-blue-100 dark:bg-blue-800 px-1 rounded">&lt;a&gt;</code> だけでは「どこにリンクするか」が分からない。<br>
				→ <code class="bg-blue-100 dark:bg-blue-800 px-1 rounded">href="URL"</code> という属性で「リンク先」を指定する。
			</p>
		</div>

		<CodePreview
			title="よく使う属性"
			description="それぞれの役割を理解しよう"
			language="html"
			code={`<!-- href: リンク先のURL -->
<a href="https://google.com">Googleへ</a>

<!-- src: 画像ファイルの場所 -->
<!-- alt: 画像が見えない時の説明文 -->
<img src="photo.jpg" alt="海の写真">

<!-- id: このページで1つだけの名前（識別用） -->
<div id="header">ヘッダー</div>

<!-- class: グループ名（同じスタイルを適用） -->
<p class="warning">警告メッセージ</p>
<p class="warning">別の警告</p>

<!-- style: 見た目を直接指定 -->
<span style="color: red;">赤い文字</span>`}
			previewHtml={`<div style="display:flex;flex-direction:column;gap:8px;">
<a href="#" style="color:#3b82f6;text-decoration:underline;">Googleへ</a>
<div style="width:100px;height:60px;background:#e5e7eb;display:flex;align-items:center;justify-content:center;border-radius:4px;font-size:11px;color:#6b7280;">海の写真</div>
<div style="font-weight:bold;padding:4px 8px;background:#f3f4f6;border-radius:4px;">#header</div>
<p style="margin:0;padding:4px 8px;background:#fef2f2;border-left:3px solid #ef4444;border-radius:2px;">.warning</p>
<span style="color:red;">赤い文字</span>
</div>`}
		/>

		<div class="p-4 rounded-lg bg-gray-100 dark:bg-gray-800 mb-6">
			<p class="text-sm text-gray-700 dark:text-gray-300">
				<strong>id と class の違い</strong><br>
				• <code class="bg-gray-200 dark:bg-gray-700 px-1 rounded">id</code>：ページ内で1つだけ。「このボタン」を特定したい時に使う<br>
				• <code class="bg-gray-200 dark:bg-gray-700 px-1 rounded">class</code>：何度でも使える。「警告メッセージすべて」に同じスタイルを適用したい時
			</p>
		</div>
	</section>

	<!-- テキスト関連の要素 -->
	<section class="mb-10">
		<h2 id="text-elements" class="text-xl font-bold mb-4">テキスト関連の要素</h2>

		<CodePreview
			title="見出し（h1〜h6）"
			description="数字が小さいほど重要な見出し"
			language="html"
			code={`<!-- h1: 一番重要。ページのタイトル（1ページに1つ） -->
<h1>サイトのメインタイトル</h1>

<!-- h2: 章のタイトル -->
<h2>第1章：はじめに</h2>

<!-- h3: 節のタイトル -->
<h3>1-1. 基本の説明</h3>

<!-- h4〜h6: さらに細かい見出し -->
<h4>補足情報</h4>`}
			previewHtml={`<div>
<h1 style="font-size:2em;margin:0.3em 0;">サイトのメインタイトル</h1>
<h2 style="font-size:1.5em;margin:0.3em 0;">第1章：はじめに</h2>
<h3 style="font-size:1.2em;margin:0.3em 0;">1-1. 基本の説明</h3>
<h4 style="font-size:1em;margin:0.3em 0;">補足情報</h4>
</div>`}
		/>

		<CodePreview
			title="テキストに意味を付ける"
			description="見た目だけでなく「意味」も伝える"
			language="html"
			code={`<!-- strong: 重要なテキスト（太字になる） -->
<p><strong>締め切りは明日です！</strong></p>

<!-- em: 強調（イタリックになる） -->
<p>これは<em>とても</em>重要です</p>

<!-- mark: ハイライト（蛍光ペン） -->
<p>テストに<mark>ここが出ます</mark></p>

<!-- del: 削除された内容（取り消し線） -->
<p>価格: <del>10,000円</del> → 8,000円</p>

<!-- code: プログラムコード -->
<p><code>console.log()</code>で出力できます</p>`}
			previewHtml={`<div style="display:flex;flex-direction:column;gap:8px;">
<p style="margin:0;"><strong>締め切りは明日です！</strong></p>
<p style="margin:0;">これは<em>とても</em>重要です</p>
<p style="margin:0;">テストに<mark>ここが出ます</mark></p>
<p style="margin:0;">価格: <del>10,000円</del> → 8,000円</p>
<p style="margin:0;"><code style="background:#f3f4f6;padding:2px 6px;border-radius:3px;font-family:monospace;">console.log()</code>で出力できます</p>
</div>`}
		/>
	</section>

	<!-- リスト要素 -->
	<section class="mb-10">
		<h2 id="list-elements" class="text-xl font-bold mb-4">リスト要素</h2>

		<div class="p-4 rounded-lg bg-gray-100 dark:bg-gray-800 mb-6">
			<p class="text-sm text-gray-700 dark:text-gray-300">
				<strong>ul と ol はいつ使い分ける？</strong><br>
				• <code class="bg-gray-200 dark:bg-gray-700 px-1 rounded">ul</code>（unordered list）：順番が関係ない → 買い物リスト、機能一覧<br>
				• <code class="bg-gray-200 dark:bg-gray-700 px-1 rounded">ol</code>（ordered list）：順番が大事 → 手順、ランキング
			</p>
		</div>

		<CodePreview
			title="順番なしリスト（ul）"
			description="・で始まる箇条書き"
			language="html"
			code={`<!-- ul: unordered list（順番なし） -->
<!-- li: list item（リストの項目） -->
<h3>好きな果物</h3>
<ul>
  <li>りんご</li>
  <li>バナナ</li>
  <li>オレンジ</li>
</ul>`}
			previewHtml={`<div>
<h3 style="font-size:1.1em;margin:0 0 8px 0;">好きな果物</h3>
<ul style="margin:0;padding-left:24px;"><li>りんご</li><li>バナナ</li><li>オレンジ</li></ul>
</div>`}
		/>

		<CodePreview
			title="順番ありリスト（ol）"
			description="1, 2, 3... と番号が付く"
			language="html"
			code={`<!-- ol: ordered list（順番あり） -->
<h3>カレーの作り方</h3>
<ol>
  <li>野菜を切る</li>
  <li>肉を炒める</li>
  <li>水を入れて煮る</li>
  <li>ルーを入れる</li>
</ol>`}
			previewHtml={`<div>
<h3 style="font-size:1.1em;margin:0 0 8px 0;">カレーの作り方</h3>
<ol style="margin:0;padding-left:24px;"><li>野菜を切る</li><li>肉を炒める</li><li>水を入れて煮る</li><li>ルーを入れる</li></ol>
</div>`}
		/>
	</section>

	<!-- まとめ -->
	<section class="mb-10">
		<h2 id="summary" class="text-xl font-bold mb-4">まとめ</h2>

		<div class="grid grid-cols-1 md:grid-cols-2 gap-4">
			<div class="p-4 rounded-lg bg-green-50 dark:bg-green-900/20 border border-green-200 dark:border-green-800">
				<h3 class="font-semibold text-green-800 dark:text-green-200 mb-2">覚えておくこと</h3>
				<ul class="text-sm text-green-700 dark:text-green-300 space-y-1">
					<li>• タグは目印、要素は全体</li>
					<li>• ブロック = 縦に並ぶ</li>
					<li>• インライン = 横に並ぶ</li>
					<li>• 属性で追加情報を付ける</li>
				</ul>
			</div>
			<div class="p-4 rounded-lg bg-blue-50 dark:bg-blue-900/20 border border-blue-200 dark:border-blue-800">
				<h3 class="font-semibold text-blue-800 dark:text-blue-200 mb-2">よく使うタグ</h3>
				<ul class="text-sm text-blue-700 dark:text-blue-300 space-y-1">
					<li>• div, p, h1〜h6（ブロック）</li>
					<li>• span, a, strong（インライン）</li>
					<li>• img, input, br（空要素）</li>
					<li>• ul/ol + li（リスト）</li>
				</ul>
			</div>
		</div>
	</section>

	<div class="flex justify-between pt-6 border-t border-gray-200 dark:border-gray-700">
		<a href="/html/basics" class="inline-flex items-center gap-2 px-4 py-2 rounded-lg border border-gray-300 dark:border-gray-600 hover:bg-gray-100 dark:hover:bg-gray-800 transition-colors">
			<svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
				<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 19l-7-7 7-7" />
			</svg>
			前へ：基本構造
		</a>
		<a href="/html/forms" class="inline-flex items-center gap-2 px-4 py-2 rounded-lg bg-primary-600 text-white hover:bg-primary-700 transition-colors">
			次へ：フォーム
			<svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
				<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 5l7 7-7 7" />
			</svg>
		</a>
	</div>
</article>
