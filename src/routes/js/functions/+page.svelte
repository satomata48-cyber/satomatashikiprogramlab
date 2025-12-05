<script>
	import CodePreview from '$lib/components/CodePreview.svelte';
</script>

<svelte:head>
	<title>JavaScript 関数 | さとまたラボ</title>
</svelte:head>

<article>
	<h1 class="text-3xl font-bold mb-2">関数</h1>
	<p class="text-lg text-gray-600 dark:text-gray-400 mb-8">
		処理をまとめて再利用可能にする
	</p>

	<!-- 関数とは -->
	<section class="mb-10">
		<h2 id="what-is" class="text-xl font-bold mb-4">関数とは？</h2>

		<div class="p-6 rounded-xl bg-blue-50 dark:bg-blue-900/20 border border-blue-200 dark:border-blue-800 mb-6">
			<p class="text-blue-800 dark:text-blue-200 mb-4">
				<strong>日常での例え：</strong>自動販売機
			</p>
			<div class="text-sm text-blue-700 dark:text-blue-300 space-y-2">
				<p><strong>入力（引数）</strong>：お金とボタン選択</p>
				<p><strong>処理</strong>：飲み物を出す</p>
				<p><strong>出力（戻り値）</strong>：選んだ飲み物</p>
				<p class="mt-3">関数は「決まった処理をして結果を返す箱」のようなもの</p>
			</div>
		</div>

		<div class="p-4 rounded-lg bg-amber-50 dark:bg-amber-900/20 border border-amber-200 dark:border-amber-800 mb-6">
			<p class="font-semibold text-amber-800 dark:text-amber-200">なぜ関数が必要？</p>
			<div class="text-sm text-amber-700 dark:text-amber-300 mt-2">
				<p class="mb-2"><strong>同じ処理を何度も書くと：</strong></p>
				<ul class="list-disc list-inside space-y-1 mb-3">
					<li>コードが長くなって読みにくい</li>
					<li>修正が必要な時、全箇所を直す必要がある</li>
					<li>バグが入りやすい</li>
				</ul>
				<p><strong>関数にまとめると：</strong>1箇所に書いて、何度でも呼び出せる！修正も1箇所だけでOK</p>
			</div>
		</div>
	</section>

	<section class="mb-10">
		<h2 id="declaration" class="text-xl font-bold mb-4">関数の宣言</h2>

		<CodePreview
			title="関数宣言"
			description="functionキーワードで定義"
			language="javascript"
			code={`// 基本的な関数宣言
function greet(name) {
  return "こんにちは、" + name + "さん！";
}

// 呼び出し
const message = greet("田中");
console.log(message); // "こんにちは、田中さん！"`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div><span style="color:#dcdcaa;">greet</span>(<span style="color:#ce9178;">"田中"</span>)</div><div style="color:#6a9955;">// → "こんにちは、田中さん！"</div></div>`}
		/>

		<CodePreview
			title="関数式"
			description="変数に代入する形式"
			language="javascript"
			code={`// 関数式
const add = function(a, b) {
  return a + b;
};

// 即座に実行
console.log(add(5, 3)); // 8`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div><span style="color:#dcdcaa;">add</span>(<span style="color:#b5cea8;">5</span>, <span style="color:#b5cea8;">3</span>)</div><div style="color:#6a9955;">// → 8</div></div>`}
		/>

		<CodePreview
			title="アロー関数"
			description="モダンで簡潔な書き方"
			language="javascript"
			code={`// 基本形
const multiply = (a, b) => {
  return a * b;
};

// 1行なら return 省略可
const multiply2 = (a, b) => a * b;

// 引数1つなら () 省略可
const double = n => n * 2;

// 引数なし
const sayHello = () => "Hello!";`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div><span style="color:#9cdcfe;">multiply</span>(4, 5) <span style="color:#6a9955;">// → 20</span></div><div><span style="color:#9cdcfe;">double</span>(7) <span style="color:#6a9955;">// → 14</span></div><div><span style="color:#9cdcfe;">sayHello</span>() <span style="color:#6a9955;">// → "Hello!"</span></div></div>`}
		/>
	</section>

	<section class="mb-10">
		<h2 id="parameters" class="text-xl font-bold mb-4">引数と戻り値</h2>

		<CodePreview
			title="デフォルト引数"
			description="引数が省略された時の初期値"
			language="javascript"
			code={`function greet(name = "ゲスト") {
  return "こんにちは、" + name + "さん！";
}

greet();        // "こんにちは、ゲストさん！"
greet("田中");  // "こんにちは、田中さん！"`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div><span style="color:#dcdcaa;">greet</span>() <span style="color:#6a9955;">// → "こんにちは、ゲストさん！"</span></div><div><span style="color:#dcdcaa;">greet</span>(<span style="color:#ce9178;">"田中"</span>) <span style="color:#6a9955;">// → "こんにちは、田中さん！"</span></div></div>`}
		/>

		<CodePreview
			title="残余引数（Rest Parameters）"
			description="可変長の引数を配列で受け取る"
			language="javascript"
			code={`function sum(...numbers) {
  return numbers.reduce((total, n) => total + n, 0);
}

sum(1, 2);           // 3
sum(1, 2, 3, 4, 5);  // 15`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div><span style="color:#dcdcaa;">sum</span>(1, 2) <span style="color:#6a9955;">// → 3</span></div><div><span style="color:#dcdcaa;">sum</span>(1, 2, 3, 4, 5) <span style="color:#6a9955;">// → 15</span></div></div>`}
		/>

		<CodePreview
			title="分割代入（オブジェクト引数）"
			description="オブジェクトのプロパティを展開"
			language="javascript"
			code={`// 引数をオブジェクトで受け取る
function createUser({ name, age, email }) {
  return { name, age, email, createdAt: new Date() };
}

// 呼び出し
createUser({
  name: "田中",
  age: 25,
  email: "tanaka@example.com"
});`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div style="color:#6a9955;">// オブジェクトで引数を渡すと</div><div style="color:#6a9955;">// 順番を気にしなくて良い</div></div>`}
		/>
	</section>

	<section class="mb-10">
		<h2 id="callback" class="text-xl font-bold mb-4">コールバック関数</h2>

		<div class="p-4 rounded-lg bg-blue-50 dark:bg-blue-900/20 border border-blue-200 dark:border-blue-800 mb-6">
			<p class="font-semibold text-blue-800 dark:text-blue-200 mb-2">コールバック関数とは？</p>
			<p class="text-sm text-blue-700 dark:text-blue-300 mb-3">
				「後で呼び出してもらう関数」のこと。<br>
				ある処理が終わった後に「これを実行して」と渡しておく関数です。
			</p>
			<p class="text-sm text-blue-700 dark:text-blue-300">
				<strong>例</strong>：配列の各要素に対して「この処理をして」と関数を渡す
			</p>
		</div>

		<CodePreview
			title="関数を引数として渡す"
			description="他の関数に処理を委ねる"
			language="javascript"
			code={`// 関数を引数に取る関数
function processArray(arr, callback) {
  const result = [];
  for (const item of arr) {
    result.push(callback(item));
  }
  return result;
}

// 使用例
const numbers = [1, 2, 3, 4, 5];
const doubled = processArray(numbers, n => n * 2);
// [2, 4, 6, 8, 10]`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div>numbers = [1, 2, 3, 4, 5]</div><div>callback = n => n * 2</div><div style="color:#6a9955;">// → [2, 4, 6, 8, 10]</div></div>`}
		/>

		<CodePreview
			title="配列メソッドでのコールバック"
			description="map, filter, reduce など"
			language="javascript"
			code={`const numbers = [1, 2, 3, 4, 5];

// map: 各要素を変換
numbers.map(n => n * 2);     // [2, 4, 6, 8, 10]

// filter: 条件に合う要素を抽出
numbers.filter(n => n > 2);  // [3, 4, 5]

// find: 条件に合う最初の要素
numbers.find(n => n > 3);    // 4

// reduce: 1つの値に集約
numbers.reduce((sum, n) => sum + n, 0); // 15`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div>.map(n => n * 2) <span style="color:#6a9955;">// [2, 4, 6, 8, 10]</span></div><div>.filter(n => n > 2) <span style="color:#6a9955;">// [3, 4, 5]</span></div><div>.find(n => n > 3) <span style="color:#6a9955;">// 4</span></div><div>.reduce((sum, n) => sum + n, 0) <span style="color:#6a9955;">// 15</span></div></div>`}
		/>
	</section>

	<section class="mb-10">
		<h2 id="scope" class="text-xl font-bold mb-4">スコープとクロージャ</h2>

		<div class="p-4 rounded-lg bg-blue-50 dark:bg-blue-900/20 border border-blue-200 dark:border-blue-800 mb-6">
			<p class="font-semibold text-blue-800 dark:text-blue-200 mb-2">「スコープ」とは？</p>
			<p class="text-sm text-blue-700 dark:text-blue-300 mb-3">
				変数が「見える範囲」のこと。<br>
				関数の中で作った変数は、その関数の中でしか使えない（他から見えない）。
			</p>
			<p class="font-semibold text-blue-800 dark:text-blue-200 mb-2">「クロージャ」とは？</p>
			<p class="text-sm text-blue-700 dark:text-blue-300">
				関数が「外側の変数を覚えている」仕組み。<br>
				これを使うと、関数の中だけで使える「プライベートな変数」が作れる。
			</p>
		</div>

		<CodePreview
			title="スコープ"
			description="変数の有効範囲"
			language="javascript"
			code={`const globalVar = "グローバル";

function outer() {
  const outerVar = "outer";

  function inner() {
    const innerVar = "inner";
    console.log(globalVar); // OK
    console.log(outerVar);  // OK
    console.log(innerVar);  // OK
  }

  console.log(innerVar);  // エラー！
}`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div style="color:#6a9955;">// 内側から外側は参照OK</div><div style="color:#6a9955;">// 外側から内側は参照NG</div></div>`}
		/>

		<CodePreview
			title="クロージャ"
			description="外部スコープの変数を記憶"
			language="javascript"
			code={`function createCounter() {
  let count = 0;  // プライベート変数

  return {
    increment() { count++; },
    decrement() { count--; },
    getCount() { return count; }
  };
}

const counter = createCounter();
counter.increment();
counter.increment();
counter.getCount(); // 2`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div>counter.increment()</div><div>counter.increment()</div><div>counter.getCount() <span style="color:#6a9955;">// → 2</span></div></div>`}
		/>
	</section>

	<div class="flex justify-between pt-6 border-t border-gray-200 dark:border-gray-700">
		<a href="/js/variables" class="inline-flex items-center gap-2 px-4 py-2 rounded-lg border border-gray-300 dark:border-gray-600 hover:bg-gray-100 dark:hover:bg-gray-800 transition-colors">
			<svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
				<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 19l-7-7 7-7" />
			</svg>
			前へ：変数と型
		</a>
		<a href="/js/arrays-objects" class="inline-flex items-center gap-2 px-4 py-2 rounded-lg bg-primary-600 text-white hover:bg-primary-700 transition-colors">
			次へ：配列とオブジェクト
			<svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
				<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 5l7 7-7 7" />
			</svg>
		</a>
	</div>
</article>
