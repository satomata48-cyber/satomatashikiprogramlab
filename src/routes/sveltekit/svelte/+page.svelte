<script>
	import CodePreview from '$lib/components/CodePreview.svelte';
</script>

<svelte:head>
	<title>Svelteとは | さとまたラボ</title>
</svelte:head>

<article>
	<h1 class="text-3xl font-bold mb-2">Svelteとは</h1>
	<p class="text-lg text-gray-600 dark:text-gray-400 mb-8">
		SvelteKitの基盤となるUIフレームワークを理解しよう
	</p>

	<!-- Svelteとは -->
	<section class="mb-12">
		<h2 id="what-is-svelte" class="text-xl font-bold mb-4">Svelteって何？</h2>

		<div class="p-6 rounded-xl bg-gradient-to-r from-orange-50 to-red-50 dark:from-orange-900/20 dark:to-red-900/20 border border-orange-200 dark:border-orange-800 mb-6">
			<p class="text-lg text-orange-800 dark:text-orange-200 mb-4">
				<strong>Svelte（スベルト）</strong> = ウェブサイトの見た目を作るためのツール
			</p>
			<p class="text-sm text-orange-700 dark:text-orange-300">
				ReactやVueと同じ「UIフレームワーク」の一種です。
				ボタンやフォーム、リストなど、画面に表示するパーツ（コンポーネント）を作るのに使います。
			</p>
		</div>

		<div class="p-4 rounded-lg bg-blue-50 dark:bg-blue-900/20 border border-blue-200 dark:border-blue-800 mb-6">
			<p class="font-semibold text-blue-800 dark:text-blue-200 mb-2">名前の由来</p>
			<p class="text-sm text-blue-700 dark:text-blue-300">
				「Svelte」は英語で「すらりとした、スマートな」という意味。
				その名の通り、シンプルで軽量なのが特徴です。
			</p>
		</div>
	</section>

	<!-- 他のフレームワークとの違い -->
	<section class="mb-12">
		<h2 id="difference" class="text-xl font-bold mb-4">React・Vueとの違い</h2>

		<p class="text-gray-700 dark:text-gray-300 mb-4">
			Svelteの最大の特徴は「<strong>コンパイラ</strong>」であることです。
		</p>

		<div class="grid md:grid-cols-2 gap-4 mb-6">
			<div class="p-4 rounded-lg bg-gray-50 dark:bg-gray-800 border border-gray-200 dark:border-gray-700">
				<p class="font-semibold text-gray-800 dark:text-gray-200 mb-3">React / Vue の場合</p>
				<div class="text-sm text-gray-600 dark:text-gray-400 space-y-2">
					<p>1. あなたがコードを書く</p>
					<p>2. React/Vueの「ランタイム」も一緒に配信</p>
					<p>3. ブラウザでランタイムが動いて画面を更新</p>
				</div>
				<div class="mt-3 p-2 bg-red-100 dark:bg-red-900/30 rounded text-xs text-red-700 dark:text-red-300">
					ランタイム = フレームワーク本体のコード（数十KB〜）
				</div>
			</div>
			<div class="p-4 rounded-lg bg-orange-50 dark:bg-orange-900/20 border border-orange-200 dark:border-orange-800">
				<p class="font-semibold text-orange-800 dark:text-orange-200 mb-3">Svelte の場合</p>
				<div class="text-sm text-orange-700 dark:text-orange-300 space-y-2">
					<p>1. あなたがコードを書く</p>
					<p>2. ビルド時に最適化されたJSに変換</p>
					<p>3. ブラウザには変換後のコードだけ配信</p>
				</div>
				<div class="mt-3 p-2 bg-green-100 dark:bg-green-900/30 rounded text-xs text-green-700 dark:text-green-300">
					ランタイム不要 = より軽量で高速！
				</div>
			</div>
		</div>

		<div class="p-4 rounded-lg bg-amber-50 dark:bg-amber-900/20 border border-amber-200 dark:border-amber-800">
			<p class="font-semibold text-amber-800 dark:text-amber-200 mb-2">コンパイラって何？</p>
			<p class="text-sm text-amber-700 dark:text-amber-300">
				「翻訳機」のようなものです。
				あなたが書いたSvelteコードを、ブラウザが理解できる普通のJavaScriptに変換します。
				この変換はビルド時（<code class="bg-amber-200 dark:bg-amber-700 px-1 rounded">npm run build</code>）に行われます。
			</p>
		</div>
	</section>

	<!-- Svelteの利点 -->
	<section class="mb-12">
		<h2 id="benefits" class="text-xl font-bold mb-4">Svelteを使うメリット</h2>

		<div class="space-y-4">
			<div class="p-4 rounded-lg bg-green-50 dark:bg-green-900/20 border border-green-200 dark:border-green-800">
				<div class="flex items-start gap-3">
					<span class="text-2xl">1</span>
					<div>
						<p class="font-semibold text-green-800 dark:text-green-200">コードが少なくて済む</p>
						<p class="text-sm text-green-700 dark:text-green-300 mt-1">
							同じ機能をReactで書くと30行、Svelteなら15行で済むことも。
							書くコードが少ない = バグも減る！
						</p>
					</div>
				</div>
			</div>

			<div class="p-4 rounded-lg bg-blue-50 dark:bg-blue-900/20 border border-blue-200 dark:border-blue-800">
				<div class="flex items-start gap-3">
					<span class="text-2xl">2</span>
					<div>
						<p class="font-semibold text-blue-800 dark:text-blue-200">学習コストが低い</p>
						<p class="text-sm text-blue-700 dark:text-blue-300 mt-1">
							HTML・CSS・JavaScriptを知っていれば、すぐに始められます。
							特別な書き方を覚える必要が少ないです。
						</p>
					</div>
				</div>
			</div>

			<div class="p-4 rounded-lg bg-purple-50 dark:bg-purple-900/20 border border-purple-200 dark:border-purple-800">
				<div class="flex items-start gap-3">
					<span class="text-2xl">3</span>
					<div>
						<p class="font-semibold text-purple-800 dark:text-purple-200">高速で軽量</p>
						<p class="text-sm text-purple-700 dark:text-purple-300 mt-1">
							ランタイムがないため、配信するファイルサイズが小さい。
							ページの読み込みが速くなります。
						</p>
					</div>
				</div>
			</div>
		</div>
	</section>

	<!-- 基本的な書き方 -->
	<section class="mb-12">
		<h2 id="syntax" class="text-xl font-bold mb-4">Svelteの基本的な書き方</h2>

		<p class="text-gray-700 dark:text-gray-300 mb-4">
			Svelteのファイルは <code>.svelte</code> という拡張子を使います。
			1つのファイルに「JavaScript」「HTML」「CSS」をまとめて書きます。
		</p>

		<CodePreview
			title="Svelteファイルの構造"
			description="3つのセクションで構成される"
			language="svelte"
			code={`<script>
  // ここにJavaScriptを書く
  let name = '太郎';
  let count = 0;
</script>

<!-- ここにHTMLを書く -->
<h1>こんにちは、{name}さん！</h1>
<p>カウント: {count}</p>
<button onclick={() => count++}>+1</button>

<style>
  /* ここにCSSを書く */
  h1 {
    color: blue;
  }
</style>`}
			previewHtml={`<div style="font-family:sans-serif;"><div style="color:blue;font-size:1.5em;font-weight:bold;">こんにちは、太郎さん！</div><p>カウント: 0</p><button style="padding:4px 12px;cursor:pointer;">+1</button></div>`}
		/>

		<div class="mt-6 space-y-4">
			<div class="p-4 rounded-lg bg-gray-50 dark:bg-gray-800">
				<p class="font-semibold text-gray-800 dark:text-gray-200 mb-2">{`{変数}`} の書き方</p>
				<p class="text-sm text-gray-600 dark:text-gray-400">
					HTMLの中で <code>{`{name}`}</code> のように波括弧で囲むと、JavaScriptの変数の値が表示されます。
					変数が変わると、自動的に画面も更新されます。
				</p>
			</div>

			<div class="p-4 rounded-lg bg-gray-50 dark:bg-gray-800">
				<p class="font-semibold text-gray-800 dark:text-gray-200 mb-2">CSSは自動でスコープ化</p>
				<p class="text-sm text-gray-600 dark:text-gray-400">
					<code>&lt;style&gt;</code> に書いたCSSは、そのコンポーネント内だけに適用されます。
					他のコンポーネントに影響しないので、クラス名の衝突を心配する必要がありません。
				</p>
			</div>
		</div>
	</section>

	<!-- リアクティビティ -->
	<section class="mb-12">
		<h2 id="reactivity" class="text-xl font-bold mb-4">リアクティビティ（自動更新）</h2>

		<p class="text-gray-700 dark:text-gray-300 mb-4">
			Svelteの最大の魅力は「<strong>リアクティビティ</strong>」です。
			変数の値が変わると、画面が自動で更新されます。
		</p>

		<CodePreview
			title="変数を変えると画面が更新される"
			description="letで宣言した変数は自動でリアクティブ"
			language="svelte"
			code={`<script>
  let count = 0;

  function increment() {
    count = count + 1;  // これだけで画面が更新される！
  }
</script>

<p>カウント: {count}</p>
<button onclick={increment}>増やす</button>`}
			previewHtml={`<div style="font-family:sans-serif;"><p>カウント: <strong>0</strong></p><button style="padding:4px 12px;background:#3b82f6;color:white;border:none;border-radius:4px;cursor:pointer;">増やす</button><p style="font-size:12px;color:#666;margin-top:8px;">ボタンを押すとcountが増え、画面の数字も変わる</p></div>`}
		/>

		<div class="mt-6 p-4 rounded-lg bg-orange-50 dark:bg-orange-900/20 border border-orange-200 dark:border-orange-800">
			<p class="font-semibold text-orange-800 dark:text-orange-200 mb-2">Reactとの違い</p>
			<div class="text-sm text-orange-700 dark:text-orange-300 space-y-2">
				<p><strong>React:</strong> <code>const [count, setCount] = useState(0)</code> → <code>setCount(count + 1)</code></p>
				<p><strong>Svelte:</strong> <code>let count = 0</code> → <code>count = count + 1</code></p>
				<p class="mt-2">Svelteの方がシンプルで直感的ですね！</p>
			</div>
		</div>
	</section>

	<!-- $state と $derived -->
	<section class="mb-12">
		<h2 id="runes" class="text-xl font-bold mb-4">Svelte 5の新機能: Runes</h2>

		<div class="p-4 rounded-lg bg-purple-50 dark:bg-purple-900/20 border border-purple-200 dark:border-purple-800 mb-6">
			<p class="font-semibold text-purple-800 dark:text-purple-200 mb-2">Runes（ルーン）とは？</p>
			<p class="text-sm text-purple-700 dark:text-purple-300">
				Svelte 5から導入された新しい書き方です。
				<code>$state</code>、<code>$derived</code>、<code>$effect</code> などがあります。
				より明示的で、大規模なアプリでも管理しやすくなりました。
			</p>
		</div>

		<CodePreview
			title="$state - 状態を宣言する"
			description="変更を追跡したい変数に使う"
			language="svelte"
			code={`<script>
  // $state() で状態を宣言
  let count = $state(0);
  let name = $state('太郎');
</script>

<p>{name}さんのカウント: {count}</p>
<button onclick={() => count++}>+1</button>`}
			previewHtml={`<div style="font-family:sans-serif;"><p>太郎さんのカウント: <strong>0</strong></p><button style="padding:4px 12px;background:#8b5cf6;color:white;border:none;border-radius:4px;cursor:pointer;">+1</button></div>`}
		/>

		<CodePreview
			title="$derived - 計算値を作る"
			description="他の値から自動計算される値"
			language="svelte"
			code={`<script>
  let price = $state(1000);
  let quantity = $state(3);

  // priceかquantityが変わると自動で再計算される
  let total = $derived(price * quantity);
  let tax = $derived(total * 0.1);
  let totalWithTax = $derived(total + tax);
</script>

<p>単価: {price}円 × 数量: {quantity}</p>
<p>小計: {total}円</p>
<p>税込: {totalWithTax}円</p>`}
			previewHtml={`<div style="font-family:sans-serif;"><p>単価: 1000円 × 数量: 3</p><p>小計: <strong>3000</strong>円</p><p>税込: <strong>3300</strong>円</p><p style="font-size:12px;color:#666;margin-top:8px;">priceやquantityを変えると、total等も自動で更新される</p></div>`}
		/>

		<div class="mt-6 p-4 rounded-lg bg-amber-50 dark:bg-amber-900/20 border border-amber-200 dark:border-amber-800">
			<p class="font-semibold text-amber-800 dark:text-amber-200 mb-2">$state と let の違い</p>
			<p class="text-sm text-amber-700 dark:text-amber-300">
				<strong>let count = 0</strong> → 従来の書き方（Svelte 4以前）<br>
				<strong>let count = $state(0)</strong> → 新しい書き方（Svelte 5）<br><br>
				どちらも動きますが、新しいプロジェクトでは <code>$state</code> を使うことが推奨されています。
			</p>
		</div>
	</section>

	<!-- コンポーネント -->
	<section class="mb-12">
		<h2 id="components" class="text-xl font-bold mb-4">コンポーネント</h2>

		<p class="text-gray-700 dark:text-gray-300 mb-4">
			画面のパーツを「コンポーネント」として分割できます。
			再利用可能で、コードの整理がしやすくなります。
		</p>

		<CodePreview
			title="コンポーネントを作る"
			description="Button.svelte"
			language="svelte"
			code={`<!-- src/lib/components/Button.svelte -->
<script>
  let { text, onclick } = $props();
</script>

<button onclick={onclick} class="btn">
  {text}
</button>

<style>
  .btn {
    padding: 8px 16px;
    background: #3b82f6;
    color: white;
    border: none;
    border-radius: 4px;
    cursor: pointer;
  }
  .btn:hover {
    background: #2563eb;
  }
</style>`}
			previewHtml={`<button style="padding:8px 16px;background:#3b82f6;color:white;border:none;border-radius:4px;cursor:pointer;">ボタン</button>`}
		/>

		<CodePreview
			title="コンポーネントを使う"
			description="+page.svelte"
			language="svelte"
			code={`<script>
  import Button from '$lib/components/Button.svelte';

  function handleClick() {
    alert('クリックされました！');
  }
</script>

<h1>マイページ</h1>
<Button text="送信する" onclick={handleClick} />
<Button text="キャンセル" onclick={() => history.back()} />`}
			previewHtml={`<div style="font-family:sans-serif;"><h1 style="font-size:1.5em;margin-bottom:12px;">マイページ</h1><button style="padding:8px 16px;background:#3b82f6;color:white;border:none;border-radius:4px;cursor:pointer;margin-right:8px;">送信する</button><button style="padding:8px 16px;background:#3b82f6;color:white;border:none;border-radius:4px;cursor:pointer;">キャンセル</button></div>`}
		/>

		<div class="mt-6 p-4 rounded-lg bg-gray-50 dark:bg-gray-800">
			<p class="font-semibold text-gray-800 dark:text-gray-200 mb-2">$props() って何？</p>
			<p class="text-sm text-gray-600 dark:text-gray-400">
				親コンポーネントから渡されたデータを受け取る仕組みです。
				上の例では、<code>text</code> と <code>onclick</code> を受け取っています。
			</p>
		</div>
	</section>

	<!-- SvelteとSvelteKitの関係 -->
	<section class="mb-12">
		<h2 id="svelte-vs-sveltekit" class="text-xl font-bold mb-4">SvelteとSvelteKitの関係</h2>

		<div class="p-6 rounded-xl bg-gradient-to-r from-orange-50 to-red-50 dark:from-orange-900/20 dark:to-red-900/20 border border-orange-200 dark:border-orange-800 mb-6">
			<div class="grid md:grid-cols-2 gap-4">
				<div>
					<p class="font-bold text-orange-800 dark:text-orange-200 mb-2">Svelte</p>
					<p class="text-sm text-orange-700 dark:text-orange-300">
						UIを作るためのツール<br>
						（コンポーネント、リアクティビティ）
					</p>
				</div>
				<div>
					<p class="font-bold text-red-800 dark:text-red-200 mb-2">SvelteKit</p>
					<p class="text-sm text-red-700 dark:text-red-300">
						Svelteを使ってアプリを作るための枠組み<br>
						（ルーティング、SSR、API、デプロイ）
					</p>
				</div>
			</div>
		</div>

		<div class="p-4 rounded-lg bg-blue-50 dark:bg-blue-900/20 border border-blue-200 dark:border-blue-800">
			<p class="font-semibold text-blue-800 dark:text-blue-200 mb-2">例えると...</p>
			<p class="text-sm text-blue-700 dark:text-blue-300">
				<strong>Svelte</strong> = レゴブロック（パーツを作る道具）<br>
				<strong>SvelteKit</strong> = レゴの設計図と組み立てガイド（パーツを組み合わせてアプリにする）<br><br>
				SvelteKitを使えば、Svelteで作ったコンポーネントを簡単にウェブアプリにできます。
			</p>
		</div>
	</section>

	<!-- まとめ -->
	<section class="mb-10">
		<h2 id="summary" class="text-xl font-bold mb-4">まとめ</h2>

		<div class="space-y-4">
			<div class="p-4 rounded-lg bg-orange-50 dark:bg-orange-900/20 border border-orange-200 dark:border-orange-800">
				<p class="font-semibold text-orange-800 dark:text-orange-200">Svelte = コンパイラ型UIフレームワーク</p>
				<p class="text-sm text-orange-700 dark:text-orange-300">
					ビルド時に最適化されるため、軽量で高速。
				</p>
			</div>
			<div class="p-4 rounded-lg bg-blue-50 dark:bg-blue-900/20 border border-blue-200 dark:border-blue-800">
				<p class="font-semibold text-blue-800 dark:text-blue-200">コードが少なくて済む</p>
				<p class="text-sm text-blue-700 dark:text-blue-300">
					ReactやVueより記述量が少なく、学習コストも低い。
				</p>
			</div>
			<div class="p-4 rounded-lg bg-green-50 dark:bg-green-900/20 border border-green-200 dark:border-green-800">
				<p class="font-semibold text-green-800 dark:text-green-200">$state、$derived でリアクティビティ</p>
				<p class="text-sm text-green-700 dark:text-green-300">
					変数が変わると画面が自動更新される。
				</p>
			</div>
			<div class="p-4 rounded-lg bg-purple-50 dark:bg-purple-900/20 border border-purple-200 dark:border-purple-800">
				<p class="font-semibold text-purple-800 dark:text-purple-200">SvelteKitと組み合わせて使う</p>
				<p class="text-sm text-purple-700 dark:text-purple-300">
					Svelteで画面を作り、SvelteKitでアプリにする。
				</p>
			</div>
		</div>
	</section>

	<!-- ナビゲーション -->
	<div class="flex justify-between pt-6 border-t border-gray-200 dark:border-gray-700">
		<a href="/sveltekit/intro" class="inline-flex items-center gap-2 px-4 py-2 rounded-lg border border-gray-300 dark:border-gray-600 hover:bg-gray-100 dark:hover:bg-gray-800 transition-colors">
			<svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
				<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 19l-7-7 7-7" />
			</svg>
			前へ：はじめに
		</a>
		<a href="/sveltekit/vite" class="inline-flex items-center gap-2 px-4 py-2 rounded-lg bg-primary-600 text-white hover:bg-primary-700 transition-colors">
			次へ：Viteとは
			<svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
				<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 5l7 7-7 7" />
			</svg>
		</a>
	</div>
</article>
