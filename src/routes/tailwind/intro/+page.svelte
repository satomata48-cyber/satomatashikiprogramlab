<script>
	import CodePreview from '$lib/components/CodePreview.svelte';
	import FeatureCard from '$lib/components/FeatureCard.svelte';

	const features = [
		{ icon: '⚡', title: 'ユーティリティファースト', description: 'クラス名でスタイルを直接適用', tag: '特徴' },
		{ icon: '📱', title: 'レスポンシブ対応', description: 'sm:, md:, lg:で画面サイズ対応', tag: '便利' },
		{ icon: '🌙', title: 'ダークモード', description: 'dark:プレフィックスで簡単実装', tag: '便利' },
		{ icon: '🎨', title: 'カスタマイズ', description: 'tailwind.config.jsで自由に設定', tag: '柔軟' },
		{ icon: '🔄', title: 'ホバー・フォーカス', description: 'hover:, focus:で状態スタイル', tag: '基本' },
		{ icon: '📦', title: '小さなバンドル', description: '使用クラスのみ出力', tag: '性能' }
	];
</script>

<svelte:head>
	<title>Tailwind CSS はじめに | さとまたラボ</title>
</svelte:head>

<article>
	<h1 class="text-3xl font-bold mb-2">Tailwind CSS</h1>
	<p class="text-lg text-gray-600 dark:text-gray-400 mb-8">
		ユーティリティファーストのモダンCSSフレームワーク
	</p>

	<!-- Tailwindとは -->
	<section class="mb-10">
		<h2 id="what-is" class="text-xl font-bold mb-4">Tailwind CSSとは？</h2>

		<div class="p-6 rounded-xl bg-blue-50 dark:bg-blue-900/20 border border-blue-200 dark:border-blue-800 mb-6">
			<p class="text-blue-800 dark:text-blue-200 mb-4">
				<strong>日常での例え：</strong>レゴブロック
			</p>
			<div class="grid grid-cols-1 md:grid-cols-2 gap-4 text-sm">
				<div class="p-3 bg-white dark:bg-gray-800 rounded-lg">
					<div class="font-semibold text-blue-700 dark:text-blue-300 mb-2">普通のCSS = 粘土</div>
					<p class="text-gray-600 dark:text-gray-400">
						自由に形を作れるが、<br>
						毎回ゼロから成形が必要
					</p>
				</div>
				<div class="p-3 bg-white dark:bg-gray-800 rounded-lg">
					<div class="font-semibold text-blue-700 dark:text-blue-300 mb-2">Tailwind = レゴブロック</div>
					<p class="text-gray-600 dark:text-gray-400">
						用意されたパーツ（クラス）を<br>
						組み合わせるだけで完成
					</p>
				</div>
			</div>
		</div>

		<div class="p-4 rounded-lg bg-amber-50 dark:bg-amber-900/20 border border-amber-200 dark:border-amber-800 mb-6">
			<p class="font-semibold text-amber-800 dark:text-amber-200">「ユーティリティファースト」とは？</p>
			<div class="text-sm text-amber-700 dark:text-amber-300 mt-2">
				<p class="mb-2">
					<strong>従来の方法</strong>：CSSファイルに <code class="bg-amber-200 dark:bg-amber-800 px-1 rounded">.card &#123; padding: 16px; &#125;</code> と書く
				</p>
				<p class="mb-2">
					<strong>Tailwind</strong>：HTMLに直接 <code class="bg-amber-200 dark:bg-amber-800 px-1 rounded">class="p-4"</code> と書く
				</p>
				<p>→ CSSファイルを行き来せず、HTMLだけ見れば完結する！</p>
			</div>
		</div>

		<div class="p-4 rounded-lg bg-gray-100 dark:bg-gray-800 mb-6">
			<p class="font-semibold text-gray-800 dark:text-gray-200 mb-2">なぜTailwindが人気？</p>
			<div class="text-sm text-gray-700 dark:text-gray-300 space-y-1">
				<p>✓ CSSを書かずにスタイリングできる → 開発が速い</p>
				<p>✓ クラス名を考える必要がない →「このボタンは何クラス名にしよう...」がなくなる</p>
				<p>✓ 使ったクラスだけが出力される → ファイルサイズが小さい</p>
				<p>✓ デザインシステムが自然と統一される → 一貫性のあるUI</p>
			</div>
		</div>
	</section>

	<!-- できること一覧 -->
	<section class="mb-10">
		<h2 id="features" class="text-xl font-bold mb-4">Tailwindでできること</h2>
		<div class="grid grid-cols-1 md:grid-cols-2 gap-3">
			{#each features as feature}
				<FeatureCard {...feature} />
			{/each}
		</div>
	</section>

	<!-- コード例 -->
	<section class="mb-10">
		<h2 id="examples" class="text-xl font-bold mb-4">コード例とプレビュー</h2>

		<CodePreview
			title="基本的なスタイリング"
			description="クラス名で直接スタイル適用"
			language="html"
			code={`<div class="p-4 bg-blue-500 text-white rounded-lg">
  パディング、背景色、文字色、角丸
</div>

<p class="text-xl font-bold text-gray-800">
  大きめの太字テキスト
</p>

<button class="px-4 py-2 bg-green-500 text-white rounded">
  ボタン
</button>`}
			previewHtml={`<div style="display:flex;flex-direction:column;gap:12px;"><div style="padding:16px;background:#3b82f6;color:white;border-radius:8px;">パディング、背景色、文字色、角丸</div><p style="font-size:20px;font-weight:bold;color:#1f2937;">大きめの太字テキスト</p><button style="padding:8px 16px;background:#22c55e;color:white;border:none;border-radius:4px;">ボタン</button></div>`}
		/>

		<CodePreview
			title="スペーシング"
			description="m-（margin）、p-（padding）"
			language="html"
			code={`<!-- マージン -->
<div class="m-4">全方向margin: 1rem</div>
<div class="mx-4">左右margin: 1rem</div>
<div class="my-2">上下margin: 0.5rem</div>
<div class="mt-8">上margin: 2rem</div>

<!-- パディング -->
<div class="p-6">全方向padding: 1.5rem</div>
<div class="px-4 py-2">左右1rem、上下0.5rem</div>

<!-- 数値: 1=0.25rem, 4=1rem, 8=2rem -->`}
			previewHtml={`<div style="display:flex;gap:8px;flex-wrap:wrap;"><div style="margin:16px;padding:8px;background:#e5e7eb;border-radius:4px;">m-4</div><div style="padding:24px;background:#dbeafe;border-radius:4px;">p-6</div><div style="padding:8px 16px;background:#dcfce7;border-radius:4px;">px-4 py-2</div></div>`}
		/>

		<CodePreview
			title="Flexbox"
			description="flexとgapで簡単レイアウト"
			language="html"
			code={`<div class="flex items-center justify-between gap-4">
  <div>左</div>
  <div>中央</div>
  <div>右</div>
</div>

<div class="flex flex-col gap-2">
  <div>縦並び1</div>
  <div>縦並び2</div>
</div>

<div class="flex flex-wrap gap-2">
  <div>折り返し対応</div>
</div>`}
			previewHtml={`<div style="display:flex;flex-direction:column;gap:16px;"><div style="display:flex;align-items:center;justify-content:space-between;gap:16px;background:#f3f4f6;padding:12px;border-radius:8px;"><span style="background:#3b82f6;color:white;padding:4px 12px;border-radius:4px;">左</span><span style="background:#3b82f6;color:white;padding:4px 12px;border-radius:4px;">中央</span><span style="background:#3b82f6;color:white;padding:4px 12px;border-radius:4px;">右</span></div><div style="display:flex;flex-direction:column;gap:8px;"><div style="background:#dbeafe;padding:8px;border-radius:4px;">縦並び1</div><div style="background:#dbeafe;padding:8px;border-radius:4px;">縦並び2</div></div></div>`}
		/>

		<CodePreview
			title="Grid"
			description="grid-colsでグリッドレイアウト"
			language="html"
			code={`<div class="grid grid-cols-3 gap-4">
  <div class="bg-purple-500 p-4 text-white">1</div>
  <div class="bg-purple-500 p-4 text-white">2</div>
  <div class="bg-purple-500 p-4 text-white">3</div>
  <div class="bg-purple-500 p-4 text-white">4</div>
  <div class="bg-purple-500 p-4 text-white">5</div>
  <div class="bg-purple-500 p-4 text-white">6</div>
</div>`}
			previewHtml={`<div style="display:grid;grid-template-columns:repeat(3,1fr);gap:16px;"><div style="background:#a855f7;padding:16px;color:white;text-align:center;border-radius:4px;">1</div><div style="background:#a855f7;padding:16px;color:white;text-align:center;border-radius:4px;">2</div><div style="background:#a855f7;padding:16px;color:white;text-align:center;border-radius:4px;">3</div><div style="background:#a855f7;padding:16px;color:white;text-align:center;border-radius:4px;">4</div><div style="background:#a855f7;padding:16px;color:white;text-align:center;border-radius:4px;">5</div><div style="background:#a855f7;padding:16px;color:white;text-align:center;border-radius:4px;">6</div></div>`}
		/>

		<CodePreview
			title="レスポンシブデザイン"
			description="sm:, md:, lg:, xl:で画面サイズ対応"
			language="html"
			code={`<!-- モバイル1列、タブレット2列、PC3列 -->
<div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-4">
  <div>Item 1</div>
  <div>Item 2</div>
  <div>Item 3</div>
</div>

<!-- 画面サイズで表示切り替え -->
<div class="block md:hidden">モバイルのみ表示</div>
<div class="hidden md:block">タブレット以上で表示</div>

<!-- ブレークポイント -->
<!-- sm: 640px, md: 768px, lg: 1024px, xl: 1280px -->`}
			previewHtml={`<div style="background:#f3f4f6;padding:12px;border-radius:8px;text-align:center;font-size:14px;"><div style="color:#6b7280;">画面幅に応じてレイアウト変化</div><div style="display:flex;gap:8px;margin-top:8px;justify-content:center;"><span style="background:#3b82f6;color:white;padding:2px 8px;border-radius:4px;font-size:12px;">sm:640px</span><span style="background:#8b5cf6;color:white;padding:2px 8px;border-radius:4px;font-size:12px;">md:768px</span><span style="background:#ec4899;color:white;padding:2px 8px;border-radius:4px;font-size:12px;">lg:1024px</span></div></div>`}
		/>

		<CodePreview
			title="ホバー・フォーカス"
			description="hover:, focus:で状態スタイル"
			language="html"
			code={`<button class="
  bg-blue-500
  hover:bg-blue-600
  active:bg-blue-700
  text-white
  px-4 py-2
  rounded
  transition
">
  ホバーで色が変わる
</button>

<input
  class="
    border border-gray-300
    focus:border-blue-500
    focus:ring-2
    focus:ring-blue-200
    rounded px-3 py-2
    outline-none
  "
  placeholder="フォーカスで枠線変化"
>`}
			previewHtml={`<div style="display:flex;flex-direction:column;gap:12px;align-items:flex-start;"><button style="background:#3b82f6;color:white;padding:8px 16px;border:none;border-radius:4px;cursor:pointer;transition:background 0.2s;" onmouseover="this.style.background='#2563eb'" onmouseout="this.style.background='#3b82f6'">ホバーで色が変わる</button><input style="border:2px solid #d1d5db;border-radius:4px;padding:8px 12px;outline:none;width:200px;" placeholder="フォーカスで枠線変化" onfocus="this.style.borderColor='#3b82f6'" onblur="this.style.borderColor='#d1d5db'"></div>`}
		/>

		<CodePreview
			title="ダークモード"
			description="dark:プレフィックスで切り替え"
			language="html"
			code={`<div class="bg-white dark:bg-gray-800 p-4 rounded-lg">
  <h2 class="text-gray-900 dark:text-white">
    タイトル
  </h2>
  <p class="text-gray-600 dark:text-gray-300">
    本文テキスト
  </p>
</div>

<!-- tailwind.config.js で darkMode: 'class' を設定 -->
<!-- <html class="dark"> でダークモード有効 -->`}
			previewHtml={`<div style="display:flex;gap:16px;"><div style="background:white;padding:16px;border-radius:8px;border:1px solid #e5e7eb;"><h2 style="color:#111827;font-weight:bold;margin-bottom:4px;">ライト</h2><p style="color:#4b5563;font-size:14px;">本文テキスト</p></div><div style="background:#1f2937;padding:16px;border-radius:8px;"><h2 style="color:white;font-weight:bold;margin-bottom:4px;">ダーク</h2><p style="color:#d1d5db;font-size:14px;">本文テキスト</p></div></div>`}
		/>

		<CodePreview
			title="カード例"
			description="よく使うコンポーネント例"
			language="html"
			code={`<div class="max-w-sm rounded-xl overflow-hidden shadow-lg bg-white">
  <img class="w-full h-48 object-cover" src="image.jpg" alt="">
  <div class="p-6">
    <h3 class="font-bold text-xl mb-2">カードタイトル</h3>
    <p class="text-gray-600 text-sm">
      カードの説明文がここに入ります。
    </p>
    <button class="mt-4 w-full bg-blue-500 hover:bg-blue-600
                   text-white py-2 rounded-lg transition">
      詳細を見る
    </button>
  </div>
</div>`}
			previewHtml={`<div style="max-width:280px;border-radius:12px;overflow:hidden;box-shadow:0 10px 15px -3px rgba(0,0,0,0.1);background:white;"><div style="height:120px;background:linear-gradient(135deg,#667eea 0%,#764ba2 100%);"></div><div style="padding:20px;"><h3 style="font-weight:bold;font-size:18px;margin-bottom:8px;color:#111827;">カードタイトル</h3><p style="color:#4b5563;font-size:14px;">カードの説明文がここに入ります。</p><button style="margin-top:16px;width:100%;background:#3b82f6;color:white;padding:8px;border:none;border-radius:8px;cursor:pointer;">詳細を見る</button></div></div>`}
		/>
	</section>

	<!-- よく使うクラス -->
	<section class="mb-10">
		<h2 id="cheatsheet" class="text-xl font-bold mb-4">よく使うクラス一覧</h2>

		<div class="grid grid-cols-1 md:grid-cols-2 gap-4">
			<div class="p-4 rounded-lg bg-gray-100 dark:bg-gray-800">
				<h3 class="font-semibold mb-2">サイズ</h3>
				<div class="text-sm space-y-1 font-mono text-gray-600 dark:text-gray-400">
					<div>w-full, w-1/2, w-64</div>
					<div>h-screen, h-full, h-32</div>
					<div>max-w-md, min-h-screen</div>
				</div>
			</div>
			<div class="p-4 rounded-lg bg-gray-100 dark:bg-gray-800">
				<h3 class="font-semibold mb-2">テキスト</h3>
				<div class="text-sm space-y-1 font-mono text-gray-600 dark:text-gray-400">
					<div>text-sm, text-lg, text-2xl</div>
					<div>font-bold, font-medium</div>
					<div>text-center, text-right</div>
				</div>
			</div>
			<div class="p-4 rounded-lg bg-gray-100 dark:bg-gray-800">
				<h3 class="font-semibold mb-2">色</h3>
				<div class="text-sm space-y-1 font-mono text-gray-600 dark:text-gray-400">
					<div>bg-blue-500, bg-gray-100</div>
					<div>text-white, text-gray-900</div>
					<div>border-gray-200</div>
				</div>
			</div>
			<div class="p-4 rounded-lg bg-gray-100 dark:bg-gray-800">
				<h3 class="font-semibold mb-2">レイアウト</h3>
				<div class="text-sm space-y-1 font-mono text-gray-600 dark:text-gray-400">
					<div>flex, grid, block, hidden</div>
					<div>items-center, justify-between</div>
					<div>gap-4, space-x-2</div>
				</div>
			</div>
		</div>
	</section>

	<!-- ナビゲーション -->
	<div class="flex justify-between pt-6 border-t border-gray-200 dark:border-gray-700">
		<a href="/sveltekit/intro" class="inline-flex items-center gap-2 px-4 py-2 rounded-lg border border-gray-300 dark:border-gray-600 hover:bg-gray-100 dark:hover:bg-gray-800 transition-colors">
			<svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
				<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 19l-7-7 7-7" />
			</svg>
			前へ：SvelteKit
		</a>
		<a href="/tailwind/utilities" class="inline-flex items-center gap-2 px-4 py-2 rounded-lg bg-primary-600 text-white hover:bg-primary-700 transition-colors">
			次へ：ユーティリティ
			<svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
				<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 5l7 7-7 7" />
			</svg>
		</a>
	</div>
</article>
