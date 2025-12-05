<script>
	import CodePreview from '$lib/components/CodePreview.svelte';
</script>

<svelte:head>
	<title>TypeScript インターフェース | さとまたラボ</title>
</svelte:head>

<article>
	<h1 class="text-3xl font-bold mb-2">インターフェース</h1>
	<p class="text-lg text-gray-600 dark:text-gray-400 mb-8">
		オブジェクトの形を定義する強力な機能
	</p>

	<!-- インターフェースとは -->
	<section class="mb-10">
		<h2 id="what-is" class="text-xl font-bold mb-4">インターフェースとは？</h2>

		<div class="p-6 rounded-xl bg-blue-50 dark:bg-blue-900/20 border border-blue-200 dark:border-blue-800 mb-6">
			<p class="text-blue-800 dark:text-blue-200 mb-4">
				<strong>日常での例え：</strong>設計図・仕様書
			</p>
			<div class="grid grid-cols-1 md:grid-cols-2 gap-4 text-sm">
				<div class="p-3 bg-white dark:bg-gray-800 rounded-lg">
					<div class="font-semibold text-blue-700 dark:text-blue-300 mb-2">建築の設計図</div>
					<p class="text-gray-600 dark:text-gray-400">
						「この建物には玄関、リビング、寝室が必要」<br>
						と構造を決める
					</p>
				</div>
				<div class="p-3 bg-white dark:bg-gray-800 rounded-lg">
					<div class="font-semibold text-blue-700 dark:text-blue-300 mb-2">interface</div>
					<p class="text-gray-600 dark:text-gray-400">
						「このオブジェクトにはname, age, emailが必要」<br>
						と構造を決める
					</p>
				</div>
			</div>
		</div>

		<div class="p-4 rounded-lg bg-amber-50 dark:bg-amber-900/20 border border-amber-200 dark:border-amber-800 mb-6">
			<p class="font-semibold text-amber-800 dark:text-amber-200">なぜinterfaceが必要？</p>
			<div class="text-sm text-amber-700 dark:text-amber-300 mt-2">
				<p class="mb-2"><strong>毎回同じ型を書くのは大変：</strong></p>
				<ul class="list-disc list-inside space-y-1 mb-3">
					<li>ユーザー情報を使う場所が10箇所あったら、10回書く？</li>
					<li>プロパティを追加したら、10箇所全部直す？</li>
				</ul>
				<p><strong>interfaceなら：</strong>1箇所で定義、どこでも使い回せる！</p>
			</div>
		</div>
	</section>

	<!-- 基本的な使い方 -->
	<section class="mb-10">
		<h2 id="basic" class="text-xl font-bold mb-4">基本的な使い方</h2>

		<CodePreview
			title="interfaceの定義"
			description="オブジェクトの形を定義"
			language="typescript"
			code={`// interfaceを定義
interface User {
  id: number;
  name: string;
  email: string;
}

// interfaceを使う
const user: User = {
  id: 1,
  name: "田中太郎",
  email: "tanaka@example.com"
};

// 関数の引数にも使える
function greetUser(user: User) {
  console.log(\`こんにちは、\${user.name}さん！\`);
}

// 配列の型にも使える
const users: User[] = [user];`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div><span style="color:#569cd6;">interface</span> <span style="color:#4ec9b0;">User</span> &#123;</div><div style="padding-left:12px;">id: <span style="color:#4ec9b0;">number</span></div><div style="padding-left:12px;">name: <span style="color:#4ec9b0;">string</span></div><div>&#125;</div></div>`}
		/>

		<CodePreview
			title="オプショナルプロパティ"
			description="あってもなくてもいいプロパティ"
			language="typescript"
			code={`interface User {
  id: number;
  name: string;
  email: string;
  age?: number;      // ? = オプショナル
  phone?: string;    // なくてもOK
}

// ageとphoneは省略可能
const user1: User = {
  id: 1,
  name: "田中",
  email: "tanaka@example.com"
};

// あってもOK
const user2: User = {
  id: 2,
  name: "鈴木",
  email: "suzuki@example.com",
  age: 30
};`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div>age<span style="color:#569cd6;">?</span>: number</div><div style="color:#6a9955;">// ? をつけると省略可能に</div></div>`}
		/>

		<CodePreview
			title="読み取り専用プロパティ"
			description="変更を禁止する"
			language="typescript"
			code={`interface Config {
  readonly apiKey: string;
  readonly baseUrl: string;
  timeout: number;
}

const config: Config = {
  apiKey: "abc123",
  baseUrl: "https://api.example.com",
  timeout: 5000
};

// readonlyは変更できない
config.apiKey = "xyz";  // ❌ エラー！

// readonlyじゃないプロパティは変更OK
config.timeout = 10000; // ✅ OK`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div><span style="color:#569cd6;">readonly</span> apiKey: string</div><div style="color:#6a9955;">// 一度設定したら変更禁止</div></div>`}
		/>
	</section>

	<!-- 関数の型 -->
	<section class="mb-10">
		<h2 id="function" class="text-xl font-bold mb-4">関数を含むinterface</h2>

		<CodePreview
			title="メソッドの定義"
			description="関数もプロパティとして定義"
			language="typescript"
			code={`interface Calculator {
  // 書き方1: メソッド記法
  add(a: number, b: number): number;

  // 書き方2: プロパティ記法
  subtract: (a: number, b: number) => number;
}

const calc: Calculator = {
  add(a, b) {
    return a + b;
  },
  subtract: (a, b) => a - b
};

console.log(calc.add(5, 3));      // 8
console.log(calc.subtract(5, 3)); // 2`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div style="color:#6a9955;">// メソッドも型定義できる</div><div>add(a, b): number</div><div>subtract: (a, b) =&gt; number</div></div>`}
		/>
	</section>

	<!-- interfaceの拡張 -->
	<section class="mb-10">
		<h2 id="extends" class="text-xl font-bold mb-4">interfaceの拡張（extends）</h2>

		<div class="p-6 rounded-xl bg-blue-50 dark:bg-blue-900/20 border border-blue-200 dark:border-blue-800 mb-6">
			<p class="text-blue-800 dark:text-blue-200 mb-4">
				<strong>日常での例え：</strong>基本プランとオプション追加
			</p>
			<div class="text-sm text-blue-700 dark:text-blue-300">
				<p>「基本プラン」に「プレミアムオプション」を追加して「プレミアムプラン」に</p>
				<p class="mt-2">extendsは既存のinterfaceに機能を追加します</p>
			</div>
		</div>

		<CodePreview
			title="extendsで拡張"
			description="既存のinterfaceを継承"
			language="typescript"
			code={`// 基本のinterface
interface Animal {
  name: string;
  age: number;
}

// Animalを拡張してDogを作る
interface Dog extends Animal {
  breed: string;  // 犬種を追加
  bark(): void;   // メソッドも追加
}

const dog: Dog = {
  name: "ポチ",
  age: 3,
  breed: "柴犬",
  bark() {
    console.log("ワンワン！");
  }
};

// Dogはname, age, breed, barkすべて必要`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div><span style="color:#569cd6;">interface</span> Dog <span style="color:#569cd6;">extends</span> Animal</div><div style="color:#6a9955;">// AnimalのプロパティをすべてDogを含む</div></div>`}
		/>

		<CodePreview
			title="複数のinterfaceを拡張"
			description="複数を組み合わせる"
			language="typescript"
			code={`interface Named {
  name: string;
}

interface Aged {
  age: number;
}

interface Emailable {
  email: string;
}

// 複数を同時に拡張
interface User extends Named, Aged, Emailable {
  id: number;
}

const user: User = {
  id: 1,
  name: "田中",
  age: 25,
  email: "tanaka@example.com"
};`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div><span style="color:#569cd6;">extends</span> A, B, C</div><div style="color:#6a9955;">// 複数のinterfaceを組み合わせ</div></div>`}
		/>
	</section>

	<!-- interface vs type -->
	<section class="mb-10">
		<h2 id="vs-type" class="text-xl font-bold mb-4">interface vs type</h2>

		<div class="p-4 rounded-lg bg-gray-100 dark:bg-gray-800 mb-6">
			<p class="font-semibold text-gray-800 dark:text-gray-200 mb-2">どっちを使う？</p>
			<div class="text-sm text-gray-700 dark:text-gray-300">
				<p class="mb-2">基本的には<strong>どちらでもOK</strong>！ほぼ同じことができます。</p>
				<p>チームで統一するか、以下の使い分けを参考に：</p>
			</div>
		</div>

		<div class="grid grid-cols-1 md:grid-cols-2 gap-4 mb-6">
			<div class="p-4 rounded-lg bg-blue-50 dark:bg-blue-900/20 border border-blue-200 dark:border-blue-800">
				<h3 class="font-semibold text-blue-800 dark:text-blue-200 mb-2">interface が向いている</h3>
				<ul class="text-sm text-blue-700 dark:text-blue-300 list-disc list-inside space-y-1">
					<li>オブジェクトの形を定義</li>
					<li>クラスで実装（implements）</li>
					<li>拡張（extends）を多用する</li>
					<li>宣言マージが必要</li>
				</ul>
			</div>
			<div class="p-4 rounded-lg bg-purple-50 dark:bg-purple-900/20 border border-purple-200 dark:border-purple-800">
				<h3 class="font-semibold text-purple-800 dark:text-purple-200 mb-2">type が向いている</h3>
				<ul class="text-sm text-purple-700 dark:text-purple-300 list-disc list-inside space-y-1">
					<li>Union型（A | B）</li>
					<li>プリミティブ型のエイリアス</li>
					<li>タプル型</li>
					<li>複雑な型の演算</li>
				</ul>
			</div>
		</div>

		<CodePreview
			title="同じことができる例"
			description="どちらでも書ける"
			language="typescript"
			code={`// interface
interface User1 {
  name: string;
  age: number;
}

// type
type User2 = {
  name: string;
  age: number;
};

// どちらも同じように使える
const user1: User1 = { name: "田中", age: 25 };
const user2: User2 = { name: "鈴木", age: 30 };`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div style="color:#6a9955;">// オブジェクトの型定義なら</div><div style="color:#6a9955;">// interfaceでもtypeでもOK</div></div>`}
		/>

		<CodePreview
			title="typeでしかできないこと"
			description="Union型やプリミティブ型"
			language="typescript"
			code={`// Union型はtypeで
type Status = "pending" | "approved" | "rejected";

// プリミティブのエイリアスはtypeで
type ID = string | number;

// タプルはtypeで
type Point = [number, number];

// これらはinterfaceでは書けない`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div><span style="color:#569cd6;">type</span> Status = <span style="color:#ce9178;">"A"</span> | <span style="color:#ce9178;">"B"</span></div><div style="color:#6a9955;">// Union型はtypeを使う</div></div>`}
		/>

		<CodePreview
			title="interfaceでしかできないこと"
			description="宣言マージ"
			language="typescript"
			code={`// 宣言マージ: 同名のinterfaceが合体する
interface Window {
  myCustomProperty: string;
}

// 既存のWindow型に追加される
// ライブラリの型を拡張する時に便利

// typeは同名で再定義するとエラー
type MyType = { a: string };
type MyType = { b: number };  // ❌ エラー！`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div style="color:#6a9955;">// interfaceは同名で追加できる</div><div style="color:#6a9955;">// （宣言マージ）</div></div>`}
		/>
	</section>

	<!-- 実践的な使い方 -->
	<section class="mb-10">
		<h2 id="practical" class="text-xl font-bold mb-4">実践的な使い方</h2>

		<CodePreview
			title="APIレスポンスの型"
			description="実際のプロジェクトでよく使う"
			language="typescript"
			code={`// APIレスポンスの型定義
interface ApiResponse<T> {
  data: T;
  status: number;
  message: string;
}

interface User {
  id: number;
  name: string;
  email: string;
}

// 使用例
async function fetchUser(id: number): Promise<ApiResponse<User>> {
  const response = await fetch(\`/api/users/\${id}\`);
  return response.json();
}

// 型安全にアクセス
const result = await fetchUser(1);
console.log(result.data.name);  // 補完が効く！`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div style="color:#6a9955;">// APIの型を定義すると</div><div style="color:#6a9955;">// レスポンスの型が保証される</div></div>`}
		/>

		<CodePreview
			title="Reactコンポーネントのprops"
			description="フロントエンド開発で頻出"
			language="typescript"
			code={`// Reactコンポーネントのprops型
interface ButtonProps {
  label: string;
  onClick: () => void;
  variant?: "primary" | "secondary";
  disabled?: boolean;
}

function Button({ label, onClick, variant = "primary", disabled }: ButtonProps) {
  return (
    <button
      onClick={onClick}
      disabled={disabled}
      className={variant}
    >
      {label}
    </button>
  );
}

// 使用時に型チェック
<Button label="送信" onClick={() => {}} />  // ✅
<Button label={123} onClick={() => {}} />   // ❌ エラー`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div style="color:#6a9955;">// propsの型を定義すると</div><div style="color:#6a9955;">// コンポーネントが安全に使える</div></div>`}
		/>
	</section>

	<!-- ナビゲーション -->
	<div class="flex justify-between pt-6 border-t border-gray-200 dark:border-gray-700">
		<a href="/ts/types" class="inline-flex items-center gap-2 px-4 py-2 rounded-lg border border-gray-300 dark:border-gray-600 hover:bg-gray-100 dark:hover:bg-gray-800 transition-colors">
			<svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
				<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 19l-7-7 7-7" />
			</svg>
			前へ：型の種類
		</a>
		<a href="/ts/generics" class="inline-flex items-center gap-2 px-4 py-2 rounded-lg bg-primary-600 text-white hover:bg-primary-700 transition-colors">
			次へ：ジェネリクス
			<svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
				<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 5l7 7-7 7" />
			</svg>
		</a>
	</div>
</article>
