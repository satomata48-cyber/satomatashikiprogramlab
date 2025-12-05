<script>
	import CodePreview from '$lib/components/CodePreview.svelte';
</script>

<svelte:head>
	<title>D1 SvelteKitと連携 | さとまたラボ</title>
</svelte:head>

<article>
	<h1 class="text-3xl font-bold mb-2">SvelteKitと連携</h1>
	<p class="text-lg text-gray-600 dark:text-gray-400 mb-8">
		SvelteKitからD1データベースを操作する
	</p>

	<!-- 基本的なアクセス方法 -->
	<section class="mb-10">
		<h2 id="access" class="text-xl font-bold mb-4">D1へのアクセス方法</h2>

		<div class="p-6 rounded-xl bg-orange-50 dark:bg-orange-900/20 border border-orange-200 dark:border-orange-800 mb-6">
			<p class="text-orange-800 dark:text-orange-200 mb-2">
				<strong>platform.env.DB でアクセス</strong>
			</p>
			<p class="text-sm text-orange-700 dark:text-orange-300">
				SvelteKitのサーバーサイドコード（+server.ts, +page.server.ts）からアクセスできます。
				クライアントサイドからは直接アクセスできません。
			</p>
		</div>

		<CodePreview
			title="基本的なアクセス"
			description="platform.env.DB を使う"
			language="typescript"
			code={`// +page.server.ts または +server.ts から
export const load = async ({ platform }) => {
  // D1データベースにアクセス
  const db = platform?.env?.DB;

  if (!db) {
    // ローカル開発時（npm run dev）はundefined
    console.warn('D1 is not available');
    return { todos: [] };
  }

  // SQLを実行
  const { results } = await db
    .prepare('SELECT * FROM todos ORDER BY created_at DESC')
    .all();

  return { todos: results };
};`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div>platform?.env?.<span style="color:#4ec9b0;">DB</span></div><div style="color:#6a9955;">// wrangler.toml の binding と同じ</div></div>`}
		/>
	</section>

	<!-- CRUD操作 -->
	<section class="mb-10">
		<h2 id="crud" class="text-xl font-bold mb-4">CRUD操作の実装</h2>

		<CodePreview
			title="データを取得（SELECT）"
			description="+page.server.ts での load 関数"
			language="typescript"
			code={`// src/routes/todos/+page.server.ts
import type { PageServerLoad } from './$types';

export const load: PageServerLoad = async ({ platform }) => {
  const db = platform?.env?.DB;
  if (!db) return { todos: [] };

  // 全件取得
  const { results } = await db
    .prepare('SELECT * FROM todos ORDER BY created_at DESC')
    .all();

  return { todos: results };
};

// 1件取得の場合
export const load: PageServerLoad = async ({ platform, params }) => {
  const db = platform?.env?.DB;
  if (!db) return { todo: null };

  const result = await db
    .prepare('SELECT * FROM todos WHERE id = ?')
    .bind(params.id)
    .first();  // .first() で1件だけ取得

  return { todo: result };
};`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div><span style="color:#dcdcaa;">.all()</span> → 全件取得</div><div><span style="color:#dcdcaa;">.first()</span> → 1件取得</div></div>`}
		/>

		<CodePreview
			title="データを追加（INSERT）"
			description="Form Actionで実装"
			language="typescript"
			code={`// src/routes/todos/+page.server.ts
import type { Actions } from './$types';
import { fail } from '@sveltejs/kit';

export const actions: Actions = {
  create: async ({ request, platform }) => {
    const db = platform?.env?.DB;
    if (!db) return fail(500, { message: 'Database not available' });

    const formData = await request.formData();
    const title = formData.get('title') as string;

    if (!title || title.trim() === '') {
      return fail(400, { message: 'タイトルは必須です' });
    }

    await db
      .prepare('INSERT INTO todos (title) VALUES (?)')
      .bind(title.trim())
      .run();

    return { success: true };
  }
};`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div><span style="color:#dcdcaa;">.bind()</span> でパラメータを安全に渡す</div><div style="color:#6a9955;">// SQLインジェクション対策</div></div>`}
		/>

		<CodePreview
			title="データを更新・削除"
			description="UPDATE / DELETE の実装"
			language="typescript"
			code={`export const actions: Actions = {
  // 完了状態を切り替え
  toggle: async ({ request, platform }) => {
    const db = platform?.env?.DB;
    if (!db) return fail(500);

    const formData = await request.formData();
    const id = formData.get('id');
    const completed = formData.get('completed') === 'true' ? 0 : 1;

    await db
      .prepare('UPDATE todos SET completed = ? WHERE id = ?')
      .bind(completed, id)
      .run();

    return { success: true };
  },

  // 削除
  delete: async ({ request, platform }) => {
    const db = platform?.env?.DB;
    if (!db) return fail(500);

    const formData = await request.formData();
    const id = formData.get('id');

    await db
      .prepare('DELETE FROM todos WHERE id = ?')
      .bind(id)
      .run();

    return { success: true };
  }
};`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div><span style="color:#dcdcaa;">.run()</span> → INSERT/UPDATE/DELETE用</div></div>`}
		/>
	</section>

	<!-- フロントエンド -->
	<section class="mb-10">
		<h2 id="frontend" class="text-xl font-bold mb-4">フロントエンドの実装</h2>

		<CodePreview
			title="Todoリストの表示とフォーム"
			description="+page.svelte"
			language="svelte"
			code={`<script lang="ts">
  import { enhance } from '$app/forms';

  let { data } = $props();
</script>

<!-- 追加フォーム -->
<form method="POST" action="?/create" use:enhance>
  <input
    type="text"
    name="title"
    placeholder="新しいタスク"
    class="border rounded px-3 py-2"
  />
  <button type="submit" class="bg-blue-500 text-white px-4 py-2 rounded">
    追加
  </button>
</form>

<!-- Todoリスト -->
<ul class="space-y-2 mt-4">
  {#each data.todos as todo}
    <li class="flex items-center gap-2 p-2 border rounded">
      <!-- 完了切り替え -->
      <form method="POST" action="?/toggle" use:enhance>
        <input type="hidden" name="id" value={todo.id} />
        <input type="hidden" name="completed" value={todo.completed} />
        <button type="submit" class="text-xl">
          {todo.completed ? '✅' : '⬜'}
        </button>
      </form>

      <span class:line-through={todo.completed}>
        {todo.title}
      </span>

      <!-- 削除 -->
      <form method="POST" action="?/delete" use:enhance class="ml-auto">
        <input type="hidden" name="id" value={todo.id} />
        <button type="submit" class="text-red-500">削除</button>
      </form>
    </li>
  {/each}
</ul>`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div style="color:#6a9955;">// use:enhance で非同期送信</div></div>`}
		/>
	</section>

	<!-- APIエンドポイント -->
	<section class="mb-10">
		<h2 id="api" class="text-xl font-bold mb-4">APIエンドポイントとして実装</h2>

		<CodePreview
			title="REST API風のエンドポイント"
			description="src/routes/api/todos/+server.ts"
			language="typescript"
			code={`// src/routes/api/todos/+server.ts
import type { RequestHandler } from './$types';
import { json } from '@sveltejs/kit';

// GET /api/todos
export const GET: RequestHandler = async ({ platform }) => {
  const db = platform?.env?.DB;
  if (!db) return json({ error: 'DB not available' }, { status: 500 });

  const { results } = await db
    .prepare('SELECT * FROM todos ORDER BY created_at DESC')
    .all();

  return json(results);
};

// POST /api/todos
export const POST: RequestHandler = async ({ request, platform }) => {
  const db = platform?.env?.DB;
  if (!db) return json({ error: 'DB not available' }, { status: 500 });

  const { title } = await request.json();

  const result = await db
    .prepare('INSERT INTO todos (title) VALUES (?) RETURNING *')
    .bind(title)
    .first();

  return json(result, { status: 201 });
};

// DELETE /api/todos/[id]
// src/routes/api/todos/[id]/+server.ts
export const DELETE: RequestHandler = async ({ params, platform }) => {
  const db = platform?.env?.DB;
  if (!db) return json({ error: 'DB not available' }, { status: 500 });

  await db
    .prepare('DELETE FROM todos WHERE id = ?')
    .bind(params.id)
    .run();

  return new Response(null, { status: 204 });
};`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div style="color:#6a9955;">// REST API として公開</div></div>`}
		/>
	</section>

	<!-- バッチ処理 -->
	<section class="mb-10">
		<h2 id="batch" class="text-xl font-bold mb-4">バッチ処理</h2>

		<CodePreview
			title="複数のSQLをまとめて実行"
			description="db.batch() を使う"
			language="typescript"
			code={`// 複数の操作をまとめて実行（トランザクション的）
const results = await db.batch([
  db.prepare('INSERT INTO todos (title) VALUES (?)').bind('タスク1'),
  db.prepare('INSERT INTO todos (title) VALUES (?)').bind('タスク2'),
  db.prepare('INSERT INTO todos (title) VALUES (?)').bind('タスク3'),
]);

// 全ての操作が成功するか、全て失敗するか
// → データの整合性を保てる`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div><span style="color:#dcdcaa;">db.batch([])</span></div><div style="color:#6a9955;">// 複数操作をアトミックに実行</div></div>`}
		/>
	</section>

	<!-- デプロイ -->
	<section class="mb-10">
		<h2 id="deploy" class="text-xl font-bold mb-4">デプロイ</h2>

		<CodePreview
			title="Cloudflare Pagesにデプロイ"
			description="wrangler でデプロイ"
			language="bash"
			code={`# ビルド
npm run build

# デプロイ
wrangler pages deploy .svelte-kit/cloudflare

# 本番のD1にスキーマを適用（初回のみ）
wrangler d1 execute my-database --remote --file=./schema.sql`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div style="color:#6a9955;"># Cloudflare Pagesにデプロイ</div></div>`}
		/>

		<div class="mt-4 p-4 rounded-lg bg-emerald-50 dark:bg-emerald-900/20 border border-emerald-200 dark:border-emerald-800">
			<p class="font-semibold text-emerald-800 dark:text-emerald-200">GitHubと連携も可能</p>
			<p class="text-sm text-emerald-700 dark:text-emerald-300 mt-1">
				Cloudflare Pagesダッシュボードでリポジトリを連携すれば、pushするだけで自動デプロイされます。
			</p>
		</div>
	</section>

	<!-- ナビゲーション -->
	<div class="flex justify-between pt-6 border-t border-gray-200 dark:border-gray-700">
		<a href="/cloudflare/d1-sql" class="inline-flex items-center gap-2 px-4 py-2 rounded-lg border border-gray-300 dark:border-gray-600 hover:bg-gray-100 dark:hover:bg-gray-800 transition-colors">
			<svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
				<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 19l-7-7 7-7" />
			</svg>
			前へ：D1 SQLの基本
		</a>
		<a href="/cloudflare/r2" class="inline-flex items-center gap-2 px-4 py-2 rounded-lg bg-primary-600 text-white hover:bg-primary-700 transition-colors">
			次へ：R2 ストレージ
			<svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
				<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 5l7 7-7 7" />
			</svg>
		</a>
	</div>
</article>
