<script>
	import CodePreview from '$lib/components/CodePreview.svelte';
</script>

<svelte:head>
	<title>TypeScript 型の種類 | さとまたラボ</title>
</svelte:head>

<article>
	<h1 class="text-3xl font-bold mb-2">型の種類</h1>
	<p class="text-lg text-gray-600 dark:text-gray-400 mb-8">
		TypeScriptで使える様々な型を学ぶ
	</p>

	<!-- プリミティブ型 -->
	<section class="mb-10">
		<h2 id="primitive" class="text-xl font-bold mb-4">プリミティブ型（基本の型）</h2>

		<div class="p-6 rounded-xl bg-blue-50 dark:bg-blue-900/20 border border-blue-200 dark:border-blue-800 mb-6">
			<p class="text-blue-800 dark:text-blue-200 mb-4">
				<strong>日常での例え：</strong>基本の材料
			</p>
			<div class="text-sm text-blue-700 dark:text-blue-300">
				<p>料理で言うと、塩・砂糖・小麦粉のような「基本の材料」</p>
				<p class="mt-2">これらを組み合わせて複雑な料理（型）を作ります</p>
			</div>
		</div>

		<CodePreview
			title="基本の型"
			description="string, number, boolean"
			language="typescript"
			code={`// 文字列型
let name: string = "田中";
let greeting: string = \`こんにちは、\${name}さん\`;

// 数値型（整数も小数も同じnumber）
let age: number = 25;
let price: number = 1980.5;
let hex: number = 0xff;  // 16進数もOK

// 真偽値型
let isActive: boolean = true;
let isLoggedIn: boolean = false;

// これらは「プリミティブ型」と呼ばれる
// 最も基本的な型です`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div><span style="color:#4ec9b0;">string</span> → 文字列</div><div><span style="color:#4ec9b0;">number</span> → 数値</div><div><span style="color:#4ec9b0;">boolean</span> → true/false</div></div>`}
		/>

		<CodePreview
			title="null と undefined"
			description="「値がない」を表す型"
			language="typescript"
			code={`// undefined: 値が設定されていない
let notSet: undefined = undefined;

// null: 意図的に「空」を設定
let empty: null = null;

// 実際の使い方（Union型と組み合わせ）
let username: string | null = null;  // まだ設定されていない
username = "田中";  // 後から設定

// undefinedは「まだない」
// nullは「意図的に空」という違いがある`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div style="color:#6a9955;">// undefined = 未定義</div><div style="color:#6a9955;">// null = 意図的な空</div></div>`}
		/>
	</section>

	<!-- 配列型 -->
	<section class="mb-10">
		<h2 id="array" class="text-xl font-bold mb-4">配列型（Array）</h2>

		<div class="p-6 rounded-xl bg-blue-50 dark:bg-blue-900/20 border border-blue-200 dark:border-blue-800 mb-6">
			<p class="text-blue-800 dark:text-blue-200 mb-4">
				<strong>日常での例え：</strong>同じ種類の物を入れる棚
			</p>
			<div class="text-sm text-blue-700 dark:text-blue-300">
				<p>「本棚」には本だけ、「靴箱」には靴だけ</p>
				<p class="mt-2">配列型も「この棚には〇〇型だけ」と決められます</p>
			</div>
		</div>

		<CodePreview
			title="配列の型指定"
			description="2つの書き方がある"
			language="typescript"
			code={`// 書き方1: 型[]
let numbers: number[] = [1, 2, 3, 4, 5];
let names: string[] = ["田中", "鈴木", "佐藤"];

// 書き方2: Array<型>
let scores: Array<number> = [85, 90, 78];
let items: Array<string> = ["りんご", "みかん"];

// 両方同じ意味！好きな方を使ってOK

// 配列に違う型を入れようとするとエラー
numbers.push("六");  // ❌ エラー！
names.push(123);     // ❌ エラー！`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div><span style="color:#4ec9b0;">number[]</span> = <span style="color:#4ec9b0;">Array&lt;number&gt;</span></div><div style="color:#6a9955;">// どちらも同じ意味</div></div>`}
		/>

		<CodePreview
			title="複合型の配列"
			description="オブジェクトの配列など"
			language="typescript"
			code={`// オブジェクトの配列
let users: { name: string; age: number }[] = [
  { name: "田中", age: 25 },
  { name: "鈴木", age: 30 }
];

// 複数の型を許容する配列
let mixed: (string | number)[] = [1, "two", 3, "four"];

// 読み取り専用の配列
const colors: readonly string[] = ["red", "green", "blue"];
colors.push("yellow");  // ❌ エラー！変更できない`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div style="color:#6a9955;">// readonly = 変更禁止</div><div style="color:#6a9955;">// 安全性が上がる</div></div>`}
		/>
	</section>

	<!-- タプル型 -->
	<section class="mb-10">
		<h2 id="tuple" class="text-xl font-bold mb-4">タプル型（Tuple）</h2>

		<div class="p-6 rounded-xl bg-blue-50 dark:bg-blue-900/20 border border-blue-200 dark:border-blue-800 mb-6">
			<p class="text-blue-800 dark:text-blue-200 mb-4">
				<strong>日常での例え：</strong>決まった順番の書類セット
			</p>
			<div class="text-sm text-blue-700 dark:text-blue-300">
				<p>「申請書セット」= 1枚目が申請書、2枚目が身分証明書、3枚目が写真</p>
				<p class="mt-2">順番と種類が決まっている配列がタプルです</p>
			</div>
		</div>

		<CodePreview
			title="タプルの基本"
			description="要素の順番と型が固定"
			language="typescript"
			code={`// タプル: [型1, 型2, 型3, ...]
let person: [string, number] = ["田中", 25];

// 順番が大事！
person = [25, "田中"];  // ❌ エラー！順番が違う

// 要素へのアクセス
const name = person[0];  // string型
const age = person[1];   // number型

// 実用例: 座標
let point: [number, number] = [10, 20];

// 実用例: キーと値のペア
let entry: [string, number] = ["price", 1000];`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div>[<span style="color:#4ec9b0;">string</span>, <span style="color:#4ec9b0;">number</span>]</div><div style="color:#6a9955;">// 1番目は文字列、2番目は数値</div></div>`}
		/>
	</section>

	<!-- オブジェクト型 -->
	<section class="mb-10">
		<h2 id="object" class="text-xl font-bold mb-4">オブジェクト型</h2>

		<div class="p-6 rounded-xl bg-blue-50 dark:bg-blue-900/20 border border-blue-200 dark:border-blue-800 mb-6">
			<p class="text-blue-800 dark:text-blue-200 mb-4">
				<strong>日常での例え：</strong>項目が決まった申込書
			</p>
			<div class="text-sm text-blue-700 dark:text-blue-300">
				<p>申込書には「名前欄」「住所欄」「電話番号欄」が決まっている</p>
				<p class="mt-2">オブジェクト型も「このプロパティが必要」と決められます</p>
			</div>
		</div>

		<CodePreview
			title="オブジェクト型の定義"
			description="プロパティの型を指定"
			language="typescript"
			code={`// インラインでオブジェクト型を定義
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
user.address;  // ❌ エラー: 'address'は存在しない

// 必須プロパティが足りないとエラー
let badUser: { name: string; age: number } = {
  name: "鈴木"
  // ❌ エラー: 'age'が必要
};`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div style="color:#6a9955;">// オブジェクトの形を定義</div><div style="color:#6a9955;">// 足りない・余分はエラー</div></div>`}
		/>

		<CodePreview
			title="オプショナルと読み取り専用"
			description="? と readonly"
			language="typescript"
			code={`let product: {
  id: number;
  name: string;
  description?: string;  // ? = オプショナル（省略可能）
  readonly price: number;  // readonly = 変更禁止
} = {
  id: 1,
  name: "ノートPC",
  price: 98000
  // descriptionは省略OK
};

// オプショナルプロパティは後から追加OK
product.description = "軽量で高性能";

// readonlyは変更できない
product.price = 88000;  // ❌ エラー！`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div><span style="color:#569cd6;">?</span> = オプショナル</div><div><span style="color:#569cd6;">readonly</span> = 変更禁止</div></div>`}
		/>
	</section>

	<!-- 列挙型 -->
	<section class="mb-10">
		<h2 id="enum" class="text-xl font-bold mb-4">列挙型（Enum）</h2>

		<div class="p-6 rounded-xl bg-blue-50 dark:bg-blue-900/20 border border-blue-200 dark:border-blue-800 mb-6">
			<p class="text-blue-800 dark:text-blue-200 mb-4">
				<strong>日常での例え：</strong>選択肢が決まっているアンケート
			</p>
			<div class="text-sm text-blue-700 dark:text-blue-300">
				<p>「満足度」→ 「とても満足」「満足」「普通」「不満」から選ぶ</p>
				<p class="mt-2">Enumは選択肢を名前付きで定義できます</p>
			</div>
		</div>

		<CodePreview
			title="Enumの基本"
			description="選択肢を定義"
			language="typescript"
			code={`// 数値Enum（デフォルト）
enum Direction {
  Up,     // 0
  Down,   // 1
  Left,   // 2
  Right   // 3
}

let move: Direction = Direction.Up;

// 文字列Enum（こちらがおすすめ）
enum Status {
  Pending = "pending",
  Approved = "approved",
  Rejected = "rejected"
}

let orderStatus: Status = Status.Pending;
console.log(orderStatus);  // "pending"

// 型安全！存在しない値はエラー
orderStatus = "unknown";  // ❌ エラー！`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div><span style="color:#569cd6;">enum</span> Status &#123;</div><div style="padding-left:12px;">Pending = <span style="color:#ce9178;">"pending"</span></div><div>&#125;</div></div>`}
		/>

		<div class="p-4 rounded-lg bg-amber-50 dark:bg-amber-900/20 border border-amber-200 dark:border-amber-800 mb-6">
			<p class="font-semibold text-amber-800 dark:text-amber-200">Enumの代わりにUnion型も使える</p>
			<div class="text-sm text-amber-700 dark:text-amber-300 mt-2">
				<p>最近は <code>type Status = "pending" | "approved" | "rejected"</code> のように</p>
				<p>Union型で書くことも多いです。こちらの方がシンプル！</p>
			</div>
		</div>
	</section>

	<!-- any, unknown, never -->
	<section class="mb-10">
		<h2 id="special" class="text-xl font-bold mb-4">特殊な型</h2>

		<CodePreview
			title="any型"
			description="なんでもOK（非推奨）"
			language="typescript"
			code={`// any: どんな型でもOK
let anything: any = "hello";
anything = 123;      // OK
anything = true;     // OK
anything = { x: 1 }; // OK

// anyは型チェックを無効化する
// TypeScriptの恩恵がなくなるので避けるべき！

// どうしても型がわからない時だけ使う
// JSONパースの結果など`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div style="color:#f14c4c;">⚠️ anyは最終手段！</div><div style="color:#6a9955;">型安全性が失われる</div></div>`}
		/>

		<CodePreview
			title="unknown型"
			description="安全な「なんでもOK」"
			language="typescript"
			code={`// unknown: 何が来るかわからない
let input: unknown = getUserInput();

// unknownはそのままでは使えない
input.toUpperCase();  // ❌ エラー！

// 型チェックしてから使う
if (typeof input === "string") {
  input.toUpperCase();  // ✅ OK！
}

// anyより安全！
// 「何かわからないけど、確認してから使う」`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div><span style="color:#4ec9b0;">unknown</span> = anyの安全版</div><div style="color:#6a9955;">// 使う前に型チェック必須</div></div>`}
		/>

		<CodePreview
			title="never型"
			description="絶対に起きない"
			language="typescript"
			code={`// never: 決して返らない関数
function throwError(message: string): never {
  throw new Error(message);
  // ここには到達しない
}

// 無限ループ
function infiniteLoop(): never {
  while (true) {
    // 永遠に終わらない
  }
}

// 型の絞り込みで残らない場合
type Shape = "circle" | "square";

function getArea(shape: Shape) {
  switch (shape) {
    case "circle": return /* ... */;
    case "square": return /* ... */;
    default:
      // ここに来たら never 型
      const _exhaustive: never = shape;
  }
}`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div><span style="color:#4ec9b0;">never</span> = 絶対に発生しない</div><div style="color:#6a9955;">// エラーや無限ループなど</div></div>`}
		/>
	</section>

	<!-- 型の絞り込み -->
	<section class="mb-10">
		<h2 id="narrowing" class="text-xl font-bold mb-4">型の絞り込み（Type Narrowing）</h2>

		<div class="p-6 rounded-xl bg-blue-50 dark:bg-blue-900/20 border border-blue-200 dark:border-blue-800 mb-6">
			<p class="text-blue-800 dark:text-blue-200 mb-4">
				<strong>日常での例え：</strong>荷物の仕分け
			</p>
			<div class="text-sm text-blue-700 dark:text-blue-300">
				<p>「この荷物は壊れ物？」→ はい → 丁寧に扱う</p>
				<p class="mt-2">条件分岐で型を特定し、適切な処理をします</p>
			</div>
		</div>

		<CodePreview
			title="typeofで絞り込み"
			description="プリミティブ型の判定"
			language="typescript"
			code={`function printValue(value: string | number) {
  // ここではvalueはstring | number

  if (typeof value === "string") {
    // ここではvalueはstring
    console.log(value.toUpperCase());
  } else {
    // ここではvalueはnumber
    console.log(value.toFixed(2));
  }
}

printValue("hello");  // HELLO
printValue(3.14159);  // 3.14`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div style="color:#6a9955;">// typeof で型を判定</div><div style="color:#6a9955;">// TypeScriptが自動で型を絞る</div></div>`}
		/>

		<CodePreview
			title="inで絞り込み"
			description="プロパティの存在チェック"
			language="typescript"
			code={`type Bird = { fly: () => void };
type Fish = { swim: () => void };

function move(animal: Bird | Fish) {
  if ("fly" in animal) {
    // animalはBird
    animal.fly();
  } else {
    // animalはFish
    animal.swim();
  }
}

// "fly"プロパティがあるか？で判定`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div><span style="color:#ce9178;">"property"</span> <span style="color:#569cd6;">in</span> object</div><div style="color:#6a9955;">// プロパティの存在で型を判定</div></div>`}
		/>
	</section>

	<!-- ナビゲーション -->
	<div class="flex justify-between pt-6 border-t border-gray-200 dark:border-gray-700">
		<a href="/ts/basics" class="inline-flex items-center gap-2 px-4 py-2 rounded-lg border border-gray-300 dark:border-gray-600 hover:bg-gray-100 dark:hover:bg-gray-800 transition-colors">
			<svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
				<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 19l-7-7 7-7" />
			</svg>
			前へ：TypeScriptとは
		</a>
		<a href="/ts/interfaces" class="inline-flex items-center gap-2 px-4 py-2 rounded-lg bg-primary-600 text-white hover:bg-primary-700 transition-colors">
			次へ：インターフェース
			<svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
				<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 5l7 7-7 7" />
			</svg>
		</a>
	</div>
</article>
