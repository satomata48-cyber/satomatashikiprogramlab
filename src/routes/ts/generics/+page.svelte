<script>
	import CodePreview from '$lib/components/CodePreview.svelte';
</script>

<svelte:head>
	<title>TypeScript ジェネリクス | さとまたラボ</title>
</svelte:head>

<article>
	<h1 class="text-3xl font-bold mb-2">ジェネリクス</h1>
	<p class="text-lg text-gray-600 dark:text-gray-400 mb-8">
		型を「あとから決める」柔軟な仕組み
	</p>

	<!-- ジェネリクスとは -->
	<section class="mb-10">
		<h2 id="what-is" class="text-xl font-bold mb-4">ジェネリクスとは？</h2>

		<div class="p-6 rounded-xl bg-blue-50 dark:bg-blue-900/20 border border-blue-200 dark:border-blue-800 mb-6">
			<p class="text-blue-800 dark:text-blue-200 mb-4">
				<strong>日常での例え：</strong>サイズ選択できるTシャツ
			</p>
			<div class="grid grid-cols-1 md:grid-cols-2 gap-4 text-sm">
				<div class="p-3 bg-white dark:bg-gray-800 rounded-lg">
					<div class="font-semibold text-blue-700 dark:text-blue-300 mb-2">サイズ固定のTシャツ</div>
					<p class="text-gray-600 dark:text-gray-400">
						「S用」「M用」「L用」を<br>
						それぞれ別に作る必要がある
					</p>
				</div>
				<div class="p-3 bg-white dark:bg-gray-800 rounded-lg">
					<div class="font-semibold text-blue-700 dark:text-blue-300 mb-2">サイズ選択可能</div>
					<p class="text-gray-600 dark:text-gray-400">
						1つのデザインで「サイズはあとで選んでね」<br>
						→ どのサイズにも対応できる
					</p>
				</div>
			</div>
		</div>

		<div class="p-4 rounded-lg bg-amber-50 dark:bg-amber-900/20 border border-amber-200 dark:border-amber-800 mb-6">
			<p class="font-semibold text-amber-800 dark:text-amber-200">なぜジェネリクスが必要？</p>
			<div class="text-sm text-amber-700 dark:text-amber-300 mt-2">
				<p class="mb-2"><strong>問題：</strong>同じ処理を型ごとに書くのは無駄</p>
				<ul class="list-disc list-inside space-y-1 mb-3">
					<li>数値の配列の最初の要素を返す関数</li>
					<li>文字列の配列の最初の要素を返す関数</li>
					<li>ユーザーの配列の最初の要素を返す関数...</li>
				</ul>
				<p><strong>ジェネリクスなら：</strong>「どんな型でもOK」な関数を1つ作れる！</p>
			</div>
		</div>
	</section>

	<!-- 問題の理解 -->
	<section class="mb-10">
		<h2 id="problem" class="text-xl font-bold mb-4">ジェネリクスなしの問題</h2>

		<CodePreview
			title="anyを使う場合"
			description="型安全性が失われる"
			language="typescript"
			code={`// anyを使うと何でも受け取れるが...
function getFirst(arr: any[]): any {
  return arr[0];
}

const nums = getFirst([1, 2, 3]);
// numsの型はany... 数値かどうか分からない

const names = getFirst(["田中", "鈴木"]);
// namesの型もany... 文字列かどうか分からない

// 型の恩恵がなくなってしまう！`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div style="color:#f14c4c;">⚠️ anyは型情報が消える</div><div style="color:#6a9955;">戻り値の型が分からない</div></div>`}
		/>

		<CodePreview
			title="型ごとに関数を作る"
			description="同じコードの重複"
			language="typescript"
			code={`// 型ごとに関数を作ると...
function getFirstNumber(arr: number[]): number {
  return arr[0];
}

function getFirstString(arr: string[]): string {
  return arr[0];
}

function getFirstUser(arr: User[]): User {
  return arr[0];
}

// 同じ処理なのに何度も書く... 非効率！`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div style="color:#f14c4c;">⚠️ 同じコードの繰り返し</div><div style="color:#6a9955;">メンテナンスが大変</div></div>`}
		/>
	</section>

	<!-- ジェネリクスの基本 -->
	<section class="mb-10">
		<h2 id="basic" class="text-xl font-bold mb-4">ジェネリクスの基本</h2>

		<CodePreview
			title="ジェネリック関数"
			description="型を引数のように受け取る"
			language="typescript"
			code={`// <T> が型パラメータ（型の引数）
function getFirst<T>(arr: T[]): T {
  return arr[0];
}

// 使う時に型を指定
const num = getFirst<number>([1, 2, 3]);
// numの型はnumber

const name = getFirst<string>(["田中", "鈴木"]);
// nameの型はstring

// 型推論もできる（省略可能）
const item = getFirst([true, false]);
// itemの型はboolean（自動推論）`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div>function <span style="color:#dcdcaa;">getFirst</span>&lt;<span style="color:#4ec9b0;">T</span>&gt;(arr: <span style="color:#4ec9b0;">T</span>[]): <span style="color:#4ec9b0;">T</span></div><div style="color:#6a9955;">// Tは「あとで決める型」</div></div>`}
		/>

		<CodePreview
			title="複数の型パラメータ"
			description="2つ以上の型も使える"
			language="typescript"
			code={`// 2つの型パラメータ
function pair<T, U>(first: T, second: U): [T, U] {
  return [first, second];
}

const result = pair<string, number>("age", 25);
// resultの型は [string, number]

// 型推論で省略
const auto = pair("name", "田中");
// autoの型は [string, string]

// キーと値のマップ
function toObject<K extends string, V>(key: K, value: V) {
  return { [key]: value };
}`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div>&lt;<span style="color:#4ec9b0;">T</span>, <span style="color:#4ec9b0;">U</span>&gt;</div><div style="color:#6a9955;">// 複数の型パラメータも可能</div></div>`}
		/>
	</section>

	<!-- ジェネリック制約 -->
	<section class="mb-10">
		<h2 id="constraints" class="text-xl font-bold mb-4">ジェネリック制約（extends）</h2>

		<div class="p-6 rounded-xl bg-blue-50 dark:bg-blue-900/20 border border-blue-200 dark:border-blue-800 mb-6">
			<p class="text-blue-800 dark:text-blue-200 mb-4">
				<strong>日常での例え：</strong>条件付きの募集
			</p>
			<div class="text-sm text-blue-700 dark:text-blue-300">
				<p>「18歳以上の方を募集」= 誰でもいいけど年齢条件あり</p>
				<p class="mt-2">ジェネリクスも「〇〇を満たす型のみ」と制約をつけられます</p>
			</div>
		</div>

		<CodePreview
			title="extendsで制約をつける"
			description="特定の型のみ許可"
			language="typescript"
			code={`// lengthプロパティを持つ型のみ許可
function logLength<T extends { length: number }>(item: T): void {
  console.log(item.length);
}

logLength("hello");      // ✅ OK (文字列はlengthあり)
logLength([1, 2, 3]);    // ✅ OK (配列はlengthあり)
logLength({ length: 5 }); // ✅ OK

logLength(123);          // ❌ エラー！numberにlengthはない
logLength({ name: "a" }); // ❌ エラー！lengthがない`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div>T <span style="color:#569cd6;">extends</span> &#123; length: number &#125;</div><div style="color:#6a9955;">// lengthを持つ型のみ許可</div></div>`}
		/>

		<CodePreview
			title="interfaceを使った制約"
			description="より明確な制約"
			language="typescript"
			code={`interface HasId {
  id: number;
}

// HasIdを満たす型のみ許可
function findById<T extends HasId>(items: T[], id: number): T | undefined {
  return items.find(item => item.id === id);
}

interface User extends HasId {
  name: string;
}

interface Product extends HasId {
  title: string;
  price: number;
}

const users: User[] = [{ id: 1, name: "田中" }];
const products: Product[] = [{ id: 1, title: "PC", price: 100000 }];

findById(users, 1);    // ✅ User | undefined
findById(products, 1); // ✅ Product | undefined`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div style="color:#6a9955;">// HasIdを満たす型なら</div><div style="color:#6a9955;">// どんな型でも使える</div></div>`}
		/>
	</section>

	<!-- ジェネリッククラス -->
	<section class="mb-10">
		<h2 id="class" class="text-xl font-bold mb-4">ジェネリッククラス</h2>

		<CodePreview
			title="クラスでジェネリクス"
			description="データ構造の実装に便利"
			language="typescript"
			code={`// スタック（後入れ先出し）のジェネリッククラス
class Stack<T> {
  private items: T[] = [];

  push(item: T): void {
    this.items.push(item);
  }

  pop(): T | undefined {
    return this.items.pop();
  }

  peek(): T | undefined {
    return this.items[this.items.length - 1];
  }
}

// 数値のスタック
const numberStack = new Stack<number>();
numberStack.push(1);
numberStack.push(2);
numberStack.pop();  // 2

// 文字列のスタック
const stringStack = new Stack<string>();
stringStack.push("hello");`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div><span style="color:#569cd6;">class</span> Stack&lt;<span style="color:#4ec9b0;">T</span>&gt;</div><div style="color:#6a9955;">// 型安全なデータ構造</div></div>`}
		/>
	</section>

	<!-- ジェネリックインターフェース -->
	<section class="mb-10">
		<h2 id="interface" class="text-xl font-bold mb-4">ジェネリックインターフェース</h2>

		<CodePreview
			title="インターフェースでジェネリクス"
			description="APIレスポンスなどに便利"
			language="typescript"
			code={`// APIレスポンスの汎用型
interface ApiResponse<T> {
  data: T;
  status: number;
  message: string;
  timestamp: Date;
}

interface User {
  id: number;
  name: string;
}

interface Product {
  id: number;
  title: string;
}

// 使い分け
type UserResponse = ApiResponse<User>;
type ProductResponse = ApiResponse<Product>;
type UsersResponse = ApiResponse<User[]>;

// 関数の戻り値にも
async function fetchUser(id: number): Promise<ApiResponse<User>> {
  // ...
}`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div>ApiResponse&lt;<span style="color:#4ec9b0;">User</span>&gt;</div><div>ApiResponse&lt;<span style="color:#4ec9b0;">Product</span>&gt;</div><div style="color:#6a9955;">// 同じ構造、違うデータ</div></div>`}
		/>
	</section>

	<!-- ユーティリティ型 -->
	<section class="mb-10">
		<h2 id="utility" class="text-xl font-bold mb-4">組み込みユーティリティ型</h2>

		<div class="p-4 rounded-lg bg-gray-100 dark:bg-gray-800 mb-6">
			<p class="font-semibold text-gray-800 dark:text-gray-200 mb-2">便利なジェネリクス型が用意されている</p>
			<div class="text-sm text-gray-700 dark:text-gray-300">
				TypeScriptには、よく使うジェネリクス型が最初から用意されています。
			</div>
		</div>

		<CodePreview
			title="Partial<T>"
			description="全プロパティをオプショナルに"
			language="typescript"
			code={`interface User {
  id: number;
  name: string;
  email: string;
}

// Partial<User> = 全プロパティが省略可能
type PartialUser = Partial<User>;
// {
//   id?: number;
//   name?: string;
//   email?: string;
// }

// 更新時に便利
function updateUser(id: number, updates: Partial<User>) {
  // 一部のプロパティだけ更新
}

updateUser(1, { name: "新しい名前" });  // ✅ OK`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div><span style="color:#4ec9b0;">Partial</span>&lt;User&gt;</div><div style="color:#6a9955;">// 全部オプショナルに</div></div>`}
		/>

		<CodePreview
			title="Required<T>"
			description="全プロパティを必須に"
			language="typescript"
			code={`interface Config {
  host?: string;
  port?: number;
  debug?: boolean;
}

// Required<Config> = 全プロパティが必須
type RequiredConfig = Required<Config>;
// {
//   host: string;
//   port: number;
//   debug: boolean;
// }

const config: RequiredConfig = {
  host: "localhost",
  port: 3000,
  debug: true
  // 全部必須！省略するとエラー
};`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div><span style="color:#4ec9b0;">Required</span>&lt;Config&gt;</div><div style="color:#6a9955;">// 全部必須に</div></div>`}
		/>

		<CodePreview
			title="Pick<T, K> と Omit<T, K>"
			description="プロパティの選択・除外"
			language="typescript"
			code={`interface User {
  id: number;
  name: string;
  email: string;
  password: string;
}

// Pick: 指定したプロパティだけ取り出す
type UserPreview = Pick<User, "id" | "name">;
// { id: number; name: string; }

// Omit: 指定したプロパティを除外
type PublicUser = Omit<User, "password">;
// { id: number; name: string; email: string; }

// APIレスポンスで便利
function getPublicUser(user: User): PublicUser {
  const { password, ...publicUser } = user;
  return publicUser;
}`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div><span style="color:#4ec9b0;">Pick</span>&lt;User, "id" | "name"&gt;</div><div><span style="color:#4ec9b0;">Omit</span>&lt;User, "password"&gt;</div></div>`}
		/>

		<CodePreview
			title="Record<K, V>"
			description="キーと値の型を指定したオブジェクト"
			language="typescript"
			code={`// Record<キーの型, 値の型>
type Scores = Record<string, number>;

const scores: Scores = {
  math: 85,
  english: 90,
  science: 78
};

// Union型をキーに
type Status = "pending" | "approved" | "rejected";
type StatusMessages = Record<Status, string>;

const messages: StatusMessages = {
  pending: "審査中です",
  approved: "承認されました",
  rejected: "却下されました"
};`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div><span style="color:#4ec9b0;">Record</span>&lt;string, number&gt;</div><div style="color:#6a9955;">// オブジェクトの型を簡潔に</div></div>`}
		/>
	</section>

	<!-- まとめ -->
	<section class="mb-10">
		<h2 id="summary" class="text-xl font-bold mb-4">ジェネリクスまとめ</h2>

		<div class="grid grid-cols-1 md:grid-cols-2 gap-4">
			<div class="p-4 rounded-lg bg-green-50 dark:bg-green-900/20 border border-green-200 dark:border-green-800">
				<h3 class="font-semibold text-green-800 dark:text-green-200 mb-2">ジェネリクスを使うと</h3>
				<ul class="text-sm text-green-700 dark:text-green-300 list-disc list-inside space-y-1">
					<li>型安全性を保ちつつ汎用的なコードが書ける</li>
					<li>同じ処理の重複を避けられる</li>
					<li>anyより安全</li>
					<li>型推論で省略もできる</li>
				</ul>
			</div>
			<div class="p-4 rounded-lg bg-blue-50 dark:bg-blue-900/20 border border-blue-200 dark:border-blue-800">
				<h3 class="font-semibold text-blue-800 dark:text-blue-200 mb-2">よく使う場面</h3>
				<ul class="text-sm text-blue-700 dark:text-blue-300 list-disc list-inside space-y-1">
					<li>配列操作の関数</li>
					<li>APIレスポンスの型</li>
					<li>データ構造（Stack, Queueなど）</li>
					<li>Reactコンポーネント</li>
				</ul>
			</div>
		</div>
	</section>

	<!-- ナビゲーション -->
	<div class="flex justify-between pt-6 border-t border-gray-200 dark:border-gray-700">
		<a href="/ts/interfaces" class="inline-flex items-center gap-2 px-4 py-2 rounded-lg border border-gray-300 dark:border-gray-600 hover:bg-gray-100 dark:hover:bg-gray-800 transition-colors">
			<svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
				<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 19l-7-7 7-7" />
			</svg>
			前へ：インターフェース
		</a>
		<a href="/nextjs/intro" class="inline-flex items-center gap-2 px-4 py-2 rounded-lg bg-primary-600 text-white hover:bg-primary-700 transition-colors">
			次へ：Next.js
			<svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
				<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 5l7 7-7 7" />
			</svg>
		</a>
	</div>
</article>
