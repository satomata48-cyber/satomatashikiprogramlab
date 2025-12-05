<script>
	import CodePreview from '$lib/components/CodePreview.svelte';
</script>

<svelte:head>
	<title>JavaScript 非同期処理 | さとまたラボ</title>
</svelte:head>

<article>
	<h1 class="text-3xl font-bold mb-2">非同期処理</h1>
	<p class="text-lg text-gray-600 dark:text-gray-400 mb-8">
		時間のかかる処理を待たずにプログラムを実行する
	</p>

	<section class="mb-10">
		<h2 id="why" class="text-xl font-bold mb-4">非同期処理とは？なぜ必要？</h2>

		<div class="p-6 rounded-xl bg-blue-50 dark:bg-blue-900/20 border border-blue-200 dark:border-blue-800 mb-6">
			<p class="text-blue-800 dark:text-blue-200 mb-4">
				<strong>日常での例え：</strong>レストランの注文
			</p>
			<div class="grid grid-cols-1 md:grid-cols-2 gap-4 text-sm">
				<div class="p-3 bg-white dark:bg-gray-800 rounded-lg">
					<div class="font-semibold text-red-700 dark:text-red-300 mb-2">同期処理（悪い例）</div>
					<p class="text-gray-600 dark:text-gray-400">
						1人の料理ができるまで<br>
						次の人の注文を取らない<br>
						→ 他のお客さんが待ちぼうけ
					</p>
				</div>
				<div class="p-3 bg-white dark:bg-gray-800 rounded-lg">
					<div class="font-semibold text-green-700 dark:text-green-300 mb-2">非同期処理（良い例）</div>
					<p class="text-gray-600 dark:text-gray-400">
						注文だけ先に全員から取る<br>
						できた料理から順番に提供<br>
						→ 効率的！
					</p>
				</div>
			</div>
		</div>

		<div class="p-4 rounded-lg bg-amber-50 dark:bg-amber-900/20 border border-amber-200 dark:border-amber-800 mb-6">
			<p class="font-semibold text-amber-800 dark:text-amber-200">Webページでの問題</p>
			<div class="text-sm text-amber-700 dark:text-amber-300 mt-2">
				<p class="mb-2"><strong>API通信やファイル読み込みは時間がかかる：</strong></p>
				<ul class="list-disc list-inside space-y-1 mb-3">
					<li>同期処理だと、通信が終わるまでページが固まる（フリーズ）</li>
					<li>ボタンも押せない、スクロールもできない</li>
				</ul>
				<p><strong>非同期処理なら：</strong>通信中も他の操作ができる！完了したら結果を受け取る</p>
			</div>
		</div>
	</section>

	<section class="mb-10">
		<h2 id="callback" class="text-xl font-bold mb-4">コールバック関数</h2>

		<CodePreview
			title="setTimeout"
			description="指定時間後に実行"
			language="javascript"
			code={`console.log("開始");

setTimeout(() => {
  console.log("2秒後に実行");
}, 2000);

console.log("終了");

// 出力順:
// "開始"
// "終了"
// "2秒後に実行"  ← 2秒後`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div style="color:#6a9955;">// 実行順序:</div><div>1. "開始"</div><div>2. "終了" <span style="color:#6a9955;">← すぐ実行</span></div><div>3. "2秒後に実行" <span style="color:#6a9955;">← 後から</span></div></div>`}
		/>
	</section>

	<section class="mb-10">
		<h2 id="promise" class="text-xl font-bold mb-4">Promise</h2>

		<div class="p-4 rounded-lg bg-blue-50 dark:bg-blue-900/20 border border-blue-200 dark:border-blue-800 mb-6">
			<p class="font-semibold text-blue-800 dark:text-blue-200 mb-2">「Promise（プロミス）」とは？</p>
			<p class="text-sm text-blue-700 dark:text-blue-300 mb-3">
				「約束」という意味。<strong>「結果は後で届けます」という約束</strong>のこと。<br>
				非同期処理の結果を「待つ」仕組みを提供します。
			</p>
			<p class="text-sm text-blue-700 dark:text-blue-300">
				<strong>3つの状態</strong>：<br>
				・<strong>pending（保留中）</strong>：まだ結果が出ていない<br>
				・<strong>fulfilled（成功）</strong>：処理が成功した → .then() で結果を受け取る<br>
				・<strong>rejected（失敗）</strong>：処理が失敗した → .catch() でエラーを処理
			</p>
		</div>

		<CodePreview
			title="Promiseの基本"
			description="非同期処理の結果を表すオブジェクト"
			language="javascript"
			code={`// Promiseの作成
const promise = new Promise((resolve, reject) => {
  // 非同期処理
  setTimeout(() => {
    const success = true;
    if (success) {
      resolve("成功！");  // 成功時
    } else {
      reject("失敗...");  // 失敗時
    }
  }, 1000);
});

// 結果を受け取る
promise
  .then(result => console.log(result))  // "成功！"
  .catch(error => console.log(error));`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div style="color:#569cd6;">Promise</div><div style="margin-left:10px;">├─ <span style="color:#4ec9b0;">pending</span> (保留中)</div><div style="margin-left:10px;">├─ <span style="color:#4ec9b0;">fulfilled</span> (成功) → .then()</div><div style="margin-left:10px;">└─ <span style="color:#4ec9b0;">rejected</span> (失敗) → .catch()</div></div>`}
		/>

		<CodePreview
			title="Promiseチェーン"
			description="連続した非同期処理"
			language="javascript"
			code={`fetch("https://api.example.com/user")
  .then(response => response.json())  // レスポンスをJSONに
  .then(user => {
    console.log(user.name);
    return fetch("/api/posts?userId=" + user.id);
  })
  .then(response => response.json())  // 次のリクエスト
  .then(posts => console.log(posts))
  .catch(error => console.error(error));  // どこかでエラー`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div style="color:#6a9955;">// .then() をつなげて順番に実行</div><div style="color:#6a9955;">// どこでエラーが起きても .catch() で捕まえる</div></div>`}
		/>
	</section>

	<section class="mb-10">
		<h2 id="async-await" class="text-xl font-bold mb-4">async / await</h2>

		<div class="p-4 rounded-lg bg-blue-50 dark:bg-blue-900/20 border border-blue-200 dark:border-blue-800 mb-6">
			<p class="font-semibold text-blue-800 dark:text-blue-200 mb-2">async / await とは？</p>
			<p class="text-sm text-blue-700 dark:text-blue-300 mb-3">
				Promiseを<strong>もっと読みやすく書くための構文</strong>です。<br>
				.then() の連鎖より、普通のコードのように書けます。
			</p>
			<div class="text-sm text-blue-700 dark:text-blue-300">
				<strong>async</strong>：「この関数は非同期処理をしますよ」と宣言<br>
				<strong>await</strong>：「この処理が終わるまで待って」と指定
			</div>
		</div>

		<CodePreview
			title="基本的な使い方"
			description="Promiseをより直感的に書く"
			language="javascript"
			code={`// async関数の定義
async function fetchUser() {
  // awaitでPromiseの完了を待つ
  const response = await fetch("https://api.example.com/user");
  const user = await response.json();
  return user;
}

// 呼び出し
const user = await fetchUser();
console.log(user.name);`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div style="color:#569cd6;">async</div><div style="margin-left:10px;">関数が Promise を返すことを宣言</div><div style="color:#569cd6;margin-top:8px;">await</div><div style="margin-left:10px;">Promise の完了を待って結果を取得</div></div>`}
		/>

		<CodePreview
			title="エラーハンドリング"
			description="try-catchでエラーを捕捉"
			language="javascript"
			code={`async function fetchData() {
  try {
    const response = await fetch("https://api.example.com/data");

    if (!response.ok) {
      throw new Error("HTTPエラー: " + response.status);
    }

    const data = await response.json();
    return data;

  } catch (error) {
    console.error("エラー発生:", error.message);
    throw error;  // 再スロー（呼び出し元に伝える）
  }
}`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div style="color:#c586c0;">try</div><div style="margin-left:10px;color:#6a9955;">// 正常な処理</div><div style="color:#c586c0;">catch</div><div style="margin-left:10px;color:#6a9955;">// エラー時の処理</div></div>`}
		/>

		<CodePreview
			title="並列実行"
			description="Promise.allで複数を同時に"
			language="javascript"
			code={`async function fetchAll() {
  // 並列で実行（速い！）
  const [users, posts, comments] = await Promise.all([
    fetch("/api/users").then(r => r.json()),
    fetch("/api/posts").then(r => r.json()),
    fetch("/api/comments").then(r => r.json())
  ]);

  return { users, posts, comments };
}

// Promise.allSettled: 全部の結果を取得（失敗も含む）
// Promise.race: 最初に完了したものを取得`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div style="color:#dcdcaa;">Promise.all</div><div style="margin-left:10px;color:#6a9955;">// 全て成功 → 結果の配列</div><div style="margin-left:10px;color:#6a9955;">// 1つでも失敗 → 即エラー</div></div>`}
		/>
	</section>

	<section class="mb-10">
		<h2 id="fetch" class="text-xl font-bold mb-4">fetch API</h2>

		<div class="p-4 rounded-lg bg-blue-50 dark:bg-blue-900/20 border border-blue-200 dark:border-blue-800 mb-6">
			<p class="font-semibold text-blue-800 dark:text-blue-200 mb-2">「fetch API」とは？</p>
			<p class="text-sm text-blue-700 dark:text-blue-300 mb-3">
				サーバーと<strong>HTTP通信</strong>するためのJavaScript標準機能。<br>
				データの取得（GET）、送信（POST）、更新（PUT/PATCH）、削除（DELETE）ができます。
			</p>
			<p class="font-semibold text-blue-800 dark:text-blue-200 mb-2">「API」って何？</p>
			<p class="text-sm text-blue-700 dark:text-blue-300">
				<strong>Application Programming Interface</strong>の略。<br>
				「サーバーとやり取りするための窓口」のこと。<br>
				例：天気APIに「東京の天気を教えて」とリクエスト → 天気情報が返ってくる
			</p>
		</div>

		<CodePreview
			title="GETリクエスト"
			description="データの取得"
			language="javascript"
			code={`// シンプルなGET
const response = await fetch("https://api.example.com/users");
const users = await response.json();

// クエリパラメータ付き
const url = new URL("https://api.example.com/search");
url.searchParams.set("q", "javascript");
url.searchParams.set("limit", "10");

const result = await fetch(url);`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div style="color:#ce9178;">GET /users</div><div style="color:#6a9955;">// → ユーザー一覧を取得</div></div>`}
		/>

		<CodePreview
			title="POSTリクエスト"
			description="データの送信"
			language="javascript"
			code={`const response = await fetch("https://api.example.com/users", {
  method: "POST",
  headers: {
    "Content-Type": "application/json"
  },
  body: JSON.stringify({
    name: "田中太郎",
    email: "tanaka@example.com"
  })
});

const newUser = await response.json();`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div style="color:#ce9178;">POST /users</div><div style="color:#6a9955;">// → 新しいユーザーを作成</div></div>`}
		/>

		<CodePreview
			title="その他のメソッド"
			description="PUT, PATCH, DELETE"
			language="javascript"
			code={`// PUT: 全体を置き換え
await fetch("/api/users/1", {
  method: "PUT",
  headers: { "Content-Type": "application/json" },
  body: JSON.stringify({ name: "新しい名前", email: "new@example.com" })
});

// PATCH: 一部を更新
await fetch("/api/users/1", {
  method: "PATCH",
  headers: { "Content-Type": "application/json" },
  body: JSON.stringify({ name: "更新された名前" })
});

// DELETE: 削除
await fetch("/api/users/1", {
  method: "DELETE"
});`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div><span style="color:#4ec9b0;">PUT</span> - 全体を置き換え</div><div><span style="color:#4ec9b0;">PATCH</span> - 一部を更新</div><div><span style="color:#4ec9b0;">DELETE</span> - 削除</div></div>`}
		/>
	</section>

	<section class="mb-10">
		<h2 id="practical" class="text-xl font-bold mb-4">実践例</h2>

		<CodePreview
			title="データ取得のパターン"
			description="エラーハンドリングとローディング"
			language="javascript"
			code={`async function loadUsers() {
  const container = document.getElementById("users");
  container.innerHTML = "<p>読み込み中...</p>";

  try {
    const response = await fetch("/api/users");

    if (!response.ok) {
      throw new Error("データの取得に失敗しました");
    }

    const users = await response.json();

    container.innerHTML = users
      .map(user => "<div>" + user.name + "</div>")
      .join("");

  } catch (error) {
    container.innerHTML = "<p>エラー: " + error.message + "</p>";
  }
}

loadUsers();`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div style="color:#6a9955;">// 1. ローディング表示</div><div style="color:#6a9955;">// 2. データ取得</div><div style="color:#6a9955;">// 3. 成功 → 表示 / 失敗 → エラー表示</div></div>`}
		/>
	</section>

	<div class="flex justify-between pt-6 border-t border-gray-200 dark:border-gray-700">
		<a href="/js/arrays-objects" class="inline-flex items-center gap-2 px-4 py-2 rounded-lg border border-gray-300 dark:border-gray-600 hover:bg-gray-100 dark:hover:bg-gray-800 transition-colors">
			<svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
				<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 19l-7-7 7-7" />
			</svg>
			前へ：配列とオブジェクト
		</a>
		<a href="/ts/basics" class="inline-flex items-center gap-2 px-4 py-2 rounded-lg bg-primary-600 text-white hover:bg-primary-700 transition-colors">
			次へ：TypeScript
			<svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
				<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 5l7 7-7 7" />
			</svg>
		</a>
	</div>
</article>
