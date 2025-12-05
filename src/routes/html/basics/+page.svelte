<script>
	import CodePreview from '$lib/components/CodePreview.svelte';
	import CodeExplain from '$lib/components/CodeExplain.svelte';
	import FeatureCard from '$lib/components/FeatureCard.svelte';

	const features = [
		{ icon: '📄', title: '文書構造の定義', description: '見出し、段落、リストなどで文書の構造を表現', tag: '基本' },
		{ icon: '🔗', title: 'ハイパーリンク', description: '他のページやサイトへのリンクを作成', tag: '基本' },
		{ icon: '🖼️', title: '画像・メディア', description: '画像、動画、音声を埋め込み', tag: '基本' },
		{ icon: '📝', title: 'フォーム', description: 'ユーザー入力を受け取るフォームを作成', tag: '重要' },
		{ icon: '📊', title: 'テーブル', description: '表形式でデータを表示', tag: '基本' },
		{ icon: '🎯', title: 'セマンティクス', description: '意味のあるタグで検索エンジンにも優しく', tag: '重要' }
	];
</script>

<svelte:head>
	<title>HTML基本構造 | さとまたラボ</title>
</svelte:head>

<article>
	<h1 class="text-3xl font-bold mb-2">HTML</h1>
	<p class="text-lg text-gray-600 dark:text-gray-400 mb-8">
		Webページの構造を作るマークアップ言語
	</p>

	<!-- できること一覧 -->
	<section class="mb-10">
		<h2 id="features" class="text-xl font-bold mb-4">HTMLでできること</h2>
		<div class="grid grid-cols-1 md:grid-cols-2 gap-3">
			{#each features as feature}
				<FeatureCard {...feature} />
			{/each}
		</div>
	</section>

	<!-- HTMLとは -->
	<section class="mb-10">
		<h2 id="what-is" class="text-xl font-bold mb-4">HTMLとは何か？</h2>

		<div class="prose dark:prose-invert max-w-none mb-6">
			<p>
				<strong>HTML（HyperText Markup Language）</strong>は、Webページの「骨組み」を作る言語です。
				ブラウザは HTMLファイルを読み込んで、その指示通りに画面を表示します。
			</p>
		</div>

		<div class="grid grid-cols-1 md:grid-cols-3 gap-4 mb-6">
			<div class="p-4 rounded-lg bg-blue-50 dark:bg-blue-900/20 border border-blue-200 dark:border-blue-800">
				<div class="text-2xl mb-2">📝</div>
				<h3 class="font-semibold text-blue-800 dark:text-blue-200">マークアップ言語</h3>
				<p class="text-sm text-blue-700 dark:text-blue-300">
					テキストに「これは見出し」「これは段落」と<strong>意味を付ける</strong>ための言語
				</p>
			</div>
			<div class="p-4 rounded-lg bg-green-50 dark:bg-green-900/20 border border-green-200 dark:border-green-800">
				<div class="text-2xl mb-2">🏗️</div>
				<h3 class="font-semibold text-green-800 dark:text-green-200">構造を定義</h3>
				<p class="text-sm text-green-700 dark:text-green-300">
					「ここがヘッダー」「ここが本文」という<strong>ページの骨組み</strong>を作る
				</p>
			</div>
			<div class="p-4 rounded-lg bg-purple-50 dark:bg-purple-900/20 border border-purple-200 dark:border-purple-800">
				<div class="text-2xl mb-2">🎨</div>
				<h3 class="font-semibold text-purple-800 dark:text-purple-200">見た目は別</h3>
				<p class="text-sm text-purple-700 dark:text-purple-300">
					色やサイズは CSS で指定。HTMLは<strong>内容と構造だけ</strong>を担当
				</p>
			</div>
		</div>
	</section>

	<!-- 基本構造の詳細解説 -->
	<section class="mb-10">
		<h2 id="structure" class="text-xl font-bold mb-4">HTMLファイルの基本構造</h2>

		<CodeExplain
			title="すべてのHTMLファイルの土台"
			language="html"
			code={`<!DOCTYPE html>
<html lang="ja">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>ページタイトル</title>
</head>
<body>
    <h1>こんにちは！</h1>
    <p>これが本文です。</p>
</body>
</html>`}
			explanations={[
				{ line: 1, code: '<!DOCTYPE html>', text: 'この文書がHTML5であることをブラウザに宣言。これがないと古いモードで表示される可能性がある' },
				{ line: 2, code: '<html lang="ja">', text: 'HTML文書の開始。lang="ja"で日本語ページと明示（検索エンジンや音声読み上げに役立つ）' },
				{ line: 3, code: '<head>', text: 'ページの「メタ情報」を入れる場所。画面には表示されないが、ブラウザや検索エンジンが使う' },
				{ line: 4, code: 'charset="UTF-8"', text: '文字コードを指定。UTF-8なら日本語が文字化けしない' },
				{ line: 5, code: 'viewport', text: 'スマホ対応の設定。これがないとスマホで極小表示になることがある' },
				{ line: 6, code: '<title>', text: 'ブラウザのタブに表示されるタイトル。検索結果にも表示される重要な要素' },
				{ line: 8, code: '<body>', text: '実際に画面に表示される内容を入れる場所。見える部分はすべてここに書く' },
			]}
		/>

		<div class="p-4 rounded-lg bg-amber-50 dark:bg-amber-900/20 border border-amber-200 dark:border-amber-800 mt-4">
			<p class="font-semibold text-amber-800 dark:text-amber-200 flex items-center gap-2">
				<span>💡</span> なぜこの構造が必要？
			</p>
			<p class="text-sm text-amber-700 dark:text-amber-300 mt-2">
				ブラウザはこの構造を読み取って「どこが設定でどこが本文か」を判断します。
				構造が崩れると、文字化けしたり、スマホで正しく表示されなかったりします。
			</p>
		</div>
	</section>

	<!-- タグの仕組み -->
	<section class="mb-10">
		<h2 id="tags" class="text-xl font-bold mb-4">タグの仕組み</h2>

		<div class="p-6 rounded-xl bg-gray-100 dark:bg-gray-800 mb-6">
			<div class="text-center mb-4">
				<code class="text-lg bg-white dark:bg-gray-900 px-4 py-2 rounded-lg">
					<span class="text-blue-600 dark:text-blue-400">&lt;タグ名&gt;</span>
					<span class="text-gray-800 dark:text-gray-200">内容</span>
					<span class="text-red-600 dark:text-red-400">&lt;/タグ名&gt;</span>
				</code>
			</div>
			<div class="grid grid-cols-3 gap-4 text-center text-sm">
				<div>
					<div class="text-blue-600 dark:text-blue-400 font-semibold">開始タグ</div>
					<div class="text-gray-600 dark:text-gray-400">「ここから始まり」</div>
				</div>
				<div>
					<div class="text-gray-800 dark:text-gray-200 font-semibold">内容</div>
					<div class="text-gray-600 dark:text-gray-400">表示されるテキスト</div>
				</div>
				<div>
					<div class="text-red-600 dark:text-red-400 font-semibold">終了タグ</div>
					<div class="text-gray-600 dark:text-gray-400">「ここで終わり」</div>
				</div>
			</div>
		</div>

		<CodePreview
			title="よく使うタグ"
			description="見出し・段落・リンク・画像"
			language="html"
			code={`<!-- h1: 最も重要な見出し（ページに1つだけ） -->
<h1>大見出し</h1>

<!-- h2: 章のタイトルなど（h6まである） -->
<h2>中見出し</h2>

<!-- p: paragraph（段落）本文を囲む -->
<p>段落のテキストです。</p>

<!-- a: anchor（錨）href属性でリンク先を指定 -->
<a href="https://google.com">リンク</a>

<!-- img: 画像。終了タグ不要 -->
<!-- src=画像パス, alt=代替テキスト -->
<img src="photo.jpg" alt="写真">`}
			previewHtml={`<h1 style="font-size:2em;font-weight:bold;margin:0.5em 0;">大見出し</h1>
<h2 style="font-size:1.5em;font-weight:bold;margin:0.5em 0;">中見出し</h2>
<p style="margin:0.5em 0;">段落のテキストです。</p>
<a href="https://google.com" style="color:#0ea5e9;text-decoration:underline;">リンク</a>
<div style="margin-top:0.5em;padding:8px;background:#f3f4f6;border-radius:4px;font-size:12px;color:#6b7280;">📷 photo.jpg (写真)</div>`}
		/>
	</section>

	<!-- コード例とプレビュー -->
	<section class="mb-10">
		<h2 id="examples" class="text-xl font-bold mb-4">実例とプレビュー</h2>

		<CodePreview
			title="見出しと段落"
			description="文書の階層構造を作る"
			language="html"
			code={`<!-- 見出しはh1〜h6まで。数字が小さいほど重要 -->
<h1>大見出し</h1>
<h2>中見出し</h2>

<!-- pタグで段落を作る -->
<p>これは段落です。文章を書きます。</p>
<p>複数の段落を作れます。</p>`}
			previewHtml={`<h1 style="font-size:2em;font-weight:bold;margin:0.3em 0;">大見出し</h1>
<h2 style="font-size:1.5em;font-weight:bold;margin:0.3em 0;">中見出し</h2>
<p style="margin:0.5em 0;">これは段落です。文章を書きます。</p>
<p style="margin:0.5em 0;">複数の段落を作れます。</p>`}
		/>

		<div class="p-4 rounded-lg bg-gray-100 dark:bg-gray-800 mb-6">
			<p class="text-sm text-gray-700 dark:text-gray-300">
				<strong>なぜ見出しタグを使う？</strong><br>
				・検索エンジンがページの構造を理解できる<br>
				・視覚障害者用の読み上げソフトがナビゲーションしやすくなる<br>
				・CSSでスタイルを一括適用しやすい
			</p>
		</div>

		<CodePreview
			title="リスト"
			description="箇条書きと番号付きリスト"
			language="html"
			code={`<h3>買い物リスト（順不同）</h3>
<!-- ul: unordered list（順番なしリスト） -->
<ul>
  <!-- li: list item（リストの項目） -->
  <li>りんご</li>
  <li>バナナ</li>
</ul>

<h3>手順（順番あり）</h3>
<!-- ol: ordered list（番号付きリスト） -->
<ol>
  <li>材料を用意</li>
  <li>混ぜる</li>
  <li>焼く</li>
</ol>`}
			previewHtml={`<h3 style="font-size:1.2em;font-weight:bold;margin:0.5em 0;">買い物リスト（順不同）</h3>
<ul style="list-style:disc;margin-left:1.5em;"><li>りんご</li><li>バナナ</li></ul>
<h3 style="font-size:1.2em;font-weight:bold;margin:0.5em 0;">手順（順番あり）</h3>
<ol style="list-style:decimal;margin-left:1.5em;"><li>材料を用意</li><li>混ぜる</li><li>焼く</li></ol>`}
		/>

		<div class="p-4 rounded-lg bg-gray-100 dark:bg-gray-800 mb-6">
			<p class="text-sm text-gray-700 dark:text-gray-300">
				<strong>ulとolの違い</strong><br>
				・<code class="bg-gray-200 dark:bg-gray-700 px-1 rounded">ul</code>（unordered list）：順番が関係ない一覧。買い物リストなど<br>
				・<code class="bg-gray-200 dark:bg-gray-700 px-1 rounded">ol</code>（ordered list）：順番が重要な一覧。手順や順位など
			</p>
		</div>

		<CodePreview
			title="リンク"
			description="他のページへ移動"
			language="html"
			code={`<!-- 外部サイトへのリンク -->
<a href="https://google.com">Googleへ移動</a>

<!-- 同じサイト内のリンク -->
<a href="/about">このサイトについて</a>

<!-- 新しいタブで開く -->
<a href="https://google.com" target="_blank">
  新しいタブで開く
</a>`}
			previewHtml={`<div style="display:flex;flex-direction:column;gap:8px;"><a href="https://google.com" style="color:#0ea5e9;text-decoration:underline;">Googleへ移動</a><a href="/about" style="color:#0ea5e9;text-decoration:underline;">このサイトについて</a></div>`}
		/>

		<div class="p-4 rounded-lg bg-gray-100 dark:bg-gray-800 mb-6">
			<p class="text-sm text-gray-700 dark:text-gray-300">
				<strong>target="_blank"を使う時の注意</strong><br>
				セキュリティのため <code class="bg-gray-200 dark:bg-gray-700 px-1 rounded">rel="noopener noreferrer"</code> も一緒につけるのが推奨
			</p>
		</div>

		<CodePreview
			title="テーブル（表）"
			description="データを表形式で表示"
			language="html"
			code={`<!-- table: 表全体を囲む -->
<table border="1">
  <!-- thead: 表のヘッダー部分 -->
  <thead>
    <!-- tr: table row（行） -->
    <tr>
      <!-- th: table header（見出しセル） -->
      <th>名前</th>
      <th>年齢</th>
    </tr>
  </thead>
  <!-- tbody: 表の本体（データ部分） -->
  <tbody>
    <tr>
      <!-- td: table data（データセル） -->
      <td>田中</td>
      <td>25</td>
    </tr>
    <tr>
      <td>佐藤</td>
      <td>30</td>
    </tr>
  </tbody>
</table>`}
			previewHtml={`<table style="border-collapse:collapse;width:100%;">
<thead><tr><th style="border:1px solid #ccc;padding:8px;background:#f3f4f6;text-align:left;">名前</th><th style="border:1px solid #ccc;padding:8px;background:#f3f4f6;text-align:left;">年齢</th></tr></thead>
<tbody><tr><td style="border:1px solid #ccc;padding:8px;">田中</td><td style="border:1px solid #ccc;padding:8px;">25</td></tr><tr><td style="border:1px solid #ccc;padding:8px;">佐藤</td><td style="border:1px solid #ccc;padding:8px;">30</td></tr></tbody>
</table>`}
		/>

		<div class="p-4 rounded-lg bg-gray-100 dark:bg-gray-800 mb-6">
			<p class="text-sm text-gray-700 dark:text-gray-300">
				<strong>テーブルの構造</strong><br>
				・<code class="bg-gray-200 dark:bg-gray-700 px-1 rounded">thead</code>：表のヘッダー行（列の見出し）<br>
				・<code class="bg-gray-200 dark:bg-gray-700 px-1 rounded">tbody</code>：表の本体（データ行）<br>
				・<code class="bg-gray-200 dark:bg-gray-700 px-1 rounded">tr</code>：table row（行）<br>
				・<code class="bg-gray-200 dark:bg-gray-700 px-1 rounded">th</code>：table header（見出しセル）<br>
				・<code class="bg-gray-200 dark:bg-gray-700 px-1 rounded">td</code>：table data（データセル）
			</p>
		</div>
	</section>

	<!-- 属性について -->
	<section class="mb-10">
		<h2 id="attributes" class="text-xl font-bold mb-4">属性（Attribute）とは</h2>

		<div class="p-6 rounded-xl bg-gray-100 dark:bg-gray-800 mb-6">
			<div class="text-center mb-4">
				<code class="text-lg bg-white dark:bg-gray-900 px-4 py-2 rounded-lg">
					&lt;タグ名 <span class="text-green-600 dark:text-green-400">属性名="値"</span>&gt;内容&lt;/タグ名&gt;
				</code>
			</div>
			<p class="text-center text-sm text-gray-600 dark:text-gray-400">
				属性はタグに<strong>追加情報</strong>を与える。リンク先URL、画像パス、IDなどを指定する
			</p>
		</div>

		<CodeExplain
			title="よく使う属性"
			language="html"
			code={`<a href="https://example.com">リンク</a>
<img src="photo.jpg" alt="説明">
<div id="header">ヘッダー</div>
<p class="highlight">ハイライト</p>
<input type="text" placeholder="入力">`}
			explanations={[
				{ line: 1, code: 'href', text: 'hyperlink referenceの略。リンク先のURLを指定' },
				{ line: 2, code: 'src', text: 'sourceの略。画像や動画のファイルパスを指定' },
				{ line: 2, code: 'alt', text: 'alternativeの略。画像が表示できない時の代替テキスト' },
				{ line: 3, code: 'id', text: 'ページ内で一意の識別子。CSSやJSで特定の要素を指定する時に使う' },
				{ line: 4, code: 'class', text: '複数の要素に同じスタイルを適用したい時に使う。複数のclassを付けられる' },
				{ line: 5, code: 'type', text: 'input要素の種類を指定。text, email, password, checkboxなど多数' },
			]}
		/>
	</section>

	<!-- まとめ -->
	<section class="mb-10">
		<h2 id="summary" class="text-xl font-bold mb-4">まとめ</h2>

		<div class="grid grid-cols-1 md:grid-cols-2 gap-4">
			<div class="p-4 rounded-lg bg-green-50 dark:bg-green-900/20 border border-green-200 dark:border-green-800">
				<h3 class="font-semibold text-green-800 dark:text-green-200 mb-2">覚えておくこと</h3>
				<ul class="text-sm text-green-700 dark:text-green-300 space-y-1">
					<li>• HTMLは「構造」を作る言語</li>
					<li>• タグで内容を囲んで意味を付ける</li>
					<li>• head は設定、body は表示内容</li>
					<li>• 属性で追加情報を指定</li>
				</ul>
			</div>
			<div class="p-4 rounded-lg bg-blue-50 dark:bg-blue-900/20 border border-blue-200 dark:border-blue-800">
				<h3 class="font-semibold text-blue-800 dark:text-blue-200 mb-2">次のステップ</h3>
				<ul class="text-sm text-blue-700 dark:text-blue-300 space-y-1">
					<li>• 要素とタグの種類を覚える</li>
					<li>• フォームの作り方を学ぶ</li>
					<li>• CSSでスタイルを付ける</li>
				</ul>
			</div>
		</div>
	</section>

	<!-- ナビゲーション -->
	<div class="flex justify-between pt-6 border-t border-gray-200 dark:border-gray-700">
		<div></div>
		<a href="/html/elements" class="inline-flex items-center gap-2 px-4 py-2 rounded-lg bg-primary-600 text-white hover:bg-primary-700 transition-colors">
			次へ：要素とタグ
			<svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
				<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 5l7 7-7 7" />
			</svg>
		</a>
	</div>
</article>
