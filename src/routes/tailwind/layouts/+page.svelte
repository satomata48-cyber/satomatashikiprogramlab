<script>
	import CodePreview from '$lib/components/CodePreview.svelte';
</script>

<svelte:head>
	<title>Tailwind モダンレイアウト | さとまたラボ</title>
</svelte:head>

<article>
	<h1 class="text-3xl font-bold mb-2">モダンレイアウト</h1>
	<p class="text-lg text-gray-600 dark:text-gray-400 mb-8">
		ヘッダー、サイドバー、フッターなど現代的なサイト構成
	</p>

	<!-- モダンなサイト構成 -->
	<section class="mb-10">
		<h2 id="overview" class="text-xl font-bold mb-4">モダンなWebサイトの構成</h2>

		<div class="p-6 rounded-xl bg-blue-50 dark:bg-blue-900/20 border border-blue-200 dark:border-blue-800 mb-6">
			<p class="text-blue-800 dark:text-blue-200 mb-4">
				<strong>基本的なレイアウトパターン</strong>
			</p>
			<div class="grid grid-cols-1 md:grid-cols-3 gap-4 text-sm">
				<div class="p-3 bg-white dark:bg-gray-800 rounded-lg">
					<div class="font-semibold text-blue-700 dark:text-blue-300 mb-2">ヘッダー + コンテンツ</div>
					<p class="text-gray-600 dark:text-gray-400">
						ブログ、ニュースサイト<br>
						シンプルなWebサイト
					</p>
				</div>
				<div class="p-3 bg-white dark:bg-gray-800 rounded-lg">
					<div class="font-semibold text-blue-700 dark:text-blue-300 mb-2">サイドバー付き</div>
					<p class="text-gray-600 dark:text-gray-400">
						管理画面、ドキュメント<br>
						このサイトのような構成
					</p>
				</div>
				<div class="p-3 bg-white dark:bg-gray-800 rounded-lg">
					<div class="font-semibold text-blue-700 dark:text-blue-300 mb-2">フルスクリーン</div>
					<p class="text-gray-600 dark:text-gray-400">
						ランディングページ<br>
						アプリケーション
					</p>
				</div>
			</div>
		</div>
	</section>

	<!-- 基本レイアウト -->
	<section class="mb-10">
		<h2 id="basic" class="text-xl font-bold mb-4">基本レイアウト（ヘッダー・フッター）</h2>

		<CodePreview
			title="Sticky Header + Footer"
			description="上固定ヘッダーとフッター"
			language="html"
			code={`<div class="min-h-screen flex flex-col">
  <!-- ヘッダー（上に固定） -->
  <header class="sticky top-0 z-50 bg-white border-b shadow-sm">
    <div class="max-w-7xl mx-auto px-4 py-3 flex items-center justify-between">
      <a href="/" class="text-xl font-bold">Logo</a>
      <nav class="flex gap-6">
        <a href="/" class="hover:text-blue-600">ホーム</a>
        <a href="/about" class="hover:text-blue-600">About</a>
        <a href="/contact" class="hover:text-blue-600">お問い合わせ</a>
      </nav>
    </div>
  </header>

  <!-- メインコンテンツ（残りのスペースを埋める） -->
  <main class="flex-1 max-w-7xl mx-auto px-4 py-8 w-full">
    <h1>コンテンツ</h1>
  </main>

  <!-- フッター（常に下に） -->
  <footer class="bg-gray-100 border-t">
    <div class="max-w-7xl mx-auto px-4 py-6">
      <p class="text-center text-gray-600">© 2024 My Website</p>
    </div>
  </footer>
</div>`}
			previewHtml={`<div style="border:1px solid #e5e7eb;border-radius:8px;overflow:hidden;"><div style="background:white;padding:8px 12px;border-bottom:1px solid #e5e7eb;display:flex;justify-content:space-between;align-items:center;"><span style="font-weight:bold;">Logo</span><div style="display:flex;gap:12px;font-size:12px;"><span style="color:#3b82f6;">ホーム</span><span style="color:#6b7280;">About</span><span style="color:#6b7280;">お問い合わせ</span></div></div><div style="padding:20px;min-height:80px;color:#6b7280;text-align:center;">コンテンツエリア</div><div style="background:#f3f4f6;padding:8px;text-align:center;font-size:12px;color:#6b7280;">© 2024 My Website</div></div>`}
		/>

		<div class="mt-4 p-4 rounded-lg bg-gray-50 dark:bg-gray-800/50 border border-gray-200 dark:border-gray-700">
			<p class="font-semibold text-gray-800 dark:text-gray-200 mb-3">コード解説：ヘッダー・フッターレイアウト</p>
			<div class="text-sm text-gray-700 dark:text-gray-300 space-y-4">
				<div>
					<p class="font-medium text-blue-600 dark:text-blue-400 mb-2">① 全体の構造</p>
					<div class="bg-gray-100 dark:bg-gray-800 p-2 rounded text-xs font-mono mb-2">
						&lt;div class="<span class="text-cyan-600">min-h-screen</span> <span class="text-green-600">flex flex-col</span>"&gt;
					</div>
					<ul class="list-disc list-inside space-y-1 ml-2">
						<li><code class="text-cyan-600">min-h-screen</code>：画面全体の高さを確保（100vh）</li>
						<li><code class="text-green-600">flex flex-col</code>：中身を縦に並べる（ヘッダー→本文→フッター）</li>
					</ul>
				</div>
				<div>
					<p class="font-medium text-blue-600 dark:text-blue-400 mb-2">② 固定ヘッダー</p>
					<div class="bg-gray-100 dark:bg-gray-800 p-2 rounded text-xs font-mono mb-2">
						&lt;header class="<span class="text-purple-600">sticky top-0</span> <span class="text-orange-600">z-50</span> bg-white border-b shadow-sm"&gt;
					</div>
					<ul class="list-disc list-inside space-y-1 ml-2">
						<li><code class="text-purple-600">sticky top-0</code>：スクロールしても上部に固定される</li>
						<li><code class="text-orange-600">z-50</code>：他の要素より前面に表示（重なり順）</li>
					</ul>
				</div>
				<div>
					<p class="font-medium text-blue-600 dark:text-blue-400 mb-2">③ メインコンテンツ</p>
					<div class="bg-gray-100 dark:bg-gray-800 p-2 rounded text-xs font-mono mb-2">
						&lt;main class="<span class="text-cyan-600">flex-1</span> <span class="text-green-600">max-w-7xl mx-auto</span> px-4 py-8 w-full"&gt;
					</div>
					<ul class="list-disc list-inside space-y-1 ml-2">
						<li><code class="text-cyan-600">flex-1</code>：残りの高さをすべて使う（フッターを下に押す）</li>
						<li><code class="text-green-600">max-w-7xl mx-auto</code>：最大幅を制限して中央に配置</li>
					</ul>
				</div>
				<div class="pt-3 border-t border-gray-200 dark:border-gray-600">
					<p class="font-medium text-green-600 dark:text-green-400 mb-1">なぜこのパターン？</p>
					<p>コンテンツが少なくても<code>flex-1</code>のおかげでフッターは常に画面下部に配置されます。</p>
				</div>
			</div>
		</div>
	</section>

	<!-- サイドバーレイアウト -->
	<section class="mb-10">
		<h2 id="sidebar" class="text-xl font-bold mb-4">サイドバーレイアウト</h2>

		<CodePreview
			title="固定サイドバー"
			description="管理画面・ドキュメントサイト向け"
			language="html"
			code={`<div class="flex min-h-screen">
  <!-- サイドバー（固定幅） -->
  <aside class="w-64 bg-gray-900 text-white flex-shrink-0">
    <div class="p-4">
      <h1 class="text-xl font-bold mb-6">Admin</h1>
      <nav class="space-y-2">
        <a href="/dashboard" class="block px-4 py-2 rounded-lg bg-gray-800 hover:bg-gray-700">
          ダッシュボード
        </a>
        <a href="/users" class="block px-4 py-2 rounded-lg hover:bg-gray-700">
          ユーザー
        </a>
        <a href="/settings" class="block px-4 py-2 rounded-lg hover:bg-gray-700">
          設定
        </a>
      </nav>
    </div>
  </aside>

  <!-- メインエリア -->
  <div class="flex-1 flex flex-col">
    <!-- ヘッダー -->
    <header class="bg-white border-b px-6 py-4 flex items-center justify-between">
      <h2 class="text-lg font-semibold">ダッシュボード</h2>
      <div class="flex items-center gap-4">
        <span>田中さん</span>
        <button>ログアウト</button>
      </div>
    </header>

    <!-- コンテンツ -->
    <main class="flex-1 p-6 bg-gray-50">
      <div class="grid grid-cols-1 md:grid-cols-3 gap-6">
        <!-- カード -->
      </div>
    </main>
  </div>
</div>`}
			previewHtml={`<div style="display:flex;border:1px solid #e5e7eb;border-radius:8px;overflow:hidden;min-height:150px;"><div style="width:100px;background:#111827;color:white;padding:12px;flex-shrink:0;"><div style="font-weight:bold;margin-bottom:12px;font-size:14px;">Admin</div><div style="font-size:11px;space-y:4px;"><div style="background:#1f2937;padding:4px 8px;border-radius:4px;margin-bottom:4px;">ダッシュボード</div><div style="padding:4px 8px;">ユーザー</div><div style="padding:4px 8px;">設定</div></div></div><div style="flex:1;display:flex;flex-direction:column;"><div style="background:white;padding:8px 12px;border-bottom:1px solid #e5e7eb;display:flex;justify-content:space-between;font-size:12px;"><span style="font-weight:600;">ダッシュボード</span><span style="color:#6b7280;">田中さん</span></div><div style="flex:1;background:#f9fafb;padding:12px;"><div style="display:grid;grid-template-columns:repeat(3,1fr);gap:8px;"><div style="background:white;padding:8px;border-radius:4px;text-align:center;font-size:10px;border:1px solid #e5e7eb;">カード</div><div style="background:white;padding:8px;border-radius:4px;text-align:center;font-size:10px;border:1px solid #e5e7eb;">カード</div><div style="background:white;padding:8px;border-radius:4px;text-align:center;font-size:10px;border:1px solid #e5e7eb;">カード</div></div></div></div></div>`}
		/>

		<div class="mt-4 p-4 rounded-lg bg-gray-50 dark:bg-gray-800/50 border border-gray-200 dark:border-gray-700">
			<p class="font-semibold text-gray-800 dark:text-gray-200 mb-3">コード解説：各クラスの役割</p>
			<div class="text-sm text-gray-700 dark:text-gray-300 space-y-4">
				<div>
					<p class="font-medium text-blue-600 dark:text-blue-400 mb-2">① 全体のコンテナ</p>
					<div class="bg-gray-100 dark:bg-gray-800 p-2 rounded text-xs font-mono mb-2">
						&lt;div class="<span class="text-cyan-600">flex</span> <span class="text-green-600">min-h-screen</span>"&gt;
					</div>
					<ul class="list-disc list-inside space-y-1 ml-2">
						<li><code class="text-cyan-600">flex</code>：子要素を横並びにする（Flexbox）</li>
						<li><code class="text-green-600">min-h-screen</code>：最低でも画面の高さを確保（100vh）</li>
					</ul>
				</div>
				<div>
					<p class="font-medium text-blue-600 dark:text-blue-400 mb-2">② サイドバー</p>
					<div class="bg-gray-100 dark:bg-gray-800 p-2 rounded text-xs font-mono mb-2">
						&lt;aside class="<span class="text-purple-600">w-64</span> <span class="text-orange-600">bg-gray-900 text-white</span> <span class="text-pink-600">flex-shrink-0</span>"&gt;
					</div>
					<ul class="list-disc list-inside space-y-1 ml-2">
						<li><code class="text-purple-600">w-64</code>：幅256px固定（16rem × 16px）</li>
						<li><code class="text-orange-600">bg-gray-900 text-white</code>：暗い背景色と白文字</li>
						<li><code class="text-pink-600">flex-shrink-0</code>：画面が狭くなっても縮まない</li>
					</ul>
				</div>
				<div>
					<p class="font-medium text-blue-600 dark:text-blue-400 mb-2">③ ナビゲーションリンク</p>
					<div class="bg-gray-100 dark:bg-gray-800 p-2 rounded text-xs font-mono mb-2">
						&lt;a class="<span class="text-cyan-600">block</span> <span class="text-green-600">px-4 py-2</span> <span class="text-orange-600">rounded-lg</span> <span class="text-purple-600">hover:bg-gray-700</span>"&gt;
					</div>
					<ul class="list-disc list-inside space-y-1 ml-2">
						<li><code class="text-cyan-600">block</code>：ブロック要素に（クリック範囲が広がる）</li>
						<li><code class="text-green-600">px-4 py-2</code>：左右16px、上下8pxの余白</li>
						<li><code class="text-orange-600">rounded-lg</code>：角を丸く（8px）</li>
						<li><code class="text-purple-600">hover:bg-gray-700</code>：マウスを乗せた時に背景色変更</li>
					</ul>
				</div>
				<div>
					<p class="font-medium text-blue-600 dark:text-blue-400 mb-2">④ メインエリア</p>
					<div class="bg-gray-100 dark:bg-gray-800 p-2 rounded text-xs font-mono mb-2">
						&lt;div class="<span class="text-cyan-600">flex-1</span> <span class="text-green-600">flex flex-col</span>"&gt;
					</div>
					<ul class="list-disc list-inside space-y-1 ml-2">
						<li><code class="text-cyan-600">flex-1</code>：残りの幅すべてを占める</li>
						<li><code class="text-green-600">flex flex-col</code>：中を縦並びに（ヘッダー→コンテンツ）</li>
					</ul>
				</div>
				<div>
					<p class="font-medium text-blue-600 dark:text-blue-400 mb-2">⑤ ヘッダー</p>
					<div class="bg-gray-100 dark:bg-gray-800 p-2 rounded text-xs font-mono mb-2">
						&lt;header class="bg-white <span class="text-orange-600">border-b</span> px-6 py-4 <span class="text-purple-600">flex items-center justify-between</span>"&gt;
					</div>
					<ul class="list-disc list-inside space-y-1 ml-2">
						<li><code class="text-orange-600">border-b</code>：下に線を引く</li>
						<li><code class="text-purple-600">flex items-center justify-between</code>：左右に要素を配置、縦中央揃え</li>
					</ul>
				</div>
				<div>
					<p class="font-medium text-blue-600 dark:text-blue-400 mb-2">⑥ コンテンツエリア</p>
					<div class="bg-gray-100 dark:bg-gray-800 p-2 rounded text-xs font-mono mb-2">
						&lt;main class="<span class="text-cyan-600">flex-1</span> p-6 <span class="text-green-600">bg-gray-50</span>"&gt;
					</div>
					<ul class="list-disc list-inside space-y-1 ml-2">
						<li><code class="text-cyan-600">flex-1</code>：残りの高さをすべて使う</li>
						<li><code class="text-green-600">bg-gray-50</code>：薄いグレーの背景</li>
					</ul>
				</div>
				<div class="pt-3 border-t border-gray-200 dark:border-gray-600">
					<p class="font-medium text-green-600 dark:text-green-400 mb-1">組み立て結果</p>
					<p>サイドバー（256px固定）が左に、残りのスペースにヘッダー＋コンテンツが縦に並び、画面全体を埋めるレイアウトが完成します。</p>
				</div>
			</div>
		</div>

		<CodePreview
			title="折りたたみ可能なサイドバー"
			description="モバイル対応"
			language="svelte"
			code={`<script>
  let sidebarOpen = $state(false);
</script>

<div class="flex min-h-screen">
  <!-- オーバーレイ（モバイル時） -->
  {#if sidebarOpen}
    <div
      class="fixed inset-0 bg-black/50 z-40 lg:hidden"
      onclick={() => sidebarOpen = false}
    ></div>
  {/if}

  <!-- サイドバー -->
  <aside class="
    fixed lg:static inset-y-0 left-0 z-50
    w-64 bg-gray-900 text-white
    transform transition-transform duration-300
    {sidebarOpen ? 'translate-x-0' : '-translate-x-full lg:translate-x-0'}
  ">
    <!-- サイドバーの中身 -->
  </aside>

  <!-- メインエリア -->
  <div class="flex-1">
    <header class="bg-white border-b px-4 py-3">
      <!-- ハンバーガーメニュー（モバイル時のみ） -->
      <button
        class="lg:hidden p-2"
        onclick={() => sidebarOpen = true}
      >
        <svg class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24">
          <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 6h16M4 12h16M4 18h16" />
        </svg>
      </button>
    </header>
    <main class="p-6">
      <!-- コンテンツ -->
    </main>
  </div>
</div>`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div style="color:#6a9955;">// PC: サイドバー常に表示</div><div style="color:#6a9955;">// モバイル: ハンバーガーメニューで開閉</div><div style="color:#6a9955;">// lg:hidden / lg:translate-x-0 で切り替え</div></div>`}
		/>
	</section>

	<!-- ナビゲーションパターン -->
	<section class="mb-10">
		<h2 id="navigation" class="text-xl font-bold mb-4">ナビゲーションパターン</h2>

		<CodePreview
			title="レスポンシブナビゲーション"
			description="PC:横並び / モバイル:ハンバーガー"
			language="svelte"
			code={`<script>
  let menuOpen = $state(false);
</script>

<header class="bg-white shadow-sm">
  <div class="max-w-7xl mx-auto px-4">
    <div class="flex items-center justify-between h-16">
      <!-- ロゴ -->
      <a href="/" class="text-xl font-bold">Logo</a>

      <!-- デスクトップナビ -->
      <nav class="hidden md:flex items-center gap-6">
        <a href="/" class="hover:text-blue-600">ホーム</a>
        <a href="/products" class="hover:text-blue-600">製品</a>
        <a href="/about" class="hover:text-blue-600">会社概要</a>
        <a href="/contact" class="px-4 py-2 bg-blue-600 text-white rounded-lg">
          お問い合わせ
        </a>
      </nav>

      <!-- モバイルメニューボタン -->
      <button
        class="md:hidden p-2"
        onclick={() => menuOpen = !menuOpen}
      >
        <svg class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24">
          {#if menuOpen}
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12" />
          {:else}
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 6h16M4 12h16M4 18h16" />
          {/if}
        </svg>
      </button>
    </div>

    <!-- モバイルナビ -->
    {#if menuOpen}
      <nav class="md:hidden py-4 border-t">
        <a href="/" class="block py-2">ホーム</a>
        <a href="/products" class="block py-2">製品</a>
        <a href="/about" class="block py-2">会社概要</a>
        <a href="/contact" class="block py-2 mt-2 text-center bg-blue-600 text-white rounded-lg">
          お問い合わせ
        </a>
      </nav>
    {/if}
  </div>
</header>`}
			previewHtml={`<div style="border:1px solid #e5e7eb;border-radius:8px;overflow:hidden;"><div style="background:white;padding:12px 16px;display:flex;justify-content:space-between;align-items:center;"><span style="font-weight:bold;">Logo</span><div style="display:flex;gap:16px;align-items:center;font-size:13px;"><span>ホーム</span><span>製品</span><span>会社概要</span><span style="background:#2563eb;color:white;padding:6px 12px;border-radius:6px;">お問い合わせ</span></div></div></div>`}
		/>

		<CodePreview
			title="タブナビゲーション"
			description="セクション切り替え"
			language="svelte"
			code={`<script>
  let activeTab = $state('overview');
</script>

<div class="border-b border-gray-200">
  <nav class="flex gap-8">
    <button
      class="py-4 px-1 border-b-2 font-medium text-sm
        {activeTab === 'overview'
          ? 'border-blue-500 text-blue-600'
          : 'border-transparent text-gray-500 hover:text-gray-700'}"
      onclick={() => activeTab = 'overview'}
    >
      概要
    </button>
    <button
      class="py-4 px-1 border-b-2 font-medium text-sm
        {activeTab === 'features'
          ? 'border-blue-500 text-blue-600'
          : 'border-transparent text-gray-500 hover:text-gray-700'}"
      onclick={() => activeTab = 'features'}
    >
      機能
    </button>
    <button
      class="py-4 px-1 border-b-2 font-medium text-sm
        {activeTab === 'pricing'
          ? 'border-blue-500 text-blue-600'
          : 'border-transparent text-gray-500 hover:text-gray-700'}"
      onclick={() => activeTab = 'pricing'}
    >
      料金
    </button>
  </nav>
</div>

<div class="py-6">
  {#if activeTab === 'overview'}
    <p>概要コンテンツ</p>
  {:else if activeTab === 'features'}
    <p>機能コンテンツ</p>
  {:else}
    <p>料金コンテンツ</p>
  {/if}
</div>`}
			previewHtml={`<div style="border-bottom:1px solid #e5e7eb;"><div style="display:flex;gap:24px;"><span style="padding:12px 4px;border-bottom:2px solid #2563eb;color:#2563eb;font-size:13px;">概要</span><span style="padding:12px 4px;color:#6b7280;font-size:13px;">機能</span><span style="padding:12px 4px;color:#6b7280;font-size:13px;">料金</span></div></div>`}
		/>
	</section>

	<!-- フッターパターン -->
	<section class="mb-10">
		<h2 id="footer" class="text-xl font-bold mb-4">フッターパターン</h2>

		<CodePreview
			title="マルチカラムフッター"
			description="リンク集＋コピーライト"
			language="html"
			code={`<footer class="bg-gray-900 text-gray-300">
  <div class="max-w-7xl mx-auto px-4 py-12">
    <!-- リンクセクション -->
    <div class="grid grid-cols-2 md:grid-cols-4 gap-8 mb-8">
      <!-- 会社情報 -->
      <div>
        <h3 class="text-white font-semibold mb-4">Company</h3>
        <ul class="space-y-2 text-sm">
          <li><a href="/about" class="hover:text-white">会社概要</a></li>
          <li><a href="/careers" class="hover:text-white">採用情報</a></li>
          <li><a href="/news" class="hover:text-white">ニュース</a></li>
        </ul>
      </div>

      <!-- 製品 -->
      <div>
        <h3 class="text-white font-semibold mb-4">Products</h3>
        <ul class="space-y-2 text-sm">
          <li><a href="/features" class="hover:text-white">機能</a></li>
          <li><a href="/pricing" class="hover:text-white">料金</a></li>
          <li><a href="/demo" class="hover:text-white">デモ</a></li>
        </ul>
      </div>

      <!-- サポート -->
      <div>
        <h3 class="text-white font-semibold mb-4">Support</h3>
        <ul class="space-y-2 text-sm">
          <li><a href="/docs" class="hover:text-white">ドキュメント</a></li>
          <li><a href="/faq" class="hover:text-white">FAQ</a></li>
          <li><a href="/contact" class="hover:text-white">お問い合わせ</a></li>
        </ul>
      </div>

      <!-- 法的情報 -->
      <div>
        <h3 class="text-white font-semibold mb-4">Legal</h3>
        <ul class="space-y-2 text-sm">
          <li><a href="/privacy" class="hover:text-white">プライバシー</a></li>
          <li><a href="/terms" class="hover:text-white">利用規約</a></li>
        </ul>
      </div>
    </div>

    <!-- 区切り線 -->
    <div class="border-t border-gray-800 pt-8 flex flex-col md:flex-row justify-between items-center gap-4">
      <p class="text-sm">© 2024 Company. All rights reserved.</p>
      <!-- SNSリンク -->
      <div class="flex gap-4">
        <a href="#" class="hover:text-white">Twitter</a>
        <a href="#" class="hover:text-white">GitHub</a>
        <a href="#" class="hover:text-white">Discord</a>
      </div>
    </div>
  </div>
</footer>`}
			previewHtml={`<div style="background:#111827;color:#9ca3af;padding:16px;border-radius:8px;font-size:11px;"><div style="display:grid;grid-template-columns:repeat(4,1fr);gap:16px;margin-bottom:12px;"><div><div style="color:white;font-weight:600;margin-bottom:8px;">Company</div><div>会社概要</div><div>採用情報</div></div><div><div style="color:white;font-weight:600;margin-bottom:8px;">Products</div><div>機能</div><div>料金</div></div><div><div style="color:white;font-weight:600;margin-bottom:8px;">Support</div><div>ドキュメント</div><div>FAQ</div></div><div><div style="color:white;font-weight:600;margin-bottom:8px;">Legal</div><div>プライバシー</div><div>利用規約</div></div></div><div style="border-top:1px solid #374151;padding-top:12px;display:flex;justify-content:space-between;"><span>© 2024 Company</span><div style="display:flex;gap:12px;">Twitter GitHub</div></div></div>`}
		/>
	</section>

	<!-- カード・グリッド -->
	<section class="mb-10">
		<h2 id="cards" class="text-xl font-bold mb-4">カードレイアウト</h2>

		<CodePreview
			title="レスポンシブカードグリッド"
			description="画面サイズで列数が変わる"
			language="html"
			code={`<!-- モバイル:1列 / タブレット:2列 / PC:3列 -->
<div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6">
  <!-- カード -->
  <div class="bg-white rounded-xl shadow-sm border overflow-hidden hover:shadow-md transition-shadow">
    <img src="/image.jpg" alt="" class="w-full h-48 object-cover" />
    <div class="p-6">
      <span class="text-xs font-medium text-blue-600 bg-blue-50 px-2 py-1 rounded">
        カテゴリ
      </span>
      <h3 class="mt-3 text-lg font-semibold">タイトル</h3>
      <p class="mt-2 text-gray-600 text-sm line-clamp-2">
        説明文がここに入ります。長い場合は2行で切り詰められます。
      </p>
      <div class="mt-4 flex items-center justify-between">
        <span class="text-sm text-gray-500">2024/01/15</span>
        <a href="#" class="text-blue-600 text-sm font-medium hover:underline">
          詳しく見る →
        </a>
      </div>
    </div>
  </div>

  <!-- 他のカード... -->
</div>`}
			previewHtml={`<div style="display:grid;grid-template-columns:repeat(3,1fr);gap:12px;"><div style="background:white;border-radius:8px;overflow:hidden;border:1px solid #e5e7eb;"><div style="height:60px;background:linear-gradient(135deg,#667eea,#764ba2);"></div><div style="padding:12px;"><span style="font-size:10px;background:#eff6ff;color:#2563eb;padding:2px 6px;border-radius:4px;">カテゴリ</span><div style="font-weight:600;font-size:13px;margin-top:6px;">タイトル</div><div style="font-size:11px;color:#6b7280;margin-top:4px;">説明文...</div></div></div><div style="background:white;border-radius:8px;overflow:hidden;border:1px solid #e5e7eb;"><div style="height:60px;background:linear-gradient(135deg,#f093fb,#f5576c);"></div><div style="padding:12px;"><span style="font-size:10px;background:#fef3c7;color:#d97706;padding:2px 6px;border-radius:4px;">カテゴリ</span><div style="font-weight:600;font-size:13px;margin-top:6px;">タイトル</div><div style="font-size:11px;color:#6b7280;margin-top:4px;">説明文...</div></div></div><div style="background:white;border-radius:8px;overflow:hidden;border:1px solid #e5e7eb;"><div style="height:60px;background:linear-gradient(135deg,#4facfe,#00f2fe);"></div><div style="padding:12px;"><span style="font-size:10px;background:#dcfce7;color:#16a34a;padding:2px 6px;border-radius:4px;">カテゴリ</span><div style="font-weight:600;font-size:13px;margin-top:6px;">タイトル</div><div style="font-size:11px;color:#6b7280;margin-top:4px;">説明文...</div></div></div></div>`}
		/>

		<div class="mt-4 p-4 rounded-lg bg-gray-50 dark:bg-gray-800/50 border border-gray-200 dark:border-gray-700">
			<p class="font-semibold text-gray-800 dark:text-gray-200 mb-3">コード解説：カードグリッドの仕組み</p>
			<div class="text-sm text-gray-700 dark:text-gray-300 space-y-4">
				<div>
					<p class="font-medium text-blue-600 dark:text-blue-400 mb-2">① グリッドコンテナ（レスポンシブ）</p>
					<div class="bg-gray-100 dark:bg-gray-800 p-2 rounded text-xs font-mono mb-2">
						&lt;div class="<span class="text-cyan-600">grid</span> <span class="text-green-600">grid-cols-1</span> <span class="text-purple-600">md:grid-cols-2</span> <span class="text-orange-600">lg:grid-cols-3</span> gap-6"&gt;
					</div>
					<ul class="list-disc list-inside space-y-1 ml-2">
						<li><code class="text-cyan-600">grid</code>：CSS Gridレイアウトを有効化</li>
						<li><code class="text-green-600">grid-cols-1</code>：デフォルトで1列（モバイル）</li>
						<li><code class="text-purple-600">md:grid-cols-2</code>：768px以上で2列</li>
						<li><code class="text-orange-600">lg:grid-cols-3</code>：1024px以上で3列</li>
						<li><code>gap-6</code>：カード間の隙間（24px）</li>
					</ul>
				</div>
				<div>
					<p class="font-medium text-blue-600 dark:text-blue-400 mb-2">② カード本体</p>
					<div class="bg-gray-100 dark:bg-gray-800 p-2 rounded text-xs font-mono mb-2">
						&lt;div class="bg-white <span class="text-cyan-600">rounded-xl</span> <span class="text-green-600">shadow-sm</span> border <span class="text-purple-600">overflow-hidden</span> <span class="text-orange-600">hover:shadow-md transition-shadow</span>"&gt;
					</div>
					<ul class="list-disc list-inside space-y-1 ml-2">
						<li><code class="text-cyan-600">rounded-xl</code>：大きめの角丸（12px）</li>
						<li><code class="text-green-600">shadow-sm</code>：軽い影</li>
						<li><code class="text-purple-600">overflow-hidden</code>：角丸から画像がはみ出ないように</li>
						<li><code class="text-orange-600">hover:shadow-md transition-shadow</code>：ホバー時に影を大きく（アニメーション付き）</li>
					</ul>
				</div>
				<div>
					<p class="font-medium text-blue-600 dark:text-blue-400 mb-2">③ 画像</p>
					<div class="bg-gray-100 dark:bg-gray-800 p-2 rounded text-xs font-mono mb-2">
						&lt;img class="<span class="text-cyan-600">w-full</span> <span class="text-green-600">h-48</span> <span class="text-purple-600">object-cover</span>"&gt;
					</div>
					<ul class="list-disc list-inside space-y-1 ml-2">
						<li><code class="text-cyan-600">w-full</code>：横幅いっぱい</li>
						<li><code class="text-green-600">h-48</code>：高さ192px固定</li>
						<li><code class="text-purple-600">object-cover</code>：縦横比を保ちつつ領域を埋める（トリミング）</li>
					</ul>
				</div>
				<div>
					<p class="font-medium text-blue-600 dark:text-blue-400 mb-2">④ カテゴリバッジ</p>
					<div class="bg-gray-100 dark:bg-gray-800 p-2 rounded text-xs font-mono mb-2">
						&lt;span class="<span class="text-cyan-600">text-xs</span> font-medium <span class="text-green-600">text-blue-600 bg-blue-50</span> px-2 py-1 rounded"&gt;
					</div>
					<ul class="list-disc list-inside space-y-1 ml-2">
						<li><code class="text-cyan-600">text-xs</code>：小さい文字</li>
						<li><code class="text-green-600">text-blue-600 bg-blue-50</code>：青文字に薄い青背景</li>
					</ul>
				</div>
				<div>
					<p class="font-medium text-blue-600 dark:text-blue-400 mb-2">⑤ フッター部分</p>
					<div class="bg-gray-100 dark:bg-gray-800 p-2 rounded text-xs font-mono mb-2">
						&lt;div class="<span class="text-purple-600">flex items-center justify-between</span>"&gt;
					</div>
					<p class="ml-2"><code class="text-purple-600">flex items-center justify-between</code>：日付を左、リンクを右に配置</p>
				</div>
			</div>
		</div>
	</section>

	<!-- よく使うパターン -->
	<section class="mb-10">
		<h2 id="patterns" class="text-xl font-bold mb-4">覚えておきたいパターン</h2>

		<div class="space-y-4">
			<div class="p-4 rounded-lg bg-gray-100 dark:bg-gray-800">
				<p class="font-semibold text-gray-800 dark:text-gray-200 mb-2">中央寄せコンテナ</p>
				<code class="text-sm bg-gray-200 dark:bg-gray-700 px-2 py-1 rounded">max-w-7xl mx-auto px-4</code>
				<p class="text-sm text-gray-600 dark:text-gray-400 mt-2">最大幅を制限して中央に配置、左右に余白</p>
			</div>

			<div class="p-4 rounded-lg bg-gray-100 dark:bg-gray-800">
				<p class="font-semibold text-gray-800 dark:text-gray-200 mb-2">画面全体を埋める</p>
				<code class="text-sm bg-gray-200 dark:bg-gray-700 px-2 py-1 rounded">min-h-screen flex flex-col</code>
				<p class="text-sm text-gray-600 dark:text-gray-400 mt-2">フッターを常に画面下に配置</p>
			</div>

			<div class="p-4 rounded-lg bg-gray-100 dark:bg-gray-800">
				<p class="font-semibold text-gray-800 dark:text-gray-200 mb-2">上に固定</p>
				<code class="text-sm bg-gray-200 dark:bg-gray-700 px-2 py-1 rounded">sticky top-0 z-50</code>
				<p class="text-sm text-gray-600 dark:text-gray-400 mt-2">スクロールしても上部に固定</p>
			</div>

			<div class="p-4 rounded-lg bg-gray-100 dark:bg-gray-800">
				<p class="font-semibold text-gray-800 dark:text-gray-200 mb-2">残りを埋める</p>
				<code class="text-sm bg-gray-200 dark:bg-gray-700 px-2 py-1 rounded">flex-1</code>
				<p class="text-sm text-gray-600 dark:text-gray-400 mt-2">Flexbox内で残りのスペースを占める</p>
			</div>

			<div class="p-4 rounded-lg bg-gray-100 dark:bg-gray-800">
				<p class="font-semibold text-gray-800 dark:text-gray-200 mb-2">PC/モバイル切り替え</p>
				<code class="text-sm bg-gray-200 dark:bg-gray-700 px-2 py-1 rounded">hidden md:flex / md:hidden</code>
				<p class="text-sm text-gray-600 dark:text-gray-400 mt-2">画面サイズで表示/非表示を切り替え</p>
			</div>
		</div>
	</section>

	<!-- ナビゲーション -->
	<div class="flex justify-between pt-6 border-t border-gray-200 dark:border-gray-700">
		<a href="/tailwind/responsive" class="inline-flex items-center gap-2 px-4 py-2 rounded-lg border border-gray-300 dark:border-gray-600 hover:bg-gray-100 dark:hover:bg-gray-800 transition-colors">
			<svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
				<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 19l-7-7 7-7" />
			</svg>
			前へ：レスポンシブ
		</a>
		<a href="/tailwind/customize" class="inline-flex items-center gap-2 px-4 py-2 rounded-lg bg-primary-600 text-white hover:bg-primary-700 transition-colors">
			次へ：カスタマイズ
			<svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
				<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 5l7 7-7 7" />
			</svg>
		</a>
	</div>
</article>
