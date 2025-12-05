<script>
	import CodePreview from '$lib/components/CodePreview.svelte';
</script>

<svelte:head>
	<title>SvelteKit 状態管理 | さとまたラボ</title>
</svelte:head>

<article>
	<h1 class="text-3xl font-bold mb-2">状態管理（Runes）</h1>
	<p class="text-lg text-gray-600 dark:text-gray-400 mb-8">
		Svelte 5のリアクティブな状態管理
	</p>

	<!-- Runesとは -->
	<section class="mb-10">
		<h2 id="what-is" class="text-xl font-bold mb-4">Runesとは？</h2>

		<div class="p-6 rounded-xl bg-blue-50 dark:bg-blue-900/20 border border-blue-200 dark:border-blue-800 mb-6">
			<p class="text-blue-800 dark:text-blue-200 mb-4">
				<strong>日常での例え：</strong>スマートホーム
			</p>
			<div class="grid grid-cols-1 md:grid-cols-2 gap-4 text-sm">
				<div class="p-3 bg-white dark:bg-gray-800 rounded-lg">
					<div class="font-semibold text-blue-700 dark:text-blue-300 mb-2">普通の家</div>
					<p class="text-gray-600 dark:text-gray-400">
						電気をつけたい<br>
						→ スイッチまで歩いて押す
					</p>
				</div>
				<div class="p-3 bg-white dark:bg-gray-800 rounded-lg">
					<div class="font-semibold text-blue-700 dark:text-blue-300 mb-2">スマートホーム</div>
					<p class="text-gray-600 dark:text-gray-400">
						「暗くなった」という状態変化<br>
						→ 自動で電気がつく
					</p>
				</div>
			</div>
		</div>

		<div class="p-4 rounded-lg bg-amber-50 dark:bg-amber-900/20 border border-amber-200 dark:border-amber-800 mb-6">
			<p class="font-semibold text-amber-800 dark:text-amber-200">なぜ状態管理が必要？</p>
			<div class="text-sm text-amber-700 dark:text-amber-300 mt-2">
				<p class="mb-2"><strong>状態管理がないと困ること：</strong></p>
				<ul class="list-disc list-inside space-y-1 mb-3">
					<li>変数を変更しても画面が更新されない</li>
					<li>「カートに3個入ってます」の数字が変わらない</li>
					<li>手動でHTMLを書き換える必要がある（大変！）</li>
				</ul>
				<p><strong>状態管理があれば：</strong>データが変わると、画面も自動で更新される！</p>
			</div>
		</div>

		<div class="p-4 rounded-lg bg-green-50 dark:bg-green-900/20 border border-green-200 dark:border-green-800 mb-6">
			<p class="font-semibold text-green-800 dark:text-green-200">Svelte 5の新しい書き方「Runes」</p>
			<div class="text-sm text-green-700 dark:text-green-300 mt-2">
				<p class="mb-2"><strong>Runes（ルーン）</strong>は $ で始まる特別な関数です：</p>
				<ul class="list-disc list-inside space-y-2">
					<li><code class="bg-green-200 dark:bg-green-800 px-1 rounded">$state</code> - 変更を追跡する状態（カウンター、入力値など）</li>
					<li><code class="bg-green-200 dark:bg-green-800 px-1 rounded">$derived</code> - 他の状態から自動計算される値（合計金額など）</li>
					<li><code class="bg-green-200 dark:bg-green-800 px-1 rounded">$effect</code> - 状態が変わったら実行される処理（保存、API呼び出し）</li>
					<li><code class="bg-green-200 dark:bg-green-800 px-1 rounded">$props</code> - 親コンポーネントから受け取る値</li>
				</ul>
			</div>
		</div>

		<div class="p-4 rounded-lg bg-purple-50 dark:bg-purple-900/20 border border-purple-200 dark:border-purple-800 mb-6">
			<p class="font-semibold text-purple-800 dark:text-purple-200 mb-2">用語解説</p>
			<div class="text-sm text-purple-700 dark:text-purple-300 space-y-2">
				<p><strong>状態（State）</strong>：アプリの「今どうなっているか」を表すデータ（例：カートの中身、ログイン状態）</p>
				<p><strong>リアクティブ</strong>：データが変わると、それに関連する表示も自動で変わる仕組み</p>
				<p><strong>コンポーネント</strong>：画面の部品。ボタン、カード、ヘッダーなど再利用できるパーツ</p>
				<p><strong>props（プロップス）</strong>：親から子コンポーネントに渡すデータ（例：ボタンに「送信」という文字を渡す）</p>
			</div>
		</div>
	</section>

	<!-- $state -->
	<section class="mb-10">
		<h2 id="state" class="text-xl font-bold mb-4">$state - 状態の定義</h2>

		<CodePreview
			title="基本的な$state"
			description="変更を追跡する変数"
			language="svelte"
			code={`<script>
  // $stateでリアクティブな状態を作る
  let count = $state(0);
  let name = $state('');
  let items = $state([]);

  function increment() {
    count++;  // 自動で画面が更新される
  }

  function addItem() {
    items.push('新しいアイテム');  // 配列の変更も検知
  }
</script>

<p>カウント: {count}</p>
<button onclick={increment}>+1</button>

<input bind:value={name} />
<p>こんにちは、{name}さん</p>`}
			previewHtml={`<div style="padding:12px;"><p style="margin-bottom:8px;">カウント: 0</p><button style="padding:4px 12px;background:#ff3e00;color:white;border:none;border-radius:4px;margin-bottom:12px;">+1</button><br><input style="padding:4px 8px;border:1px solid #ccc;border-radius:4px;margin-bottom:8px;" placeholder="名前を入力"><p>こんにちは、さん</p></div>`}
		/>

		<div class="mt-4 p-4 rounded-lg bg-gray-50 dark:bg-gray-800/50 border border-gray-200 dark:border-gray-700">
			<p class="font-semibold text-gray-800 dark:text-gray-200 mb-3">コード解説：$stateの動作</p>
			<div class="text-sm text-gray-700 dark:text-gray-300 space-y-3">
				<div>
					<p class="font-medium text-orange-600 dark:text-orange-400 mb-1">① 変数の宣言</p>
					<div class="bg-gray-100 dark:bg-gray-800 p-2 rounded text-xs font-mono mb-2">
						let count = $state(0);
					</div>
					<p><code class="text-orange-500">$state(0)</code> で「0」という初期値を持つ、変更を追跡する変数を作成。普通の変数との違いは、値が変わると<strong>画面も自動で更新される</strong>こと。</p>
				</div>
				<div>
					<p class="font-medium text-orange-600 dark:text-orange-400 mb-1">② 関数での更新</p>
					<div class="bg-gray-100 dark:bg-gray-800 p-2 rounded text-xs font-mono mb-2">
						function increment() {'{'} count++; {'}'}
					</div>
					<p>普通のJavaScriptと同じように <code>count++</code> で値を増やせます。ただし、$stateで作った変数なので、<strong>画面の「カウント: 0」も自動で「カウント: 1」に変わります</strong>。</p>
				</div>
				<div>
					<p class="font-medium text-orange-600 dark:text-orange-400 mb-1">③ bind:value で双方向バインディング</p>
					<div class="bg-gray-100 dark:bg-gray-800 p-2 rounded text-xs font-mono mb-2">
						&lt;input bind:value={'{name}'} /&gt;
					</div>
					<p>入力欄に文字を打つと <code>name</code> 変数が更新され、同時に <code>{'{'}{name}{'}'}</code> で表示している場所も更新されます。</p>
				</div>
				<div class="pt-2 border-t border-gray-200 dark:border-gray-600">
					<p class="font-medium text-green-600 dark:text-green-400 mb-1">処理の流れ</p>
					<p>1. ボタンをクリック → 2. increment()が実行 → 3. count++ でcountが1に → 4. 画面の {'{count}'} が自動で「1」に更新</p>
				</div>
			</div>
		</div>

		<CodePreview
			title="オブジェクトの状態"
			description="ネストしたデータも追跡"
			language="svelte"
			code={`<script>
  let user = $state({
    name: '田中',
    profile: {
      age: 25,
      email: 'tanaka@example.com'
    }
  });

  function updateAge() {
    // ネストしたプロパティも変更を検知！
    user.profile.age++;
  }
</script>

<p>{user.name}さん（{user.profile.age}歳）</p>
<button onclick={updateAge}>年齢+1</button>`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div style="color:#6a9955;">// $stateはディープリアクティブ</div><div style="color:#6a9955;">// ネストしたプロパティも追跡される</div></div>`}
		/>
	</section>

	<!-- $derived -->
	<section class="mb-10">
		<h2 id="derived" class="text-xl font-bold mb-4">$derived - 計算された値</h2>

		<div class="p-4 rounded-lg bg-blue-50 dark:bg-blue-900/20 border border-blue-200 dark:border-blue-800 mb-6">
			<p class="font-semibold text-blue-800 dark:text-blue-200 mb-2">$derivedとは？</p>
			<p class="text-sm text-blue-700 dark:text-blue-300">
				他の状態から<strong>自動的に計算される値</strong>を作ります。<br>
				元の値が変わると、derivedも自動で再計算されます。
			</p>
		</div>

		<CodePreview
			title="基本的な$derived"
			description="他の状態から計算"
			language="svelte"
			code={`<script>
  let items = $state([
    { name: 'りんご', price: 100 },
    { name: 'みかん', price: 80 },
    { name: 'バナナ', price: 120 }
  ]);

  // itemsが変わると自動で再計算
  let total = $derived(
    items.reduce((sum, item) => sum + item.price, 0)
  );

  let count = $derived(items.length);

  function addItem() {
    items.push({ name: '新商品', price: 150 });
    // totalとcountは自動更新！
  }
</script>

<p>商品数: {count}</p>
<p>合計: {total}円</p>`}
			previewHtml={`<div style="padding:12px;"><p>商品数: 3</p><p>合計: 300円</p><p style="color:#6b7280;font-size:12px;margin-top:8px;">itemsが変わると自動更新</p></div>`}
		/>

		<div class="mt-4 p-4 rounded-lg bg-gray-50 dark:bg-gray-800/50 border border-gray-200 dark:border-gray-700">
			<p class="font-semibold text-gray-800 dark:text-gray-200 mb-3">コード解説：$derivedの動作</p>
			<div class="text-sm text-gray-700 dark:text-gray-300 space-y-3">
				<div>
					<p class="font-medium text-cyan-600 dark:text-cyan-400 mb-1">① 元のデータ（$state）</p>
					<div class="bg-gray-100 dark:bg-gray-800 p-2 rounded text-xs font-mono mb-2">
						let items = $state([{'{name: "りんご", price: 100}'}, ...]);
					</div>
					<p>商品データの配列。これが「元」になるデータです。</p>
				</div>
				<div>
					<p class="font-medium text-cyan-600 dark:text-cyan-400 mb-1">② 合計金額の自動計算</p>
					<div class="bg-gray-100 dark:bg-gray-800 p-2 rounded text-xs font-mono mb-2">
						let total = $derived(items.reduce((sum, item) =&gt; sum + item.price, 0));
					</div>
					<ul class="list-disc list-inside space-y-1 ml-2">
						<li><code>reduce()</code>：配列の各要素を足し合わせる JavaScript のメソッド</li>
						<li><code>$derived()</code>：itemsが変わると total も自動で再計算される</li>
						<li>100 + 80 + 120 = <strong>300</strong>円</li>
					</ul>
				</div>
				<div>
					<p class="font-medium text-cyan-600 dark:text-cyan-400 mb-1">③ 商品数の自動計算</p>
					<div class="bg-gray-100 dark:bg-gray-800 p-2 rounded text-xs font-mono mb-2">
						let count = $derived(items.length);
					</div>
					<p>配列の長さ（3）を自動で追跡。商品が追加されると自動で更新されます。</p>
				</div>
				<div class="pt-2 border-t border-gray-200 dark:border-gray-600">
					<p class="font-medium text-green-600 dark:text-green-400 mb-1">addItem()を実行すると...</p>
					<p>1. items に新商品（150円）が追加される → 2. <code>total</code> が自動で 450 に更新 → 3. <code>count</code> が自動で 4 に更新</p>
					<p class="mt-2 text-gray-500">手動で total = ... と書き直す必要がないのが $derived の便利なところ！</p>
				</div>
			</div>
		</div>

		<CodePreview
			title="$derived.by - 複雑な計算"
			description="関数で計算ロジックを書く"
			language="svelte"
			code={`<script>
  let items = $state([...]);
  let filter = $state('all');  // 'all' | 'expensive' | 'cheap'

  // 複雑なロジックは $derived.by を使う
  let filteredItems = $derived.by(() => {
    if (filter === 'all') return items;

    if (filter === 'expensive') {
      return items.filter(item => item.price >= 100);
    }

    return items.filter(item => item.price < 100);
  });

  let message = $derived.by(() => {
    const count = filteredItems.length;
    if (count === 0) return '商品がありません';
    return \`\${count}件の商品があります\`;
  });
</script>

<select bind:value={filter}>
  <option value="all">すべて</option>
  <option value="expensive">100円以上</option>
  <option value="cheap">100円未満</option>
</select>

<p>{message}</p>`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div><span style="color:#dcdcaa;">$derived</span>(単純な式)</div><div><span style="color:#dcdcaa;">$derived.by</span>(() =&gt; 複雑なロジック)</div></div>`}
		/>
	</section>

	<!-- $effect -->
	<section class="mb-10">
		<h2 id="effect" class="text-xl font-bold mb-4">$effect - 副作用</h2>

		<div class="p-4 rounded-lg bg-blue-50 dark:bg-blue-900/20 border border-blue-200 dark:border-blue-800 mb-6">
			<p class="font-semibold text-blue-800 dark:text-blue-200 mb-2">$effectとは？</p>
			<p class="text-sm text-blue-700 dark:text-blue-300">
				状態が変わったときに<strong>自動で実行される処理</strong>を定義します。<br>
				ログ出力、ローカルストレージ保存、外部APIの呼び出しなどに使います。
			</p>
		</div>

		<CodePreview
			title="基本的な$effect"
			description="状態変化時に実行"
			language="svelte"
			code={`<script>
  let searchQuery = $state('');
  let results = $state([]);

  // searchQueryが変わるたびに実行
  $effect(() => {
    console.log('検索クエリ:', searchQuery);

    // 空でなければAPIを呼ぶ
    if (searchQuery.length > 2) {
      fetch(\`/api/search?q=\${searchQuery}\`)
        .then(r => r.json())
        .then(data => {
          results = data;
        });
    }
  });
</script>

<input bind:value={searchQuery} placeholder="検索..." />`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div style="color:#6a9955;">// $effect内で使った$stateが変わると</div><div style="color:#6a9955;">// 自動的に再実行される</div></div>`}
		/>

		<CodePreview
			title="クリーンアップ処理"
			description="effectの後片付け"
			language="svelte"
			code={`<script>
  let isConnected = $state(false);

  $effect(() => {
    // WebSocket接続
    const ws = new WebSocket('wss://example.com');

    ws.onopen = () => {
      isConnected = true;
    };

    ws.onclose = () => {
      isConnected = false;
    };

    // クリーンアップ関数を返す
    return () => {
      ws.close();  // コンポーネント破棄時に実行
    };
  });
</script>

<p>接続状態: {isConnected ? '接続中' : '切断'}</p>`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div style="color:#6a9955;">// return () =&gt; { ... }</div><div style="color:#6a9955;">// コンポーネント破棄時や</div><div style="color:#6a9955;">// 次のeffect実行前に呼ばれる</div></div>`}
		/>

		<CodePreview
			title="ローカルストレージとの連携"
			description="よくある使用例"
			language="svelte"
			code={`<script>
  // 初期値はローカルストレージから
  let theme = $state(
    localStorage.getItem('theme') || 'light'
  );

  // themeが変わるたびに保存
  $effect(() => {
    localStorage.setItem('theme', theme);
    document.documentElement.classList.toggle('dark', theme === 'dark');
  });

  function toggleTheme() {
    theme = theme === 'light' ? 'dark' : 'light';
  }
</script>

<button onclick={toggleTheme}>
  {theme === 'light' ? '🌙' : '☀️'} テーマ切替
</button>`}
			previewHtml={`<button style="padding:8px 16px;background:#374151;color:white;border:none;border-radius:8px;font-size:16px;">🌙 テーマ切替</button>`}
		/>
	</section>

	<!-- $props -->
	<section class="mb-10">
		<h2 id="props" class="text-xl font-bold mb-4">$props - プロパティ</h2>

		<CodePreview
			title="コンポーネントのprops"
			description="親から値を受け取る"
			language="svelte"
			code={`<!-- Button.svelte -->
<script>
  // propsを受け取る
  let {
    label,
    variant = 'primary',  // デフォルト値
    disabled = false,
    onclick  // イベントハンドラ
  } = $props();
</script>

<button
  class="btn btn-{variant}"
  {disabled}
  {onclick}
>
  {label}
</button>

<!-- 親コンポーネントから使う -->
<Button
  label="送信"
  variant="primary"
  onclick={() => console.log('クリック')}
/>`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div><span style="color:#c586c0;">let</span> &#123; prop1, prop2 &#125; = <span style="color:#dcdcaa;">$props</span>()</div><div style="color:#6a9955;">// 分割代入でpropsを受け取る</div></div>`}
		/>

		<CodePreview
			title="TypeScriptとの組み合わせ"
			description="型安全なprops"
			language="svelte"
			code={`<script lang="ts">
  interface Props {
    title: string;
    count: number;
    items?: string[];  // オプショナル
    onSave: (data: string) => void;
  }

  let {
    title,
    count,
    items = [],
    onSave
  }: Props = $props();
</script>

<h2>{title}</h2>
<p>カウント: {count}</p>
<ul>
  {#each items as item}
    <li>{item}</li>
  {/each}
</ul>`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div style="color:#569cd6;">interface</span> Props &#123;...&#125;</div><div style="color:#6a9955;">// TypeScriptで型定義</div></div>`}
		/>
	</section>

	<!-- グローバル状態 -->
	<section class="mb-10">
		<h2 id="global" class="text-xl font-bold mb-4">グローバル状態</h2>

		<div class="p-4 rounded-lg bg-amber-50 dark:bg-amber-900/20 border border-amber-200 dark:border-amber-800 mb-6">
			<p class="font-semibold text-amber-800 dark:text-amber-200">コンポーネント間で状態を共有するには？</p>
			<p class="text-sm text-amber-700 dark:text-amber-300 mt-2">
				別ファイルで状態を定義し、importして使います。<br>
				Svelte 5では.svelte.tsファイルでrunesが使えます。
			</p>
		</div>

		<CodePreview
			title="グローバルストア"
			description=".svelte.tsファイルで状態管理"
			language="typescript"
			code={`// src/lib/stores/counter.svelte.ts
let count = $state(0);

export function getCount() {
  return count;
}

export function increment() {
  count++;
}

export function decrement() {
  count--;
}

// ----- 使う側 -----
// src/routes/+page.svelte
<script>
  import { getCount, increment, decrement } from '$lib/stores/counter.svelte';

  // リアクティブに値を取得
  let count = $derived(getCount());
</script>

<p>カウント: {count}</p>
<button onclick={increment}>+</button>
<button onclick={decrement}>-</button>`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div style="color:#ce9178;">counter.svelte.ts</div><div style="color:#6a9955;">// .svelte.ts でrunesが使える</div><div style="color:#6a9955;">// 複数コンポーネントで共有</div></div>`}
		/>

		<CodePreview
			title="ユーザー状態の例"
			description="認証状態の管理"
			language="typescript"
			code={`// src/lib/stores/auth.svelte.ts
interface User {
  id: number;
  name: string;
  email: string;
}

let user = $state<User | null>(null);

export function getUser() {
  return user;
}

export function isLoggedIn() {
  return user !== null;
}

export function login(userData: User) {
  user = userData;
}

export function logout() {
  user = null;
}

// ----- 使う側 -----
<script>
  import { getUser, isLoggedIn, logout } from '$lib/stores/auth.svelte';

  let user = $derived(getUser());
  let loggedIn = $derived(isLoggedIn());
</script>

{#if loggedIn}
  <p>ようこそ、{user.name}さん</p>
  <button onclick={logout}>ログアウト</button>
{:else}
  <a href="/login">ログイン</a>
{/if}`}
			previewHtml={`<div style="padding:12px;"><p>ようこそ、田中さん</p><button style="padding:4px 12px;background:#ef4444;color:white;border:none;border-radius:4px;">ログアウト</button></div>`}
		/>
	</section>

	<!-- ナビゲーション -->
	<div class="flex justify-between pt-6 border-t border-gray-200 dark:border-gray-700">
		<a href="/sveltekit/hooks" class="inline-flex items-center gap-2 px-4 py-2 rounded-lg border border-gray-300 dark:border-gray-600 hover:bg-gray-100 dark:hover:bg-gray-800 transition-colors">
			<svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
				<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 19l-7-7 7-7" />
			</svg>
			前へ：Hooks
		</a>
		<a href="/sveltekit/layouts" class="inline-flex items-center gap-2 px-4 py-2 rounded-lg bg-primary-600 text-white hover:bg-primary-700 transition-colors">
			次へ：レイアウト
			<svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
				<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 5l7 7-7 7" />
			</svg>
		</a>
	</div>
</article>
