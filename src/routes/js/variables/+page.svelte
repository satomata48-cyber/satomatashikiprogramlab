<script>
	import CodePreview from '$lib/components/CodePreview.svelte';
	import FeatureCard from '$lib/components/FeatureCard.svelte';

	const features = [
		{ icon: '📦', title: '変数・定数', description: 'データを保存して再利用', tag: '基本' },
		{ icon: '🔢', title: 'データ型', description: '文字列、数値、配列、オブジェクト', tag: '基本' },
		{ icon: '⚙️', title: '関数', description: '処理をまとめて再利用可能に', tag: '重要' },
		{ icon: '🔄', title: 'ループ', description: '繰り返し処理を自動化', tag: '基本' },
		{ icon: '🎯', title: 'DOM操作', description: 'HTMLを動的に変更', tag: '重要' },
		{ icon: '🌐', title: '非同期処理', description: 'API通信やファイル読み込み', tag: '応用' }
	];
</script>

<svelte:head>
	<title>JavaScript 変数と型 | さとまたラボ</title>
</svelte:head>

<article>
	<h1 class="text-3xl font-bold mb-2">JavaScript</h1>
	<p class="text-lg text-gray-600 dark:text-gray-400 mb-8">
		Webページに動的な機能を追加するプログラミング言語
	</p>

	<!-- JavaScriptとは -->
	<section class="mb-10">
		<h2 id="what-is" class="text-xl font-bold mb-4">JavaScriptとは？</h2>

		<div class="p-6 rounded-xl bg-blue-50 dark:bg-blue-900/20 border border-blue-200 dark:border-blue-800 mb-6">
			<p class="text-blue-800 dark:text-blue-200 mb-4">
				<strong>日常での例え：</strong>Webページの「脳」
			</p>
			<div class="grid grid-cols-1 md:grid-cols-3 gap-4 text-sm">
				<div class="p-3 bg-white dark:bg-gray-800 rounded-lg">
					<div class="font-semibold text-blue-700 dark:text-blue-300 mb-2">HTML = 骨格</div>
					<p class="text-gray-600 dark:text-gray-400">ページの構造・内容</p>
				</div>
				<div class="p-3 bg-white dark:bg-gray-800 rounded-lg">
					<div class="font-semibold text-blue-700 dark:text-blue-300 mb-2">CSS = 外見</div>
					<p class="text-gray-600 dark:text-gray-400">見た目・デザイン</p>
				</div>
				<div class="p-3 bg-white dark:bg-gray-800 rounded-lg">
					<div class="font-semibold text-blue-700 dark:text-blue-300 mb-2">JavaScript = 脳</div>
					<p class="text-gray-600 dark:text-gray-400">動き・判断・処理</p>
				</div>
			</div>
		</div>

		<div class="p-4 rounded-lg bg-amber-50 dark:bg-amber-900/20 border border-amber-200 dark:border-amber-800 mb-6">
			<p class="font-semibold text-amber-800 dark:text-amber-200">なぜJavaScriptが必要？</p>
			<div class="text-sm text-amber-700 dark:text-amber-300 mt-2">
				<p class="mb-2"><strong>HTMLとCSSだけでは：</strong></p>
				<ul class="list-disc list-inside space-y-1 mb-3">
					<li>ボタンを押しても何も起きない（見た目が変わるだけ）</li>
					<li>入力内容のチェックができない</li>
					<li>サーバーと通信できない（データの取得・送信）</li>
				</ul>
				<p><strong>JavaScriptがあると：</strong>ユーザーの操作に反応して、ページの内容を動的に変えられる！</p>
			</div>
		</div>
	</section>

	<!-- できること一覧 -->
	<section class="mb-10">
		<h2 id="features" class="text-xl font-bold mb-4">JavaScriptでできること</h2>
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
			title="変数の宣言"
			description="let、const、varの違い"
			language="javascript"
			code={`// 変更可能な変数
let count = 0;
count = 10;

// 変更不可の定数
const PI = 3.14159;

// 古い書き方（非推奨）
var oldStyle = "使わない";

console.log(count);  // 10
console.log(PI);     // 3.14159`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div><span style="color:#9cdcfe;">count</span> = <span style="color:#b5cea8;">10</span></div><div><span style="color:#9cdcfe;">PI</span> = <span style="color:#b5cea8;">3.14159</span></div></div>`}
		/>

		<CodePreview
			title="データ型"
			description="JavaScriptの基本的な型"
			language="javascript"
			code={`// 文字列
const name = "田中太郎";

// 数値
const age = 25;
const price = 1980.5;

// 真偽値
const isStudent = true;

// 配列
const fruits = ["りんご", "バナナ", "オレンジ"];

// オブジェクト
const user = {
  name: "田中",
  age: 25,
  email: "tanaka@example.com"
};`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div><span style="color:#ce9178;">"田中太郎"</span> → 文字列</div><div><span style="color:#b5cea8;">25</span> → 数値</div><div><span style="color:#569cd6;">true</span> → 真偽値</div><div><span style="color:#9cdcfe;">["りんご", ...]</span> → 配列</div><div><span style="color:#9cdcfe;">&#123;name: ...&#125;</span> → オブジェクト</div></div>`}
		/>

		<CodePreview
			title="関数"
			description="処理をまとめる"
			language="javascript"
			code={`// 関数宣言
function greet(name) {
  return "こんにちは、" + name + "さん！";
}

// アロー関数（モダンな書き方）
const add = (a, b) => a + b;

// 使用例
console.log(greet("田中"));  // こんにちは、田中さん！
console.log(add(5, 3));      // 8`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div><span style="color:#dcdcaa;">greet</span>(<span style="color:#ce9178;">"田中"</span>) → <span style="color:#ce9178;">"こんにちは、田中さん！"</span></div><div><span style="color:#dcdcaa;">add</span>(<span style="color:#b5cea8;">5</span>, <span style="color:#b5cea8;">3</span>) → <span style="color:#b5cea8;">8</span></div></div>`}
		/>

		<CodePreview
			title="条件分岐"
			description="if文で処理を分ける"
			language="javascript"
			code={`const score = 85;

if (score >= 90) {
  console.log("優秀！");
} else if (score >= 70) {
  console.log("合格！");
} else {
  console.log("もう少し頑張ろう");
}

// 三項演算子
const result = score >= 70 ? "合格" : "不合格";`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div>score = 85 の場合:</div><div style="color:#6a9955;">// → "合格！"</div><div style="margin-top:8px;">result = <span style="color:#ce9178;">"合格"</span></div></div>`}
		/>

		<CodePreview
			title="ループ"
			description="繰り返し処理"
			language="javascript"
			code={`const fruits = ["りんご", "バナナ", "オレンジ"];

// for...of（配列向け）
for (const fruit of fruits) {
  console.log(fruit);
}

// forEach（メソッド形式）
fruits.forEach((fruit, index) => {
  console.log(index + ": " + fruit);
});

// map（変換して新配列を作成）
const upperFruits = fruits.map(f => f.toUpperCase());`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div>for...of 出力:</div><div style="color:#ce9178;margin-left:10px;">りんご<br>バナナ<br>オレンジ</div></div>`}
		/>

		<CodePreview
			title="DOM操作"
			description="HTMLを動的に変更"
			language="javascript"
			code={`// 要素を取得
const button = document.querySelector("#myButton");
const title = document.getElementById("title");

// 内容を変更
title.textContent = "新しいタイトル";

// クリックイベント
button.addEventListener("click", () => {
  alert("クリックされました！");
});

// 要素を追加
const newDiv = document.createElement("div");
newDiv.textContent = "新しい要素";
document.body.appendChild(newDiv);`}
			previewHtml={`<div style="background:#f3f4f6;padding:12px;border-radius:6px;"><button style="padding:8px 16px;background:#3b82f6;color:white;border:none;border-radius:4px;cursor:pointer;" onclick="alert('クリックされました！')">クリックしてみて</button></div>`}
		/>

		<CodePreview
			title="非同期処理"
			description="async/awaitでAPI通信"
			language="javascript"
			code={`// 非同期関数
async function fetchData() {
  try {
    const response = await fetch("https://api.example.com/data");
    const data = await response.json();
    console.log(data);
  } catch (error) {
    console.error("エラー:", error);
  }
}

// 呼び出し
fetchData();`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div style="color:#6a9955;">// API通信は非同期で実行</div><div style="color:#6a9955;">// 完了を待ってからデータを処理</div></div>`}
		/>
	</section>

	<!-- ナビゲーション -->
	<div class="flex justify-between pt-6 border-t border-gray-200 dark:border-gray-700">
		<a href="/css/selectors" class="inline-flex items-center gap-2 px-4 py-2 rounded-lg border border-gray-300 dark:border-gray-600 hover:bg-gray-100 dark:hover:bg-gray-800 transition-colors">
			<svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
				<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 19l-7-7 7-7" />
			</svg>
			前へ：CSS
		</a>
		<a href="/js/functions" class="inline-flex items-center gap-2 px-4 py-2 rounded-lg bg-primary-600 text-white hover:bg-primary-700 transition-colors">
			次へ：関数
			<svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
				<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 5l7 7-7 7" />
			</svg>
		</a>
	</div>
</article>
