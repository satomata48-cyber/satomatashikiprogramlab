<script>
	import CodePreview from '$lib/components/CodePreview.svelte';
</script>

<svelte:head>
	<title>HTML セマンティクス | さとまたラボ</title>
</svelte:head>

<article>
	<h1 class="text-3xl font-bold mb-2">セマンティクス</h1>
	<p class="text-lg text-gray-600 dark:text-gray-400 mb-8">
		HTMLタグに「意味」を持たせて、わかりやすいコードを書く
	</p>

	<!-- セマンティックとは -->
	<section class="mb-10">
		<h2 id="what-is" class="text-xl font-bold mb-4">セマンティック（Semantic）とは？</h2>

		<div class="p-6 rounded-xl bg-blue-50 dark:bg-blue-900/20 border border-blue-200 dark:border-blue-800 mb-6">
			<p class="text-blue-800 dark:text-blue-200 mb-4">
				<strong>Semantic = 「意味のある」「意味的な」</strong>
			</p>
			<div class="grid grid-cols-1 md:grid-cols-2 gap-4 text-sm">
				<div class="p-3 bg-white dark:bg-gray-800 rounded-lg">
					<div class="font-semibold text-red-600 dark:text-red-400 mb-2">❌ 意味がない書き方</div>
					<code class="text-xs">&lt;div class="header"&gt;</code>
					<p class="text-gray-600 dark:text-gray-400 mt-1">
						divは「ただの箱」。クラス名で意味を伝えているだけ。
					</p>
				</div>
				<div class="p-3 bg-white dark:bg-gray-800 rounded-lg">
					<div class="font-semibold text-green-600 dark:text-green-400 mb-2">✅ 意味がある書き方</div>
					<code class="text-xs">&lt;header&gt;</code>
					<p class="text-gray-600 dark:text-gray-400 mt-1">
						タグ自体が「これはヘッダー」と意味を伝えている。
					</p>
				</div>
			</div>
		</div>

		<div class="p-4 rounded-lg bg-amber-50 dark:bg-amber-900/20 border border-amber-200 dark:border-amber-800 mb-6">
			<p class="font-semibold text-amber-800 dark:text-amber-200">日常での例え</p>
			<p class="text-sm text-amber-700 dark:text-amber-300 mt-2">
				本を書く時「第1章」「まえがき」「あとがき」と名前を付けますよね？<br>
				HTMLでも同じように、「ここがヘッダー」「ここがメインコンテンツ」と
				<strong>名前を付けて構造を明確にする</strong>のがセマンティックHTMLです。
			</p>
		</div>
	</section>

	<!-- なぜ重要か -->
	<section class="mb-10">
		<h2 id="why" class="text-xl font-bold mb-4">なぜセマンティックHTMLが重要？</h2>

		<div class="grid grid-cols-1 md:grid-cols-3 gap-4 mb-6">
			<div class="p-4 rounded-lg bg-blue-50 dark:bg-blue-900/20 border border-blue-200 dark:border-blue-800">
				<div class="text-2xl mb-2">♿</div>
				<h3 class="font-semibold text-blue-800 dark:text-blue-200">アクセシビリティ</h3>
				<p class="text-sm text-blue-700 dark:text-blue-300 mt-2">
					<strong>スクリーンリーダー</strong>（視覚障害者用の読み上げソフト）が
					ページの構造を理解して、「ナビゲーションへ移動」などの操作ができる。
				</p>
			</div>
			<div class="p-4 rounded-lg bg-green-50 dark:bg-green-900/20 border border-green-200 dark:border-green-800">
				<div class="text-2xl mb-2">🔍</div>
				<h3 class="font-semibold text-green-800 dark:text-green-200">SEO</h3>
				<p class="text-sm text-green-700 dark:text-green-300 mt-2">
					<strong>SEO = Search Engine Optimization</strong>（検索エンジン最適化）<br>
					Googleが「ここがメインコンテンツ」と理解し、検索順位に良い影響を与える。
				</p>
			</div>
			<div class="p-4 rounded-lg bg-purple-50 dark:bg-purple-900/20 border border-purple-200 dark:border-purple-800">
				<div class="text-2xl mb-2">👨‍💻</div>
				<h3 class="font-semibold text-purple-800 dark:text-purple-200">保守性</h3>
				<p class="text-sm text-purple-700 dark:text-purple-300 mt-2">
					他の開発者（や未来の自分）がコードを見た時に
					「ここがヘッダー、ここがサイドバー」とすぐ分かる。
				</p>
			</div>
		</div>
	</section>

	<!-- ページ構造 -->
	<section class="mb-10">
		<h2 id="structure" class="text-xl font-bold mb-4">ページ構造のタグ</h2>

		<div class="p-4 rounded-lg bg-gray-100 dark:bg-gray-800 mb-6">
			<p class="text-sm text-gray-700 dark:text-gray-300">
				<strong>よくあるWebページの構造</strong><br>
				header（ヘッダー）→ main（メインコンテンツ）→ footer（フッター）<br>
				この構造をHTMLタグで表現します。
			</p>
		</div>

		<CodePreview
			title="セマンティックなページ構造"
			description="本の構成のように、パーツに名前を付ける"
			language="html"
			code={`<body>
  <!-- header: ページ上部（ロゴ、ナビなど） -->
  <header>
    <h1>サイトタイトル</h1>
    <!-- nav: ナビゲーションリンク -->
    <nav>
      <ul>
        <li><a href="/">ホーム</a></li>
        <li><a href="/about">概要</a></li>
      </ul>
    </nav>
  </header>

  <!-- main: ページの主要コンテンツ（1ページに1つ） -->
  <main>
    <!-- article: 独立した記事 -->
    <article>
      <h2>記事タイトル</h2>
      <p>記事の本文...</p>
    </article>

    <!-- aside: 補足情報（サイドバー） -->
    <aside>
      <h3>関連リンク</h3>
      <ul>...</ul>
    </aside>
  </main>

  <!-- footer: ページ下部（著作権、連絡先など） -->
  <footer>
    <p>© 2024 My Website</p>
  </footer>
</body>`}
			previewHtml={`<div style="border:2px solid #e5e7eb;border-radius:8px;overflow:hidden;font-size:12px;">
<div style="background:#3b82f6;color:white;padding:12px;">
<strong>header</strong>
<div style="font-size:10px;margin-top:4px;opacity:0.8;">ロゴ・ナビゲーション</div>
</div>
<div style="display:flex;">
<div style="flex:1;background:#f3f4f6;padding:12px;border-right:1px solid #e5e7eb;">
<strong>main</strong>
<div style="background:white;padding:8px;margin:8px 0;border-radius:4px;border:1px solid #e5e7eb;">
<strong style="color:#6366f1;">article</strong>
<div style="font-size:10px;color:#6b7280;">記事コンテンツ</div>
</div>
</div>
<div style="width:100px;background:#fef3c7;padding:12px;">
<strong>aside</strong>
<div style="font-size:10px;margin-top:4px;color:#92400e;">サイドバー</div>
</div>
</div>
<div style="background:#374151;color:white;padding:12px;">
<strong>footer</strong>
<div style="font-size:10px;margin-top:4px;opacity:0.8;">著作権・連絡先</div>
</div>
</div>`}
		/>
	</section>

	<!-- 主要なタグ -->
	<section class="mb-10">
		<h2 id="tags" class="text-xl font-bold mb-4">よく使うセマンティックタグ</h2>

		<div class="overflow-x-auto mb-6">
			<table class="w-full text-sm">
				<thead>
					<tr class="border-b border-gray-200 dark:border-gray-700">
						<th class="text-left py-2 px-4">タグ</th>
						<th class="text-left py-2 px-4">意味</th>
						<th class="text-left py-2 px-4">使いどころ</th>
					</tr>
				</thead>
				<tbody>
					<tr class="border-b border-gray-200 dark:border-gray-700">
						<td class="py-2 px-4 font-mono text-blue-600">&lt;header&gt;</td>
						<td class="py-2 px-4">ヘッダー</td>
						<td class="py-2 px-4 text-gray-600 dark:text-gray-400">ページ上部、ロゴやナビ</td>
					</tr>
					<tr class="border-b border-gray-200 dark:border-gray-700">
						<td class="py-2 px-4 font-mono text-blue-600">&lt;nav&gt;</td>
						<td class="py-2 px-4">ナビゲーション</td>
						<td class="py-2 px-4 text-gray-600 dark:text-gray-400">メニューリンク</td>
					</tr>
					<tr class="border-b border-gray-200 dark:border-gray-700">
						<td class="py-2 px-4 font-mono text-blue-600">&lt;main&gt;</td>
						<td class="py-2 px-4">メインコンテンツ</td>
						<td class="py-2 px-4 text-gray-600 dark:text-gray-400">ページの主要部分（1つだけ）</td>
					</tr>
					<tr class="border-b border-gray-200 dark:border-gray-700">
						<td class="py-2 px-4 font-mono text-blue-600">&lt;article&gt;</td>
						<td class="py-2 px-4">独立した記事</td>
						<td class="py-2 px-4 text-gray-600 dark:text-gray-400">ブログ記事、ニュース</td>
					</tr>
					<tr class="border-b border-gray-200 dark:border-gray-700">
						<td class="py-2 px-4 font-mono text-blue-600">&lt;section&gt;</td>
						<td class="py-2 px-4">セクション</td>
						<td class="py-2 px-4 text-gray-600 dark:text-gray-400">テーマごとのまとまり</td>
					</tr>
					<tr class="border-b border-gray-200 dark:border-gray-700">
						<td class="py-2 px-4 font-mono text-blue-600">&lt;aside&gt;</td>
						<td class="py-2 px-4">補足情報</td>
						<td class="py-2 px-4 text-gray-600 dark:text-gray-400">サイドバー、関連リンク</td>
					</tr>
					<tr class="border-b border-gray-200 dark:border-gray-700">
						<td class="py-2 px-4 font-mono text-blue-600">&lt;footer&gt;</td>
						<td class="py-2 px-4">フッター</td>
						<td class="py-2 px-4 text-gray-600 dark:text-gray-400">ページ下部、著作権</td>
					</tr>
				</tbody>
			</table>
		</div>

		<CodePreview
			title="article と section の違い"
			description="独立性があるかどうか"
			language="html"
			code={`<!-- article: それ単体で意味が通じる（独立している） -->
<!-- 例: ブログ記事、商品カード、コメント -->
<article>
  <h2>新商品のお知らせ</h2>
  <p>この記事だけ切り取っても意味が通じる</p>
</article>

<!-- section: ページ内のテーマ分け（依存している） -->
<!-- 例: 「サービス紹介」「料金」「FAQ」の各セクション -->
<section>
  <h2>サービス紹介</h2>
  <p>このページの一部として存在する</p>
</section>
<section>
  <h2>料金プラン</h2>
  <p>...</p>
</section>`}
			previewHtml={`<div style="display:flex;flex-direction:column;gap:12px;">
<article style="background:white;padding:12px;border:2px solid #6366f1;border-radius:4px;">
<div style="font-size:10px;color:#6366f1;margin-bottom:4px;">article（独立）</div>
<h2 style="font-size:14px;font-weight:bold;">新商品のお知らせ</h2>
</article>
<div style="display:flex;gap:8px;">
<section style="flex:1;background:#f3f4f6;padding:12px;border-radius:4px;">
<div style="font-size:10px;color:#6b7280;margin-bottom:4px;">section</div>
<h2 style="font-size:12px;font-weight:bold;">サービス</h2>
</section>
<section style="flex:1;background:#f3f4f6;padding:12px;border-radius:4px;">
<div style="font-size:10px;color:#6b7280;margin-bottom:4px;">section</div>
<h2 style="font-size:12px;font-weight:bold;">料金</h2>
</section>
</div>
</div>`}
		/>
	</section>

	<!-- 比較 -->
	<section class="mb-10">
		<h2 id="comparison" class="text-xl font-bold mb-4">divだらけ vs セマンティック</h2>

		<div class="p-4 rounded-lg bg-amber-50 dark:bg-amber-900/20 border border-amber-200 dark:border-amber-800 mb-6">
			<p class="font-semibold text-amber-800 dark:text-amber-200">よくある問題</p>
			<p class="text-sm text-amber-700 dark:text-amber-300 mt-2">
				「div地獄」と呼ばれる状態。すべてdivで書かれていて、
				どこが何なのか分からない...
			</p>
		</div>

		<div class="grid grid-cols-1 md:grid-cols-2 gap-4">
			<div class="p-4 rounded-lg bg-red-50 dark:bg-red-900/20 border border-red-200 dark:border-red-800">
				<h3 class="font-semibold text-red-800 dark:text-red-200 mb-2">❌ divだらけ</h3>
				<pre class="text-xs text-red-700 dark:text-red-300 overflow-x-auto bg-white dark:bg-gray-800 p-2 rounded"><code>{`<div class="header">
  <div class="nav">...</div>
</div>
<div class="main">
  <div class="article">...</div>
  <div class="sidebar">...</div>
</div>
<div class="footer">...</div>`}</code></pre>
				<p class="text-xs text-red-600 dark:text-red-400 mt-2">
					クラス名を見ないと構造が分からない
				</p>
			</div>
			<div class="p-4 rounded-lg bg-green-50 dark:bg-green-900/20 border border-green-200 dark:border-green-800">
				<h3 class="font-semibold text-green-800 dark:text-green-200 mb-2">✅ セマンティック</h3>
				<pre class="text-xs text-green-700 dark:text-green-300 overflow-x-auto bg-white dark:bg-gray-800 p-2 rounded"><code>{`<header>
  <nav>...</nav>
</header>
<main>
  <article>...</article>
  <aside>...</aside>
</main>
<footer>...</footer>`}</code></pre>
				<p class="text-xs text-green-600 dark:text-green-400 mt-2">
					タグ名だけで構造が分かる！
				</p>
			</div>
		</div>
	</section>

	<!-- まとめ -->
	<section class="mb-10">
		<h2 id="summary" class="text-xl font-bold mb-4">まとめ</h2>

		<div class="grid grid-cols-1 md:grid-cols-2 gap-4">
			<div class="p-4 rounded-lg bg-green-50 dark:bg-green-900/20 border border-green-200 dark:border-green-800">
				<h3 class="font-semibold text-green-800 dark:text-green-200 mb-2">覚えておくこと</h3>
				<ul class="text-sm text-green-700 dark:text-green-300 space-y-1">
					<li>• セマンティック = 意味のある</li>
					<li>• divの代わりに意味のあるタグを使う</li>
					<li>• アクセシビリティとSEOに良い</li>
					<li>• コードが読みやすくなる</li>
				</ul>
			</div>
			<div class="p-4 rounded-lg bg-blue-50 dark:bg-blue-900/20 border border-blue-200 dark:border-blue-800">
				<h3 class="font-semibold text-blue-800 dark:text-blue-200 mb-2">基本の構造</h3>
				<ul class="text-sm text-blue-700 dark:text-blue-300 space-y-1">
					<li>• header → nav</li>
					<li>• main → article / section</li>
					<li>• aside（サイドバー）</li>
					<li>• footer</li>
				</ul>
			</div>
		</div>
	</section>

	<div class="flex justify-between pt-6 border-t border-gray-200 dark:border-gray-700">
		<a href="/html/forms" class="inline-flex items-center gap-2 px-4 py-2 rounded-lg border border-gray-300 dark:border-gray-600 hover:bg-gray-100 dark:hover:bg-gray-800 transition-colors">
			<svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
				<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 19l-7-7 7-7" />
			</svg>
			前へ：フォーム
		</a>
		<a href="/css/selectors" class="inline-flex items-center gap-2 px-4 py-2 rounded-lg bg-primary-600 text-white hover:bg-primary-700 transition-colors">
			次へ：CSS
			<svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
				<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 5l7 7-7 7" />
			</svg>
		</a>
	</div>
</article>
