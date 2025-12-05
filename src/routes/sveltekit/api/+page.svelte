<script>
	import CodePreview from '$lib/components/CodePreview.svelte';
</script>

<svelte:head>
	<title>SvelteKit APIエンドポイント | さとまたラボ</title>
</svelte:head>

<article>
	<h1 class="text-3xl font-bold mb-2">APIエンドポイント</h1>
	<p class="text-lg text-gray-600 dark:text-gray-400 mb-8">
		+server.ts でバックエンドAPIを作る
	</p>

	<!-- APIエンドポイントとは -->
	<section class="mb-10">
		<h2 id="what-is" class="text-xl font-bold mb-4">APIエンドポイントとは？</h2>

		<div class="p-6 rounded-xl bg-blue-50 dark:bg-blue-900/20 border border-blue-200 dark:border-blue-800 mb-6">
			<p class="text-blue-800 dark:text-blue-200 mb-4">
				<strong>日常での例え：</strong>レストランの厨房への注文窓口
			</p>
			<div class="grid grid-cols-1 md:grid-cols-2 gap-4 text-sm">
				<div class="p-3 bg-white dark:bg-gray-800 rounded-lg">
					<div class="font-semibold text-blue-700 dark:text-blue-300 mb-2">注文窓口</div>
					<p class="text-gray-600 dark:text-gray-400">
						お客さん（フロントエンド）が<br>
						「カレーください」と注文<br>
						→ 厨房が調理して提供
					</p>
				</div>
				<div class="p-3 bg-white dark:bg-gray-800 rounded-lg">
					<div class="font-semibold text-blue-700 dark:text-blue-300 mb-2">APIエンドポイント</div>
					<p class="text-gray-600 dark:text-gray-400">
						クライアントが<br>
						「/api/users」にリクエスト<br>
						→ サーバーがデータを返す
					</p>
				</div>
			</div>
		</div>

		<div class="p-4 rounded-lg bg-amber-50 dark:bg-amber-900/20 border border-amber-200 dark:border-amber-800 mb-6">
			<p class="font-semibold text-amber-800 dark:text-amber-200">なぜAPIエンドポイントが必要？</p>
			<div class="text-sm text-amber-700 dark:text-amber-300 mt-2">
				<p class="mb-2"><strong>APIエンドポイントがないと困ること：</strong></p>
				<ul class="list-disc list-inside space-y-1 mb-3">
					<li>データベースに直接アクセス？→ セキュリティ的に危険すぎる</li>
					<li>外部サービス（決済など）の呼び出し→ APIキーが丸見えになる</li>
					<li>サーバーでしかできない処理が実行できない</li>
				</ul>
				<p><strong>APIエンドポイントがあれば：</strong>安全にデータのやり取りができる！<br>
				機密情報はサーバー側に隠したまま処理できます。</p>
			</div>
		</div>

		<div class="p-4 rounded-lg bg-green-50 dark:bg-green-900/20 border border-green-200 dark:border-green-800 mb-6">
			<p class="font-semibold text-green-800 dark:text-green-200">SvelteKitの良いところ</p>
			<p class="text-sm text-green-700 dark:text-green-300 mt-2">
				フロントエンドとバックエンドが<strong>同じプロジェクト</strong>で書ける！<br>
				別のサーバーを用意する必要がありません。
			</p>
		</div>

		<div class="p-4 rounded-lg bg-gray-100 dark:bg-gray-800 mb-6">
			<p class="font-semibold text-gray-800 dark:text-gray-200 mb-2">用語解説</p>
			<div class="text-sm text-gray-700 dark:text-gray-300 space-y-2">
				<p><strong>API</strong>：アプリケーション同士がデータをやり取りするための窓口。</p>
				<p><strong>エンドポイント</strong>：APIの「住所」のこと。例：<code>/api/users</code></p>
				<p><strong>GET</strong>：データを「取得」する時のリクエスト方法。</p>
				<p><strong>POST</strong>：データを「送信・作成」する時のリクエスト方法。</p>
				<p><strong>PUT / PATCH</strong>：データを「更新」する時のリクエスト方法。</p>
				<p><strong>DELETE</strong>：データを「削除」する時のリクエスト方法。</p>
				<p><strong>JSON</strong>：データ交換用の形式。<code>&#123;"name": "太郎", "age": 20&#125;</code> のような書き方。</p>
				<p><strong>ステータスコード</strong>：リクエストの結果を表す番号。200=成功、404=見つからない、500=サーバーエラー</p>
			</div>
		</div>

		<div class="p-4 rounded-lg bg-gray-100 dark:bg-gray-800 mb-6">
			<p class="font-semibold text-gray-800 dark:text-gray-200 mb-2">+server.ts の場所</p>
			<div class="text-sm text-gray-700 dark:text-gray-300">
				<p><code class="bg-gray-200 dark:bg-gray-700 px-1 rounded">src/routes/api/users/+server.ts</code></p>
				<p class="mt-1">→ <code>/api/users</code> でアクセス可能</p>
			</div>
		</div>
	</section>

	<!-- 基本的なAPI -->
	<section class="mb-10">
		<h2 id="basic" class="text-xl font-bold mb-4">基本的なAPI</h2>

		<CodePreview
			title="GETリクエスト"
			description="データの取得"
			language="typescript"
			code={`// src/routes/api/users/+server.ts
import { json } from '@sveltejs/kit';
import type { RequestHandler } from './$types';

// GET /api/users
export const GET: RequestHandler = async () => {
  const users = [
    { id: 1, name: '田中太郎' },
    { id: 2, name: '鈴木花子' }
  ];

  return json(users);
};

// レスポンス:
// [{"id":1,"name":"田中太郎"},{"id":2,"name":"鈴木花子"}]`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div><span style="color:#ce9178;">GET</span> /api/users</div><div style="color:#6a9955;">// ユーザー一覧を返す</div></div>`}
		/>

		<CodePreview
			title="POSTリクエスト"
			description="データの作成"
			language="typescript"
			code={`// src/routes/api/users/+server.ts
import { json, error } from '@sveltejs/kit';
import type { RequestHandler } from './$types';

// POST /api/users
export const POST: RequestHandler = async ({ request }) => {
  // リクエストボディを取得
  const body = await request.json();

  // バリデーション
  if (!body.name || !body.email) {
    throw error(400, 'name と email は必須です');
  }

  // DBに保存（例）
  const newUser = await db.user.create({
    data: {
      name: body.name,
      email: body.email
    }
  });

  // 201 Created で返す
  return json(newUser, { status: 201 });
};`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div><span style="color:#ce9178;">POST</span> /api/users</div><div style="color:#6a9955;">// 新しいユーザーを作成</div></div>`}
		/>

		<CodePreview
			title="他のHTTPメソッド"
			description="PUT, PATCH, DELETE"
			language="typescript"
			code={`// src/routes/api/users/[id]/+server.ts
import { json, error } from '@sveltejs/kit';
import type { RequestHandler } from './$types';

// GET /api/users/:id
export const GET: RequestHandler = async ({ params }) => {
  const user = await db.user.findUnique({
    where: { id: Number(params.id) }
  });

  if (!user) {
    throw error(404, 'ユーザーが見つかりません');
  }

  return json(user);
};

// PUT /api/users/:id （全体更新）
export const PUT: RequestHandler = async ({ params, request }) => {
  const body = await request.json();
  const user = await db.user.update({
    where: { id: Number(params.id) },
    data: body
  });
  return json(user);
};

// PATCH /api/users/:id （部分更新）
export const PATCH: RequestHandler = async ({ params, request }) => {
  const body = await request.json();
  const user = await db.user.update({
    where: { id: Number(params.id) },
    data: body
  });
  return json(user);
};

// DELETE /api/users/:id
export const DELETE: RequestHandler = async ({ params }) => {
  await db.user.delete({
    where: { id: Number(params.id) }
  });
  return new Response(null, { status: 204 });
};`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div><span style="color:#4ec9b0;">GET</span> - 取得</div><div><span style="color:#4ec9b0;">PUT</span> - 全体更新</div><div><span style="color:#4ec9b0;">PATCH</span> - 部分更新</div><div><span style="color:#4ec9b0;">DELETE</span> - 削除</div></div>`}
		/>
	</section>

	<!-- リクエスト情報 -->
	<section class="mb-10">
		<h2 id="request" class="text-xl font-bold mb-4">リクエスト情報の取得</h2>

		<CodePreview
			title="様々なリクエスト情報"
			description="event オブジェクトから取得"
			language="typescript"
			code={`export const GET: RequestHandler = async (event) => {
  // URLパラメータ: /api/users/123 → params.id = "123"
  const { id } = event.params;

  // クエリパラメータ: /api/users?page=2&limit=10
  const page = event.url.searchParams.get('page') || '1';
  const limit = event.url.searchParams.get('limit') || '10';

  // リクエストヘッダー
  const authHeader = event.request.headers.get('Authorization');

  // Cookie
  const session = event.cookies.get('session');

  // ローカル（hooksで設定した値）
  const user = event.locals.user;

  return json({ page, limit });
};`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div><span style="color:#9cdcfe;">params</span> - URLパラメータ</div><div><span style="color:#9cdcfe;">url.searchParams</span> - クエリ</div><div><span style="color:#9cdcfe;">request.headers</span> - ヘッダー</div><div><span style="color:#9cdcfe;">cookies</span> - Cookie</div></div>`}
		/>

		<CodePreview
			title="FormDataの処理"
			description="ファイルアップロードなど"
			language="typescript"
			code={`// src/routes/api/upload/+server.ts
export const POST: RequestHandler = async ({ request }) => {
  const formData = await request.formData();

  // テキストフィールド
  const title = formData.get('title');

  // ファイル
  const file = formData.get('file') as File;

  if (file) {
    const buffer = await file.arrayBuffer();
    // ファイルを保存...
    console.log('ファイル名:', file.name);
    console.log('サイズ:', file.size);
    console.log('タイプ:', file.type);
  }

  return json({ success: true });
};`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div style="color:#6a9955;">// FormDataでファイルを受け取る</div><div style="color:#6a9955;">// request.formData() で取得</div></div>`}
		/>
	</section>

	<!-- レスポンス -->
	<section class="mb-10">
		<h2 id="response" class="text-xl font-bold mb-4">レスポンスの種類</h2>

		<CodePreview
			title="様々なレスポンス"
			description="JSON以外も返せる"
			language="typescript"
			code={`import { json, text, error, redirect } from '@sveltejs/kit';

// JSON レスポンス
export const GET: RequestHandler = async () => {
  return json({ message: 'Hello' });
};

// テキスト レスポンス
export const GET: RequestHandler = async () => {
  return text('Hello, World!');
};

// エラー レスポンス
export const GET: RequestHandler = async () => {
  throw error(404, 'Not Found');
};

// リダイレクト
export const GET: RequestHandler = async () => {
  throw redirect(302, '/login');
};

// カスタムレスポンス
export const GET: RequestHandler = async () => {
  return new Response('<h1>HTML</h1>', {
    status: 200,
    headers: {
      'Content-Type': 'text/html'
    }
  });
};`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div><span style="color:#dcdcaa;">json</span>() - JSON</div><div><span style="color:#dcdcaa;">text</span>() - テキスト</div><div><span style="color:#dcdcaa;">error</span>() - エラー</div><div><span style="color:#dcdcaa;">redirect</span>() - リダイレクト</div></div>`}
		/>
	</section>

	<!-- フロントエンドからの呼び出し -->
	<section class="mb-10">
		<h2 id="frontend" class="text-xl font-bold mb-4">フロントエンドからの呼び出し</h2>

		<CodePreview
			title="fetchでAPIを呼ぶ"
			description="Svelteコンポーネントから"
			language="svelte"
			code={`<script>
  let users = $state([]);
  let loading = $state(false);
  let error = $state('');

  async function loadUsers() {
    loading = true;
    error = '';

    try {
      const response = await fetch('/api/users');

      if (!response.ok) {
        throw new Error('データの取得に失敗しました');
      }

      users = await response.json();
    } catch (e) {
      error = e.message;
    } finally {
      loading = false;
    }
  }

  async function createUser() {
    const response = await fetch('/api/users', {
      method: 'POST',
      headers: {
        'Content-Type': 'application/json'
      },
      body: JSON.stringify({
        name: '新しいユーザー',
        email: 'new@example.com'
      })
    });

    if (response.ok) {
      await loadUsers();  // リストを更新
    }
  }

  // 初回読み込み
  $effect(() => {
    loadUsers();
  });
</script>

{#if loading}
  <p>読み込み中...</p>
{:else if error}
  <p class="error">{error}</p>
{:else}
  <ul>
    {#each users as user}
      <li>{user.name}</li>
    {/each}
  </ul>
{/if}

<button onclick={createUser}>ユーザー追加</button>`}
			previewHtml={`<div style="padding:12px;"><ul style="margin-bottom:12px;"><li>田中太郎</li><li>鈴木花子</li></ul><button style="padding:6px 12px;background:#ff3e00;color:white;border:none;border-radius:4px;">ユーザー追加</button></div>`}
		/>
	</section>

	<!-- 認証付きAPI -->
	<section class="mb-10">
		<h2 id="auth" class="text-xl font-bold mb-4">認証付きAPI</h2>

		<CodePreview
			title="認証チェック"
			description="localsを使った認証"
			language="typescript"
			code={`// src/routes/api/protected/+server.ts
import { json, error } from '@sveltejs/kit';
import type { RequestHandler } from './$types';

export const GET: RequestHandler = async ({ locals }) => {
  // hooksで設定したユーザー情報をチェック
  if (!locals.user) {
    throw error(401, '認証が必要です');
  }

  // 権限チェック
  if (locals.user.role !== 'admin') {
    throw error(403, '権限がありません');
  }

  // 保護されたデータを返す
  const secretData = await getSecretData();
  return json(secretData);
};

// src/hooks.server.ts
export const handle: Handle = async ({ event, resolve }) => {
  const session = event.cookies.get('session');
  if (session) {
    event.locals.user = await getUserFromSession(session);
  }
  return resolve(event);
};`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div style="color:#6a9955;">// hooks.server.ts でユーザーを設定</div><div style="color:#6a9955;">// API側で locals.user をチェック</div></div>`}
		/>
	</section>

	<!-- ベストプラクティス -->
	<section class="mb-10">
		<h2 id="tips" class="text-xl font-bold mb-4">ベストプラクティス</h2>

		<div class="grid grid-cols-1 md:grid-cols-2 gap-4">
			<div class="p-4 rounded-lg bg-green-50 dark:bg-green-900/20 border border-green-200 dark:border-green-800">
				<h3 class="font-semibold text-green-800 dark:text-green-200 mb-2">✅ やるべきこと</h3>
				<ul class="text-sm text-green-700 dark:text-green-300 list-disc list-inside space-y-1">
					<li>バリデーションを必ず行う</li>
					<li>適切なステータスコードを返す</li>
					<li>エラーメッセージを分かりやすく</li>
					<li>型定義をしっかり書く</li>
				</ul>
			</div>
			<div class="p-4 rounded-lg bg-red-50 dark:bg-red-900/20 border border-red-200 dark:border-red-800">
				<h3 class="font-semibold text-red-800 dark:text-red-200 mb-2">❌ 避けるべきこと</h3>
				<ul class="text-sm text-red-700 dark:text-red-300 list-disc list-inside space-y-1">
					<li>ユーザー入力を信用する</li>
					<li>機密情報をレスポンスに含める</li>
					<li>エラーの詳細を本番で露出</li>
					<li>認証なしで機密データにアクセス</li>
				</ul>
			</div>
		</div>
	</section>

	<!-- ナビゲーション -->
	<div class="flex justify-between pt-6 border-t border-gray-200 dark:border-gray-700">
		<a href="/sveltekit/layouts" class="inline-flex items-center gap-2 px-4 py-2 rounded-lg border border-gray-300 dark:border-gray-600 hover:bg-gray-100 dark:hover:bg-gray-800 transition-colors">
			<svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
				<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 19l-7-7 7-7" />
			</svg>
			前へ：レイアウト
		</a>
		<a href="/sveltekit/libraries" class="inline-flex items-center gap-2 px-4 py-2 rounded-lg bg-primary-600 text-white hover:bg-primary-700 transition-colors">
			次へ：ライブラリ
			<svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
				<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 5l7 7-7 7" />
			</svg>
		</a>
	</div>
</article>
