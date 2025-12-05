<script>
	import CodePreview from '$lib/components/CodePreview.svelte';
</script>

<svelte:head>
	<title>Viteとは | さとまたラボ</title>
</svelte:head>

<article>
	<h1 class="text-3xl font-bold mb-2">Viteとは</h1>
	<p class="text-lg text-gray-600 dark:text-gray-400 mb-8">
		SvelteKitの裏側で動いている高速ビルドツールを理解しよう
	</p>

	<!-- Viteとは -->
	<section class="mb-12">
		<h2 id="what-is-vite" class="text-xl font-bold mb-4">Viteって何？</h2>

		<div class="p-6 rounded-xl bg-gradient-to-r from-purple-50 to-blue-50 dark:from-purple-900/20 dark:to-blue-900/20 border border-purple-200 dark:border-purple-800 mb-6">
			<p class="text-lg text-purple-800 dark:text-purple-200 mb-4">
				<strong>Vite（ヴィート）</strong> = 開発を超高速にするツール
			</p>
			<p class="text-sm text-purple-700 dark:text-purple-300">
				フランス語で「速い」という意味。
				開発サーバーの起動やファイル変更の反映が非常に高速です。
			</p>
		</div>

		<div class="p-4 rounded-lg bg-blue-50 dark:bg-blue-900/20 border border-blue-200 dark:border-blue-800 mb-6">
			<p class="font-semibold text-blue-800 dark:text-blue-200 mb-2">Vue.jsの作者が開発</p>
			<p class="text-sm text-blue-700 dark:text-blue-300">
				ViteはVue.jsの作者であるEvan You（エヴァン・ユー）が開発しました。
				でもVue専用ではなく、React、Svelte、その他のフレームワークでも使えます。
			</p>
		</div>
	</section>

	<!-- ビルドツールとは -->
	<section class="mb-12">
		<h2 id="what-is-build-tool" class="text-xl font-bold mb-4">ビルドツールって何？</h2>

		<p class="text-gray-700 dark:text-gray-300 mb-4">
			まず「なぜビルドツールが必要なの？」を理解しましょう。
		</p>

		<div class="p-4 rounded-lg bg-amber-50 dark:bg-amber-900/20 border border-amber-200 dark:border-amber-800 mb-6">
			<p class="font-semibold text-amber-800 dark:text-amber-200 mb-3">現代のウェブ開発の問題</p>
			<div class="text-sm text-amber-700 dark:text-amber-300 space-y-2">
				<p>1. ファイルがたくさんある（.svelte, .ts, .css, ...）</p>
				<p>2. ブラウザは .svelte や .ts を直接理解できない</p>
				<p>3. 100個のファイルを別々に読み込むと遅い</p>
			</div>
		</div>

		<div class="grid md:grid-cols-2 gap-4 mb-6">
			<div class="p-4 rounded-lg bg-gray-50 dark:bg-gray-800 border border-gray-200 dark:border-gray-700">
				<p class="font-semibold text-gray-800 dark:text-gray-200 mb-3">ビルドツールがやること</p>
				<div class="text-sm text-gray-600 dark:text-gray-400 space-y-2">
					<p>1. <strong>変換</strong>: .svelte → .js に変換</p>
					<p>2. <strong>バンドル</strong>: 複数ファイルを1つにまとめる</p>
					<p>3. <strong>最適化</strong>: 不要なコードを削除、圧縮</p>
				</div>
			</div>
			<div class="p-4 rounded-lg bg-green-50 dark:bg-green-900/20 border border-green-200 dark:border-green-800">
				<p class="font-semibold text-green-800 dark:text-green-200 mb-3">結果</p>
				<div class="text-sm text-green-700 dark:text-green-300 space-y-2">
					<p>ブラウザが理解できる形式になる</p>
					<p>ファイル数が減って読み込みが速くなる</p>
					<p>ファイルサイズが小さくなる</p>
				</div>
			</div>
		</div>

		<div class="bg-gray-900 rounded-lg p-4 font-mono text-sm">
			<p class="text-gray-400 mb-2"># ビルドのイメージ</p>
			<div class="text-gray-300">
				<p>src/routes/+page.svelte</p>
				<p>src/routes/about/+page.svelte</p>
				<p>src/lib/components/Button.svelte</p>
				<p>src/lib/styles/global.css</p>
				<p class="text-gray-500">... 100個以上のファイル</p>
			</div>
			<p class="text-purple-400 my-2 text-center">↓ Viteがビルド ↓</p>
			<div class="text-green-400">
				<p>build/app.js （最適化済み）</p>
				<p>build/style.css （最適化済み）</p>
			</div>
		</div>
	</section>

	<!-- Viteの特徴 -->
	<section class="mb-12">
		<h2 id="features" class="text-xl font-bold mb-4">Viteが速い理由</h2>

		<div class="space-y-6">
			<!-- ESModules -->
			<div class="p-5 rounded-xl bg-purple-50 dark:bg-purple-900/20 border border-purple-200 dark:border-purple-800">
				<div class="flex items-start gap-3">
					<span class="w-8 h-8 bg-purple-500 text-white rounded-full flex items-center justify-center font-bold">1</span>
					<div>
						<p class="font-semibold text-purple-800 dark:text-purple-200">開発時はバンドルしない</p>
						<p class="text-sm text-purple-700 dark:text-purple-300 mt-2">
							従来のツール（Webpack等）は、開発時も全ファイルをバンドルしていました。
							ファイルが増えると、サーバー起動に何十秒もかかることも。
						</p>
						<p class="text-sm text-purple-700 dark:text-purple-300 mt-2">
							Viteは開発時にはバンドルせず、ブラウザの「ESModules」機能を使って
							必要なファイルだけを読み込みます。
						</p>
					</div>
				</div>
			</div>

			<!-- HMR -->
			<div class="p-5 rounded-xl bg-blue-50 dark:bg-blue-900/20 border border-blue-200 dark:border-blue-800">
				<div class="flex items-start gap-3">
					<span class="w-8 h-8 bg-blue-500 text-white rounded-full flex items-center justify-center font-bold">2</span>
					<div>
						<p class="font-semibold text-blue-800 dark:text-blue-200">超高速なHMR</p>
						<p class="text-sm text-blue-700 dark:text-blue-300 mt-2">
							<strong>HMR（Hot Module Replacement）</strong> = ファイルを保存すると、
							ページをリロードせずに変更が即座に反映される機能。
						</p>
						<p class="text-sm text-blue-700 dark:text-blue-300 mt-2">
							Viteは変更されたファイルだけを更新するため、
							プロジェクトが大きくなっても更新速度が落ちません。
						</p>
					</div>
				</div>
			</div>

			<!-- esbuild -->
			<div class="p-5 rounded-xl bg-green-50 dark:bg-green-900/20 border border-green-200 dark:border-green-800">
				<div class="flex items-start gap-3">
					<span class="w-8 h-8 bg-green-500 text-white rounded-full flex items-center justify-center font-bold">3</span>
					<div>
						<p class="font-semibold text-green-800 dark:text-green-200">esbuildで高速変換</p>
						<p class="text-sm text-green-700 dark:text-green-300 mt-2">
							TypeScript → JavaScript の変換に「esbuild」を使用。
							Go言語で書かれていて、従来のツールより10〜100倍速いです。
						</p>
					</div>
				</div>
			</div>
		</div>

		<div class="mt-6 p-4 rounded-lg bg-gray-100 dark:bg-gray-800">
			<p class="font-semibold text-gray-800 dark:text-gray-200 mb-3">速度の比較（体感）</p>
			<div class="space-y-2 text-sm">
				<div class="flex items-center gap-3">
					<span class="text-gray-600 dark:text-gray-400 w-24">Webpack:</span>
					<div class="flex-1 bg-red-200 dark:bg-red-900 rounded h-4" style="width: 80%;"></div>
					<span class="text-gray-600 dark:text-gray-400">10〜30秒</span>
				</div>
				<div class="flex items-center gap-3">
					<span class="text-gray-600 dark:text-gray-400 w-24">Vite:</span>
					<div class="flex-1 bg-green-400 dark:bg-green-600 rounded h-4" style="width: 10%;"></div>
					<span class="text-gray-600 dark:text-gray-400">1〜2秒</span>
				</div>
			</div>
			<p class="text-xs text-gray-500 mt-2">※ プロジェクトサイズにより異なります</p>
		</div>
	</section>

	<!-- よく使うコマンド -->
	<section class="mb-12">
		<h2 id="commands" class="text-xl font-bold mb-4">よく使うコマンド</h2>

		<p class="text-gray-700 dark:text-gray-300 mb-4">
			SvelteKitプロジェクトでは、Viteのコマンドがpackage.jsonに設定されています。
		</p>

		<div class="space-y-4">
			<CodePreview
				title="npm run dev"
				description="開発サーバーを起動"
				language="bash"
				code={`npm run dev

# 実行結果:
#   VITE v5.x.x  ready in xxx ms
#
#   ➜  Local:   http://localhost:5173/
#   ➜  Network: http://192.168.x.x:5173/`}
				previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div style="color:#6a9955;">// 開発中はこのコマンドを使う</div><div style="color:#6a9955;">// ファイルを保存すると自動で画面が更新される</div></div>`}
			/>

			<CodePreview
				title="npm run build"
				description="本番用にビルド"
				language="bash"
				code={`npm run build

# 実行結果:
# vite v5.x.x building for production...
# ✓ xxx modules transformed.
# .svelte-kit/output/client/...
# .svelte-kit/output/server/...`}
				previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div style="color:#6a9955;">// デプロイ前に実行</div><div style="color:#6a9955;">// 最適化されたファイルが生成される</div></div>`}
			/>

			<CodePreview
				title="npm run preview"
				description="ビルド結果を確認"
				language="bash"
				code={`npm run preview

# ビルド済みのファイルをローカルで確認できる
# 本番環境と同じ状態でテストしたいときに使う`}
				previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div style="color:#6a9955;">// build後に実行</div><div style="color:#6a9955;">// 本番と同じ状態を確認できる</div></div>`}
			/>
		</div>
	</section>

	<!-- vite.config.js -->
	<section class="mb-12">
		<h2 id="config" class="text-xl font-bold mb-4">設定ファイル</h2>

		<p class="text-gray-700 dark:text-gray-300 mb-4">
			Viteの設定は <code>vite.config.js</code>（または <code>vite.config.ts</code>）に書きます。
			SvelteKitでは基本的に変更する必要はありませんが、カスタマイズも可能です。
		</p>

		<CodePreview
			title="vite.config.ts"
			description="SvelteKitのデフォルト設定"
			language="typescript"
			code={`import { sveltekit } from '@sveltejs/kit/vite';
import { defineConfig } from 'vite';

export default defineConfig({
  plugins: [sveltekit()]
});`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div style="color:#6a9955;">// SvelteKitを使う場合、</div><div style="color:#6a9955;">// これだけでOK！</div></div>`}
		/>

		<div class="mt-6">
			<p class="font-semibold text-gray-800 dark:text-gray-200 mb-3">カスタマイズの例</p>

			<CodePreview
				title="ポート番号を変更"
				description="デフォルトの5173から変更したい場合"
				language="typescript"
				code={`import { sveltekit } from '@sveltejs/kit/vite';
import { defineConfig } from 'vite';

export default defineConfig({
  plugins: [sveltekit()],
  server: {
    port: 3000  // http://localhost:3000 でアクセス
  }
});`}
			/>

			<CodePreview
				title="パスエイリアスを追加"
				description="@components でインポートできるようにする"
				language="typescript"
				code={`import { sveltekit } from '@sveltejs/kit/vite';
import { defineConfig } from 'vite';
import path from 'path';

export default defineConfig({
  plugins: [sveltekit()],
  resolve: {
    alias: {
      '@components': path.resolve('./src/lib/components')
    }
  }
});

// 使い方:
// import Button from '@components/Button.svelte';`}
			/>
		</div>
	</section>

	<!-- よくあるエラー -->
	<section class="mb-12">
		<h2 id="errors" class="text-xl font-bold mb-4">よくあるエラーと対処法</h2>

		<div class="space-y-4">
			<div class="p-4 rounded-lg bg-red-50 dark:bg-red-900/20 border border-red-200 dark:border-red-800">
				<p class="font-semibold text-red-800 dark:text-red-200 mb-2">ポートが既に使われている</p>
				<pre class="text-xs bg-gray-800 text-red-400 p-2 rounded mb-2 overflow-x-auto">Error: listen EADDRINUSE: address already in use :::5173</pre>
				<p class="text-sm text-red-700 dark:text-red-300">
					<strong>原因:</strong> 別のプロセスがポート5173を使用中<br>
					<strong>対処:</strong> 別のターミナルで実行中のサーバーを停止するか、ポート番号を変更
				</p>
			</div>

			<div class="p-4 rounded-lg bg-amber-50 dark:bg-amber-900/20 border border-amber-200 dark:border-amber-800">
				<p class="font-semibold text-amber-800 dark:text-amber-200 mb-2">変更が反映されない</p>
				<p class="text-sm text-amber-700 dark:text-amber-300">
					<strong>対処:</strong><br>
					1. ブラウザのキャッシュをクリア（Ctrl+Shift+R）<br>
					2. 開発サーバーを再起動（Ctrl+C → npm run dev）<br>
					3. node_modules を削除して再インストール
				</p>
				<pre class="text-xs bg-gray-800 text-gray-300 p-2 rounded mt-2 overflow-x-auto">rm -rf node_modules && npm install</pre>
			</div>

			<div class="p-4 rounded-lg bg-blue-50 dark:bg-blue-900/20 border border-blue-200 dark:border-blue-800">
				<p class="font-semibold text-blue-800 dark:text-blue-200 mb-2">ビルドエラー</p>
				<p class="text-sm text-blue-700 dark:text-blue-300">
					<strong>対処:</strong> エラーメッセージをよく読む。多くの場合：<br>
					1. importのパスが間違っている<br>
					2. 存在しないファイルを参照している<br>
					3. TypeScriptの型エラー
				</p>
			</div>
		</div>
	</section>

	<!-- SvelteKitとの関係 -->
	<section class="mb-12">
		<h2 id="with-sveltekit" class="text-xl font-bold mb-4">SvelteKitとViteの関係</h2>

		<div class="p-6 rounded-xl bg-gradient-to-r from-purple-50 to-orange-50 dark:from-purple-900/20 dark:to-orange-900/20 border border-purple-200 dark:border-purple-800 mb-6">
			<div class="space-y-4">
				<div class="flex items-center gap-4">
					<div class="w-24 text-center">
						<div class="text-3xl">📝</div>
						<p class="text-xs text-gray-600 dark:text-gray-400">あなたのコード</p>
					</div>
					<div class="text-2xl text-gray-400">→</div>
					<div class="w-24 text-center">
						<div class="text-3xl text-purple-500">⚡</div>
						<p class="text-xs text-gray-600 dark:text-gray-400">Vite</p>
						<p class="text-xs text-gray-500">変換・最適化</p>
					</div>
					<div class="text-2xl text-gray-400">→</div>
					<div class="w-24 text-center">
						<div class="text-3xl text-orange-500">🔥</div>
						<p class="text-xs text-gray-600 dark:text-gray-400">SvelteKit</p>
						<p class="text-xs text-gray-500">ルーティング等</p>
					</div>
					<div class="text-2xl text-gray-400">→</div>
					<div class="w-24 text-center">
						<div class="text-3xl">🌐</div>
						<p class="text-xs text-gray-600 dark:text-gray-400">ブラウザ</p>
					</div>
				</div>
			</div>
		</div>

		<div class="p-4 rounded-lg bg-gray-50 dark:bg-gray-800">
			<p class="font-semibold text-gray-800 dark:text-gray-200 mb-2">役割分担</p>
			<div class="text-sm text-gray-600 dark:text-gray-400 space-y-2">
				<p><strong>Vite:</strong> ファイルの変換、開発サーバー、ビルドの最適化</p>
				<p><strong>SvelteKit:</strong> ルーティング、SSR、フォームアクション、API</p>
				<p><strong>Svelte:</strong> コンポーネント、リアクティビティ</p>
			</div>
			<p class="text-sm text-gray-600 dark:text-gray-400 mt-3">
				普段の開発では、Viteを意識することはほとんどありません。
				<code>npm run dev</code> を実行すれば、裏側で自動的に動いてくれます。
			</p>
		</div>
	</section>

	<!-- まとめ -->
	<section class="mb-10">
		<h2 id="summary" class="text-xl font-bold mb-4">まとめ</h2>

		<div class="space-y-4">
			<div class="p-4 rounded-lg bg-purple-50 dark:bg-purple-900/20 border border-purple-200 dark:border-purple-800">
				<p class="font-semibold text-purple-800 dark:text-purple-200">Vite = 高速ビルドツール</p>
				<p class="text-sm text-purple-700 dark:text-purple-300">
					開発サーバーの起動やHMRが非常に速い。
				</p>
			</div>
			<div class="p-4 rounded-lg bg-blue-50 dark:bg-blue-900/20 border border-blue-200 dark:border-blue-800">
				<p class="font-semibold text-blue-800 dark:text-blue-200">npm run dev で開発</p>
				<p class="text-sm text-blue-700 dark:text-blue-300">
					ファイル保存時に自動で画面が更新される。
				</p>
			</div>
			<div class="p-4 rounded-lg bg-green-50 dark:bg-green-900/20 border border-green-200 dark:border-green-800">
				<p class="font-semibold text-green-800 dark:text-green-200">npm run build で本番ビルド</p>
				<p class="text-sm text-green-700 dark:text-green-300">
					最適化されたファイルが生成される。
				</p>
			</div>
			<div class="p-4 rounded-lg bg-orange-50 dark:bg-orange-900/20 border border-orange-200 dark:border-orange-800">
				<p class="font-semibold text-orange-800 dark:text-orange-200">普段は意識しなくてOK</p>
				<p class="text-sm text-orange-700 dark:text-orange-300">
					SvelteKitが裏側で自動的にViteを使ってくれる。
				</p>
			</div>
		</div>
	</section>

	<!-- ナビゲーション -->
	<div class="flex justify-between pt-6 border-t border-gray-200 dark:border-gray-700">
		<a href="/sveltekit/svelte" class="inline-flex items-center gap-2 px-4 py-2 rounded-lg border border-gray-300 dark:border-gray-600 hover:bg-gray-100 dark:hover:bg-gray-800 transition-colors">
			<svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
				<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 19l-7-7 7-7" />
			</svg>
			前へ：Svelteとは
		</a>
		<a href="/sveltekit/setup" class="inline-flex items-center gap-2 px-4 py-2 rounded-lg bg-primary-600 text-white hover:bg-primary-700 transition-colors">
			次へ：Tailwind導入
			<svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
				<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 5l7 7-7 7" />
			</svg>
		</a>
	</div>
</article>
