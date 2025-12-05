<script>
	import CodePreview from '$lib/components/CodePreview.svelte';
	import FeatureCard from '$lib/components/FeatureCard.svelte';

	const features = [
		{ icon: '🔒', title: '型安全', description: 'コンパイル時にエラーを検出', tag: '特徴' },
		{ icon: '📝', title: '型推論', description: '自動で型を推測してくれる', tag: '便利' },
		{ icon: '🔧', title: 'IDE補完', description: 'コード補完が強力になる', tag: '便利' },
		{ icon: '📚', title: 'ドキュメント', description: '型がコードの説明書になる', tag: '特徴' },
		{ icon: '🐛', title: 'バグ防止', description: '実行前にミスを発見', tag: '重要' },
		{ icon: '🔄', title: 'リファクタリング', description: '安全にコード変更できる', tag: '重要' }
	];
</script>

<svelte:head>
	<title>TypeScript はじめに | さとまたラボ</title>
</svelte:head>

<article>
	<h1 class="text-3xl font-bold mb-2">TypeScript</h1>
	<p class="text-lg text-gray-600 dark:text-gray-400 mb-8">
		JavaScriptに「型」を追加した言語
	</p>

	<!-- TypeScriptとは -->
	<section class="mb-10">
		<h2 id="what-is" class="text-xl font-bold mb-4">TypeScriptとは？</h2>

		<div class="p-6 rounded-xl bg-blue-50 dark:bg-blue-900/20 border border-blue-200 dark:border-blue-800 mb-6">
			<p class="text-blue-800 dark:text-blue-200 mb-4">
				<strong>日常での例え：</strong>ラベル付きの収納ボックス
			</p>
			<div class="grid grid-cols-1 md:grid-cols-2 gap-4 text-sm">
				<div class="p-3 bg-white dark:bg-gray-800 rounded-lg">
					<div class="font-semibold text-blue-700 dark:text-blue-300 mb-2">JavaScript = ラベルなし</div>
					<p class="text-gray-600 dark:text-gray-400">
						箱に何でも入れられる<br>
						→ 開けてみるまで中身が分からない
					</p>
				</div>
				<div class="p-3 bg-white dark:bg-gray-800 rounded-lg">
					<div class="font-semibold text-blue-700 dark:text-blue-300 mb-2">TypeScript = ラベル付き</div>
					<p class="text-gray-600 dark:text-gray-400">
						「おもちゃ用」「服用」とラベルがある<br>
						→ 間違ったものを入れようとすると警告
					</p>
				</div>
			</div>
		</div>

		<div class="p-4 rounded-lg bg-amber-50 dark:bg-amber-900/20 border border-amber-200 dark:border-amber-800 mb-6">
			<p class="font-semibold text-amber-800 dark:text-amber-200">なぜTypeScriptが必要？</p>
			<div class="text-sm text-amber-700 dark:text-amber-300 mt-2">
				<p class="mb-2"><strong>JavaScriptだけだと起きる問題：</strong></p>
				<ul class="list-disc list-inside space-y-1 mb-3">
					<li>数字を期待している関数に文字列を渡してしまう</li>
					<li>存在しないプロパティにアクセスしてエラー</li>
					<li>タイプミスに実行するまで気づけない</li>
				</ul>
				<p><strong>TypeScriptなら：</strong>コードを書いている時点でエラーを教えてくれる！</p>
			</div>
		</div>

		<div class="p-4 rounded-lg bg-gray-100 dark:bg-gray-800 mb-6">
			<p class="font-semibold text-gray-800 dark:text-gray-200 mb-2">TypeScriptとJavaScriptの関係</p>
			<div class="text-sm text-gray-700 dark:text-gray-300">
				<p><strong>TypeScript = JavaScript + 型</strong></p>
				<p class="mt-2">TypeScriptは最終的にJavaScriptに変換（コンパイル）されて実行されます。</p>
				<p>つまり、JavaScriptの知識はそのまま使えます！</p>
			</div>
		</div>
	</section>

	<!-- できること一覧 -->
	<section class="mb-10">
		<h2 id="features" class="text-xl font-bold mb-4">TypeScriptでできること</h2>
		<div class="grid grid-cols-1 md:grid-cols-2 gap-3">
			{#each features as feature}
				<FeatureCard {...feature} />
			{/each}
		</div>
	</section>

	<!-- コード例 -->
	<section class="mb-10">
		<h2 id="examples" class="text-xl font-bold mb-4">コード例</h2>

		<CodePreview
			title="基本的な型指定"
			description="変数に型を付ける"
			language="typescript"
			code={`// 型を指定
let name: string = "田中";
let age: number = 25;
let isStudent: boolean = true;

// 型が違うとエラー！
name = 123;  // ❌ エラー: string型にnumberは代入できない
age = "二十五";  // ❌ エラー: number型にstringは代入できない

// 型推論（自動で型を推測）
let city = "東京";  // 自動的にstring型
let score = 100;    // 自動的にnumber型`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div style="color:#6a9955;">// TypeScriptは型が違うと</div><div style="color:#6a9955;">// 実行前に教えてくれる</div><div style="color:#f14c4c;margin-top:8px;">❌ name = 123; // エラー！</div></div>`}
		/>

		<!-- JS比較：基本的な型 -->
		<div class="mt-4 mb-8 p-4 rounded-lg bg-yellow-50 dark:bg-yellow-900/20 border border-yellow-200 dark:border-yellow-800">
			<p class="font-semibold text-yellow-800 dark:text-yellow-200 mb-3">JavaScriptだと？</p>
			<div class="grid md:grid-cols-2 gap-4">
				<div>
					<p class="text-sm font-medium text-yellow-700 dark:text-yellow-300 mb-2">JavaScript（型チェックなし）</p>
					<pre class="text-xs bg-gray-900 text-gray-100 p-3 rounded overflow-x-auto"><code>let name = "田中";
let age = 25;

// 何でも代入できてしまう
name = 123;      // ⚠️ エラーにならない
age = "二十五";   // ⚠️ エラーにならない

// 実行時に予期せぬ動作...
console.log(name.toUpperCase());
// → TypeError: name.toUpperCase is not a function
// （数値には toUpperCase がない！）</code></pre>
				</div>
				<div>
					<p class="text-sm font-medium text-blue-700 dark:text-blue-300 mb-2">TypeScript（型チェックあり）</p>
					<pre class="text-xs bg-gray-900 text-gray-100 p-3 rounded overflow-x-auto"><code>let name: string = "田中";
let age: number = 25;

// 型が違うとコンパイル時にエラー
name = 123;      // ❌ コンパイルエラー！
age = "二十五";   // ❌ コンパイルエラー！

// 実行前に問題を発見できる
// → バグを未然に防げる！</code></pre>
				</div>
			</div>
			<p class="text-xs text-yellow-600 dark:text-yellow-400 mt-3">
				JSは「動的型付け」なので実行時まで型エラーに気づけない。TSは「静的型付け」なのでコードを書いている時点でエラーを教えてくれる。
			</p>
		</div>

		<CodePreview
			title="配列とオブジェクトの型"
			description="複合的なデータ構造の型"
			language="typescript"
			code={`// 配列の型
let numbers: number[] = [1, 2, 3, 4, 5];
let names: string[] = ["田中", "鈴木", "佐藤"];

// オブジェクトの型
let user: {
  name: string;
  age: number;
  email: string;
} = {
  name: "田中太郎",
  age: 25,
  email: "tanaka@example.com"
};

// 存在しないプロパティはエラー
user.address;  // ❌ エラー: 'address'は存在しない`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div>numbers: <span style="color:#4ec9b0;">number[]</span></div><div>user: <span style="color:#4ec9b0;">&#123; name, age, email &#125;</span></div><div style="color:#f14c4c;margin-top:8px;">❌ user.address // 存在しない！</div></div>`}
		/>

		<!-- JS比較：配列とオブジェクト -->
		<div class="mt-4 mb-8 p-4 rounded-lg bg-yellow-50 dark:bg-yellow-900/20 border border-yellow-200 dark:border-yellow-800">
			<p class="font-semibold text-yellow-800 dark:text-yellow-200 mb-3">JavaScriptだと？</p>
			<div class="grid md:grid-cols-2 gap-4">
				<div>
					<p class="text-sm font-medium text-yellow-700 dark:text-yellow-300 mb-2">JavaScript</p>
					<pre class="text-xs bg-gray-900 text-gray-100 p-3 rounded overflow-x-auto"><code>let user = &#123;
  name: "田中太郎",
  age: 25,
  email: "tanaka@example.com"
&#125;;

// タイプミスしても気づけない
console.log(user.adress);  // ⚠️ undefined
// "address"のつもりが"adress"...

// 配列に何でも入る
let numbers = [1, 2, "三", true];
// ⚠️ 数値配列のはずが混在</code></pre>
				</div>
				<div>
					<p class="text-sm font-medium text-blue-700 dark:text-blue-300 mb-2">TypeScript</p>
					<pre class="text-xs bg-gray-900 text-gray-100 p-3 rounded overflow-x-auto"><code>let user: &#123;
  name: string;
  age: number;
  email: string;
&#125; = &#123; ... &#125;;

// タイプミスをすぐに検出
console.log(user.adress);  // ❌ エラー！
// → "adress"は存在しません

// 配列の型も守られる
let numbers: number[] = [1, 2, "三"];
// ❌ エラー: stringは入れられない</code></pre>
				</div>
			</div>
			<p class="text-xs text-yellow-600 dark:text-yellow-400 mt-3">
				JSでは存在しないプロパティにアクセスすると<code>undefined</code>が返る。TSではコンパイル時にエラーになるのでタイプミスを防げる。
			</p>
		</div>

		<CodePreview
			title="関数の型"
			description="引数と戻り値に型を付ける"
			language="typescript"
			code={`// 引数と戻り値の型
function greet(name: string): string {
  return "こんにちは、" + name + "さん！";
}

greet("田中");  // ✅ OK
greet(123);     // ❌ エラー: numberはstringに代入できない

// アロー関数
const add = (a: number, b: number): number => {
  return a + b;
};

// 戻り値がない関数
function log(message: string): void {
  console.log(message);
}`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div><span style="color:#dcdcaa;">greet</span>(name: <span style="color:#4ec9b0;">string</span>): <span style="color:#4ec9b0;">string</span></div><div style="color:#6a9955;">// 引数も戻り値も型で守られる</div></div>`}
		/>

		<!-- JS比較：関数の型 -->
		<div class="mt-4 mb-8 p-4 rounded-lg bg-yellow-50 dark:bg-yellow-900/20 border border-yellow-200 dark:border-yellow-800">
			<p class="font-semibold text-yellow-800 dark:text-yellow-200 mb-3">JavaScriptだと？</p>
			<div class="grid md:grid-cols-2 gap-4">
				<div>
					<p class="text-sm font-medium text-yellow-700 dark:text-yellow-300 mb-2">JavaScript</p>
					<pre class="text-xs bg-gray-900 text-gray-100 p-3 rounded overflow-x-auto"><code>function greet(name) &#123;
  return "こんにちは、" + name + "さん！";
&#125;

greet("田中");  // "こんにちは、田中さん！"
greet(123);     // "こんにちは、123さん！" ⚠️
greet();        // "こんにちは、undefinedさん！" ⚠️

// 引数を忘れても、型を間違えても
// エラーにならず実行されてしまう</code></pre>
				</div>
				<div>
					<p class="text-sm font-medium text-blue-700 dark:text-blue-300 mb-2">TypeScript</p>
					<pre class="text-xs bg-gray-900 text-gray-100 p-3 rounded overflow-x-auto"><code>function greet(name: string): string &#123;
  return "こんにちは、" + name + "さん！";
&#125;

greet("田中");  // ✅ OK
greet(123);     // ❌ エラー: 型が違う
greet();        // ❌ エラー: 引数が足りない

// 間違った使い方を事前に防げる
// IDEの補完も効く！</code></pre>
				</div>
			</div>
			<p class="text-xs text-yellow-600 dark:text-yellow-400 mt-3">
				JSでは引数の型も個数もチェックされない。TSでは関数の「正しい使い方」が型で定義され、間違えるとすぐに教えてくれる。
			</p>
		</div>

		<CodePreview
			title="Union型（複数の型を許容）"
			description="「AまたはB」という型"
			language="typescript"
			code={`// string または number を許容
let id: string | number;
id = "abc123";  // ✅ OK
id = 12345;     // ✅ OK
id = true;      // ❌ エラー: booleanは許可されていない

// null を許容する
let username: string | null = null;
username = "田中";  // ✅ OK
username = null;    // ✅ OK

// 関数の引数でも使える
function printId(id: string | number) {
  console.log("ID:", id);
}`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div><span style="color:#9cdcfe;">id</span>: <span style="color:#4ec9b0;">string</span> | <span style="color:#4ec9b0;">number</span></div><div style="color:#6a9955;">// 「どちらかの型」を表現できる</div></div>`}
		/>

		<!-- JS比較：Union型 -->
		<div class="mt-4 mb-8 p-4 rounded-lg bg-yellow-50 dark:bg-yellow-900/20 border border-yellow-200 dark:border-yellow-800">
			<p class="font-semibold text-yellow-800 dark:text-yellow-200 mb-3">JavaScriptだと？</p>
			<div class="grid md:grid-cols-2 gap-4">
				<div>
					<p class="text-sm font-medium text-yellow-700 dark:text-yellow-300 mb-2">JavaScript</p>
					<pre class="text-xs bg-gray-900 text-gray-100 p-3 rounded overflow-x-auto"><code>let id;
id = "abc123";  // OK
id = 12345;     // OK
id = true;      // OK（何でも入る）
id = &#123;&#125;;        // OK（オブジェクトも）
id = [];        // OK（配列も）

// 何が入っているか分からない
// → 使う側が常に確認が必要
if (typeof id === "string") &#123;
  // 文字列として処理
&#125;</code></pre>
				</div>
				<div>
					<p class="text-sm font-medium text-blue-700 dark:text-blue-300 mb-2">TypeScript</p>
					<pre class="text-xs bg-gray-900 text-gray-100 p-3 rounded overflow-x-auto"><code>let id: string | number;
id = "abc123";  // ✅ OK
id = 12345;     // ✅ OK
id = true;      // ❌ エラー！
id = &#123;&#125;;        // ❌ エラー！
id = [];        // ❌ エラー！

// 許可された型だけが入る
// → IDEも補完してくれる
// → 安心して使える</code></pre>
				</div>
			</div>
			<p class="text-xs text-yellow-600 dark:text-yellow-400 mt-3">
				JSには「この変数には文字列か数値だけ」という制限がない。TSのUnion型は「許可する型を明示的に指定」できる。
			</p>
		</div>

		<CodePreview
			title="型エイリアス（type）"
			description="型に名前を付けて再利用"
			language="typescript"
			code={`// 型エイリアスの定義
type User = {
  id: number;
  name: string;
  email: string;
};

// 再利用できる
const user1: User = {
  id: 1,
  name: "田中",
  email: "tanaka@example.com"
};

const user2: User = {
  id: 2,
  name: "鈴木",
  email: "suzuki@example.com"
};

// 配列でも使える
const users: User[] = [user1, user2];`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div><span style="color:#569cd6;">type</span> <span style="color:#4ec9b0;">User</span> = &#123; id, name, email &#125;</div><div style="color:#6a9955;">// 一度定義すれば何度でも使える</div></div>`}
		/>

		<!-- JS比較：型エイリアス -->
		<div class="mt-4 mb-8 p-4 rounded-lg bg-yellow-50 dark:bg-yellow-900/20 border border-yellow-200 dark:border-yellow-800">
			<p class="font-semibold text-yellow-800 dark:text-yellow-200 mb-3">JavaScriptだと？</p>
			<div class="grid md:grid-cols-2 gap-4">
				<div>
					<p class="text-sm font-medium text-yellow-700 dark:text-yellow-300 mb-2">JavaScript</p>
					<pre class="text-xs bg-gray-900 text-gray-100 p-3 rounded overflow-x-auto"><code>// 型の定義ができない
const user1 = &#123;
  id: 1,
  name: "田中",
  email: "tanaka@example.com"
&#125;;

// 別のユーザーを作るとき...
const user2 = &#123;
  id: 2,
  nama: "鈴木",  // ⚠️ タイプミス！
  mail: "suzuki@example.com"  // ⚠️ emailじゃない！
&#125;;
// エラーにならない...</code></pre>
				</div>
				<div>
					<p class="text-sm font-medium text-blue-700 dark:text-blue-300 mb-2">TypeScript</p>
					<pre class="text-xs bg-gray-900 text-gray-100 p-3 rounded overflow-x-auto"><code>// 型を一度定義
type User = &#123;
  id: number;
  name: string;
  email: string;
&#125;;

// 型に従わないとエラー
const user2: User = &#123;
  id: 2,
  nama: "鈴木",  // ❌ エラー: namaは存在しない
  mail: "..."    // ❌ エラー: mailは存在しない
&#125;;
// すぐに気づける！</code></pre>
				</div>
			</div>
			<p class="text-xs text-yellow-600 dark:text-yellow-400 mt-3">
				JSではオブジェクトの「正しい形」を定義できない。TSの型エイリアスは「設計図」として機能し、統一された構造を強制できる。
			</p>
		</div>

		<CodePreview
			title="オプショナルプロパティ"
			description="「あってもなくてもいい」プロパティ"
			language="typescript"
			code={`type User = {
  id: number;
  name: string;
  email?: string;  // ? をつけると省略可能
};

// emailはなくてもOK
const user1: User = {
  id: 1,
  name: "田中"
};

// emailがあってもOK
const user2: User = {
  id: 2,
  name: "鈴木",
  email: "suzuki@example.com"
};`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div>email<span style="color:#569cd6;">?</span>: string</div><div style="color:#6a9955;">// ? = オプショナル（省略可能）</div></div>`}
		/>

		<!-- JS比較：オプショナルプロパティ -->
		<div class="mt-4 mb-8 p-4 rounded-lg bg-yellow-50 dark:bg-yellow-900/20 border border-yellow-200 dark:border-yellow-800">
			<p class="font-semibold text-yellow-800 dark:text-yellow-200 mb-3">JavaScriptだと？</p>
			<div class="grid md:grid-cols-2 gap-4">
				<div>
					<p class="text-sm font-medium text-yellow-700 dark:text-yellow-300 mb-2">JavaScript</p>
					<pre class="text-xs bg-gray-900 text-gray-100 p-3 rounded overflow-x-auto"><code>const user1 = &#123;
  id: 1,
  name: "田中"
  // emailがない
&#125;;

const user2 = &#123;
  id: 2,
  name: "鈴木",
  email: "suzuki@example.com"
&#125;;

// どちらが「正しい」か分からない
// emailは必須？任意？
// → コメントやドキュメントを見るしかない</code></pre>
				</div>
				<div>
					<p class="text-sm font-medium text-blue-700 dark:text-blue-300 mb-2">TypeScript</p>
					<pre class="text-xs bg-gray-900 text-gray-100 p-3 rounded overflow-x-auto"><code>type User = &#123;
  id: number;
  name: string;
  email?: string;  // ? = 任意
&#125;;

const user1: User = &#123;
  id: 1,
  name: "田中"  // ✅ emailなしでOK
&#125;;

// 型を見れば「emailは任意」と
// 一目で分かる！
// IDEのヒントでも表示される</code></pre>
				</div>
			</div>
			<p class="text-xs text-yellow-600 dark:text-yellow-400 mt-3">
				JSでは「このプロパティは必須？任意？」がコードから読み取れない。TSの<code>?</code>は「省略可能」を明示し、コードが自己文書化される。
			</p>
		</div>
	</section>

	<!-- TypeScript vs JavaScript -->
	<section class="mb-10">
		<h2 id="comparison" class="text-xl font-bold mb-4">JavaScript vs TypeScript</h2>

		<div class="grid grid-cols-1 md:grid-cols-2 gap-4">
			<div class="p-4 rounded-lg bg-yellow-50 dark:bg-yellow-900/20 border border-yellow-200 dark:border-yellow-800">
				<h3 class="font-semibold text-yellow-800 dark:text-yellow-200 mb-2">JavaScript</h3>
				<pre class="text-sm bg-gray-900 text-gray-100 p-3 rounded overflow-x-auto"><code>function greet(name) &#123;
  return "Hello, " + name;
&#125;

greet(123);  // 実行時まで
             // エラーに気づけない</code></pre>
			</div>
			<div class="p-4 rounded-lg bg-blue-50 dark:bg-blue-900/20 border border-blue-200 dark:border-blue-800">
				<h3 class="font-semibold text-blue-800 dark:text-blue-200 mb-2">TypeScript</h3>
				<pre class="text-sm bg-gray-900 text-gray-100 p-3 rounded overflow-x-auto"><code>function greet(name: string) &#123;
  return "Hello, " + name;
&#125;

greet(123);  // ❌ コンパイル時に
             // エラーを検出！</code></pre>
			</div>
		</div>
	</section>

	<!-- ナビゲーション -->
	<div class="flex justify-between pt-6 border-t border-gray-200 dark:border-gray-700">
		<a href="/js/async" class="inline-flex items-center gap-2 px-4 py-2 rounded-lg border border-gray-300 dark:border-gray-600 hover:bg-gray-100 dark:hover:bg-gray-800 transition-colors">
			<svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
				<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 19l-7-7 7-7" />
			</svg>
			前へ：JavaScript
		</a>
		<a href="/ts/types" class="inline-flex items-center gap-2 px-4 py-2 rounded-lg bg-primary-600 text-white hover:bg-primary-700 transition-colors">
			次へ：型の種類
			<svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
				<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 5l7 7-7 7" />
			</svg>
		</a>
	</div>
</article>
