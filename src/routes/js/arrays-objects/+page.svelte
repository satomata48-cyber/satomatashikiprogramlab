<script>
	import CodePreview from '$lib/components/CodePreview.svelte';
</script>

<svelte:head>
	<title>JavaScript 配列とオブジェクト | さとまたラボ</title>
</svelte:head>

<article>
	<h1 class="text-3xl font-bold mb-2">配列とオブジェクト</h1>
	<p class="text-lg text-gray-600 dark:text-gray-400 mb-8">
		複数のデータをまとめて管理する
	</p>

	<!-- 配列とオブジェクトとは -->
	<section class="mb-10">
		<h2 id="what-is" class="text-xl font-bold mb-4">配列とオブジェクトとは？</h2>

		<div class="p-6 rounded-xl bg-blue-50 dark:bg-blue-900/20 border border-blue-200 dark:border-blue-800 mb-6">
			<p class="text-blue-800 dark:text-blue-200 mb-4">
				<strong>日常での例え</strong>
			</p>
			<div class="grid grid-cols-1 md:grid-cols-2 gap-4 text-sm">
				<div class="p-3 bg-white dark:bg-gray-800 rounded-lg">
					<div class="font-semibold text-blue-700 dark:text-blue-300 mb-2">配列 = 番号付きロッカー</div>
					<p class="text-gray-600 dark:text-gray-400">
						「1番に〇〇、2番に△△...」<br>
						順番が大事な時に使う
					</p>
				</div>
				<div class="p-3 bg-white dark:bg-gray-800 rounded-lg">
					<div class="font-semibold text-blue-700 dark:text-blue-300 mb-2">オブジェクト = 名前付きロッカー</div>
					<p class="text-gray-600 dark:text-gray-400">
						「名前に〇〇、年齢に△△...」<br>
						意味のある名前で管理したい時
					</p>
				</div>
			</div>
		</div>

		<div class="p-4 rounded-lg bg-amber-50 dark:bg-amber-900/20 border border-amber-200 dark:border-amber-800 mb-6">
			<p class="font-semibold text-amber-800 dark:text-amber-200">なぜ配列とオブジェクトが必要？</p>
			<div class="text-sm text-amber-700 dark:text-amber-300 mt-2">
				<p class="mb-2"><strong>個別の変数だけだと：</strong></p>
				<ul class="list-disc list-inside space-y-1 mb-3">
					<li>100人のユーザーに100個の変数が必要 → 管理が大変</li>
					<li>「全員の名前を表示」のような一括処理ができない</li>
				</ul>
				<p><strong>配列/オブジェクトを使うと：</strong>まとめて管理、一括処理、追加・削除も簡単！</p>
			</div>
		</div>
	</section>

	<section class="mb-10">
		<h2 id="array-basic" class="text-xl font-bold mb-4">配列の基本</h2>

		<CodePreview
			title="配列の作成とアクセス"
			description="[]で作成、インデックスでアクセス"
			language="javascript"
			code={`// 配列の作成
const fruits = ["りんご", "バナナ", "オレンジ"];

// インデックスでアクセス（0から始まる）
fruits[0];  // "りんご"
fruits[1];  // "バナナ"
fruits[2];  // "オレンジ"

// 長さ
fruits.length;  // 3

// 要素の変更
fruits[1] = "ぶどう";`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div>fruits[0] <span style="color:#6a9955;">// → "りんご"</span></div><div>fruits[1] <span style="color:#6a9955;">// → "バナナ"</span></div><div>fruits.length <span style="color:#6a9955;">// → 3</span></div></div>`}
		/>

		<CodePreview
			title="配列の操作メソッド"
			description="追加・削除・検索"
			language="javascript"
			code={`const arr = [1, 2, 3];

// 末尾に追加
arr.push(4);        // [1, 2, 3, 4]

// 末尾から削除
arr.pop();          // [1, 2, 3]

// 先頭に追加
arr.unshift(0);     // [0, 1, 2, 3]

// 先頭から削除
arr.shift();        // [1, 2, 3]

// 含まれているか
arr.includes(2);    // true

// インデックスを取得
arr.indexOf(2);     // 1`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div>.push(4) <span style="color:#6a9955;">// 末尾に追加</span></div><div>.pop() <span style="color:#6a9955;">// 末尾を削除</span></div><div>.includes(2) <span style="color:#6a9955;">// → true</span></div><div>.indexOf(2) <span style="color:#6a9955;">// → 1</span></div></div>`}
		/>

		<CodePreview
			title="配列の変換メソッド"
			description="map, filter, reduce"
			language="javascript"
			code={`const numbers = [1, 2, 3, 4, 5];

// map: 各要素を変換して新配列を作成
const doubled = numbers.map(n => n * 2);
// [2, 4, 6, 8, 10]

// filter: 条件に合う要素だけ抽出
const evens = numbers.filter(n => n % 2 === 0);
// [2, 4]

// reduce: 1つの値にまとめる
const sum = numbers.reduce((acc, n) => acc + n, 0);
// 15

// チェーン（連結）できる
const result = numbers
  .filter(n => n > 2)
  .map(n => n * 10);
// [30, 40, 50]`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div>.map(n => n * 2) <span style="color:#6a9955;">// [2, 4, 6, 8, 10]</span></div><div>.filter(n => n % 2 === 0) <span style="color:#6a9955;">// [2, 4]</span></div><div>.reduce((acc, n) => acc + n, 0) <span style="color:#6a9955;">// 15</span></div></div>`}
		/>
	</section>

	<section class="mb-10">
		<h2 id="object-basic" class="text-xl font-bold mb-4">オブジェクトの基本</h2>

		<CodePreview
			title="オブジェクトの作成とアクセス"
			description="キーと値のペア"
			language="javascript"
			code={`// オブジェクトの作成
const user = {
  name: "田中太郎",
  age: 25,
  email: "tanaka@example.com"
};

// ドット記法でアクセス
user.name;   // "田中太郎"
user.age;    // 25

// ブラケット記法（変数キーに便利）
user["email"];  // "tanaka@example.com"
const key = "name";
user[key];      // "田中太郎"

// プロパティの追加・変更
user.city = "東京";
user.age = 26;`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div>user.name <span style="color:#6a9955;">// → "田中太郎"</span></div><div>user.age <span style="color:#6a9955;">// → 25</span></div><div>user["email"] <span style="color:#6a9955;">// → "tanaka@example.com"</span></div></div>`}
		/>

		<CodePreview
			title="オブジェクトのメソッド"
			description="Object.keys, values, entries"
			language="javascript"
			code={`const user = { name: "田中", age: 25, city: "東京" };

// キーの配列
Object.keys(user);
// ["name", "age", "city"]

// 値の配列
Object.values(user);
// ["田中", 25, "東京"]

// [キー, 値] の配列
Object.entries(user);
// [["name", "田中"], ["age", 25], ["city", "東京"]]

// プロパティの存在確認
"name" in user;           // true
user.hasOwnProperty("age"); // true`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div>Object.keys(user) <span style="color:#6a9955;">// ["name", "age", "city"]</span></div><div>Object.values(user) <span style="color:#6a9955;">// ["田中", 25, "東京"]</span></div><div>"name" in user <span style="color:#6a9955;">// true</span></div></div>`}
		/>
	</section>

	<section class="mb-10">
		<h2 id="spread" class="text-xl font-bold mb-4">スプレッド構文</h2>

		<div class="p-4 rounded-lg bg-blue-50 dark:bg-blue-900/20 border border-blue-200 dark:border-blue-800 mb-6">
			<p class="font-semibold text-blue-800 dark:text-blue-200 mb-2">「スプレッド構文（...）」とは？</p>
			<p class="text-sm text-blue-700 dark:text-blue-300">
				配列やオブジェクトを<strong>展開（バラバラにする）</strong>記号。<br>
				「箱の中身を取り出して並べる」イメージです。<br>
				配列のコピー、結合、オブジェクトのマージに使います。
			</p>
		</div>

		<CodePreview
			title="配列のスプレッド"
			description="...で展開・コピー"
			language="javascript"
			code={`const arr1 = [1, 2, 3];
const arr2 = [4, 5, 6];

// 配列の結合
const combined = [...arr1, ...arr2];
// [1, 2, 3, 4, 5, 6]

// 配列のコピー
const copy = [...arr1];

// 途中に挿入
const inserted = [0, ...arr1, 4];
// [0, 1, 2, 3, 4]`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div>[...arr1, ...arr2] <span style="color:#6a9955;">// [1, 2, 3, 4, 5, 6]</span></div><div>[0, ...arr1, 4] <span style="color:#6a9955;">// [0, 1, 2, 3, 4]</span></div></div>`}
		/>

		<CodePreview
			title="オブジェクトのスプレッド"
			description="マージやコピー"
			language="javascript"
			code={`const defaults = { theme: "light", lang: "ja" };
const settings = { theme: "dark" };

// オブジェクトのマージ（後から上書き）
const merged = { ...defaults, ...settings };
// { theme: "dark", lang: "ja" }

// プロパティの追加
const updated = { ...defaults, fontSize: 16 };

// 一部を変更したコピー
const newSettings = { ...settings, lang: "en" };`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div style="color:#6a9955;">// defaults を settings で上書きマージ</div><div>&#123; ...defaults, ...settings &#125;</div><div style="color:#6a9955;">// → &#123; theme: "dark", lang: "ja" &#125;</div></div>`}
		/>
	</section>

	<section class="mb-10">
		<h2 id="destructuring" class="text-xl font-bold mb-4">分割代入</h2>

		<div class="p-4 rounded-lg bg-blue-50 dark:bg-blue-900/20 border border-blue-200 dark:border-blue-800 mb-6">
			<p class="font-semibold text-blue-800 dark:text-blue-200 mb-2">「分割代入」とは？</p>
			<p class="text-sm text-blue-700 dark:text-blue-300">
				配列やオブジェクトから<strong>必要な値だけを取り出す</strong>構文。<br>
				「箱から特定のものだけ取り出して、変数に入れる」イメージです。
			</p>
		</div>

		<CodePreview
			title="配列の分割代入"
			description="配列から変数に展開"
			language="javascript"
			code={`const colors = ["red", "green", "blue"];

// 分割代入
const [first, second, third] = colors;
// first = "red", second = "green", third = "blue"

// 一部だけ取得
const [primary, , tertiary] = colors;
// primary = "red", tertiary = "blue"

// 残りをまとめる
const [head, ...rest] = colors;
// head = "red", rest = ["green", "blue"]`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div>const [first, second] = colors</div><div style="color:#6a9955;">// first = "red", second = "green"</div></div>`}
		/>

		<CodePreview
			title="オブジェクトの分割代入"
			description="プロパティを変数に展開"
			language="javascript"
			code={`const user = {
  name: "田中",
  age: 25,
  email: "tanaka@example.com"
};

// 分割代入
const { name, age } = user;
// name = "田中", age = 25

// 別名をつける
const { name: userName } = user;
// userName = "田中"

// デフォルト値
const { city = "不明" } = user;
// city = "不明"

// 関数の引数で使う
function greet({ name, age }) {
  console.log(name + "は" + age + "歳");
}`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div>const &#123; name, age &#125; = user</div><div style="color:#6a9955;">// name = "田中", age = 25</div></div>`}
		/>
	</section>

	<section class="mb-10">
		<h2 id="json" class="text-xl font-bold mb-4">JSON</h2>

		<div class="p-4 rounded-lg bg-blue-50 dark:bg-blue-900/20 border border-blue-200 dark:border-blue-800 mb-6">
			<p class="font-semibold text-blue-800 dark:text-blue-200 mb-2">「JSON（ジェイソン）」とは？</p>
			<p class="text-sm text-blue-700 dark:text-blue-300 mb-3">
				<strong>JavaScript Object Notation</strong>の略。<br>
				データをやり取りするための「共通フォーマット」です。
			</p>
			<p class="font-semibold text-blue-800 dark:text-blue-200 mb-2">なぜJSONが必要？</p>
			<p class="text-sm text-blue-700 dark:text-blue-300">
				サーバーとブラウザでデータをやり取りする時、<br>
				「文字列」にしないと送れない → JSONで文字列に変換！<br>
				受け取った後は、オブジェクトに戻して使う。
			</p>
		</div>

		<CodePreview
			title="JSON変換"
			description="文字列とオブジェクトの相互変換"
			language="javascript"
			code={`const user = { name: "田中", age: 25 };

// オブジェクト → JSON文字列
const jsonString = JSON.stringify(user);
// '{"name":"田中","age":25}'

// 整形して出力
JSON.stringify(user, null, 2);
// {
//   "name": "田中",
//   "age": 25
// }

// JSON文字列 → オブジェクト
const parsed = JSON.parse(jsonString);
// { name: "田中", age: 25 }`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div>JSON.stringify(user)</div><div style="color:#ce9178;">'&#123;"name":"田中","age":25&#125;'</div><div style="margin-top:8px;">JSON.parse(jsonString)</div><div style="color:#6a9955;">// → オブジェクトに戻る</div></div>`}
		/>
	</section>

	<div class="flex justify-between pt-6 border-t border-gray-200 dark:border-gray-700">
		<a href="/js/functions" class="inline-flex items-center gap-2 px-4 py-2 rounded-lg border border-gray-300 dark:border-gray-600 hover:bg-gray-100 dark:hover:bg-gray-800 transition-colors">
			<svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
				<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 19l-7-7 7-7" />
			</svg>
			前へ：関数
		</a>
		<a href="/js/async" class="inline-flex items-center gap-2 px-4 py-2 rounded-lg bg-primary-600 text-white hover:bg-primary-700 transition-colors">
			次へ：非同期処理
			<svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
				<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 5l7 7-7 7" />
			</svg>
		</a>
	</div>
</article>
