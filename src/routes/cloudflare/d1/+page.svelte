<script>
	import CodePreview from '$lib/components/CodePreview.svelte';
	import FeatureCard from '$lib/components/FeatureCard.svelte';

	const features = [
		{ icon: '🗄️', title: 'SQLite', description: '軽量で高速なデータベース', tag: 'データベース' },
		{ icon: '🌍', title: 'エッジ実行', description: 'ユーザーに近い場所で動作', tag: 'パフォーマンス' },
		{ icon: '💰', title: '低コスト', description: '従量課金で無駄がない', tag: '料金' },
		{ icon: '🔧', title: 'Wrangler', description: 'CLIで簡単管理', tag: 'ツール' },
		{ icon: '⚡', title: 'サーバーレス', description: 'インフラ管理不要', tag: '特徴' },
		{ icon: '🔗', title: 'Workers連携', description: 'Cloudflare Workersと統合', tag: '連携' }
	];
</script>

<svelte:head>
	<title>Cloudflare D1 はじめに | さとまたラボ</title>
</svelte:head>

<article>
	<h1 class="text-3xl font-bold mb-2">Cloudflare D1</h1>
	<p class="text-lg text-gray-600 dark:text-gray-400 mb-8">
		エッジで動くサーバーレスSQLiteデータベース
	</p>

	<!-- D1とは -->
	<section class="mb-10">
		<h2 id="what-is" class="text-xl font-bold mb-4">Cloudflare D1とは？</h2>

		<div class="p-6 rounded-xl bg-orange-50 dark:bg-orange-900/20 border border-orange-200 dark:border-orange-800 mb-6">
			<p class="text-orange-800 dark:text-orange-200 mb-4">
				<strong>一言で言うと：</strong>「世界中のエッジで動くSQLiteデータベース」
			</p>
			<div class="grid grid-cols-1 md:grid-cols-2 gap-4 text-sm">
				<div class="p-3 bg-white dark:bg-gray-800 rounded-lg">
					<div class="font-semibold text-orange-700 dark:text-orange-300 mb-2">従来のデータベース</div>
					<ul class="text-gray-600 dark:text-gray-400 space-y-1">
						<li>・1つの場所（リージョン）にある</li>
						<li>・遠いユーザーは遅延が発生</li>
						<li>・サーバー管理が必要</li>
						<li>・常時稼働でコストがかかる</li>
					</ul>
				</div>
				<div class="p-3 bg-white dark:bg-gray-800 rounded-lg">
					<div class="font-semibold text-orange-700 dark:text-orange-300 mb-2">D1なら...</div>
					<ul class="text-gray-600 dark:text-gray-400 space-y-1">
						<li>・世界中のエッジに配置</li>
						<li>・ユーザーに近い場所で実行</li>
						<li>・サーバーレスで管理不要</li>
						<li>・使った分だけの課金</li>
					</ul>
				</div>
			</div>
		</div>

		<div class="p-4 rounded-lg bg-blue-50 dark:bg-blue-900/20 border border-blue-200 dark:border-blue-800 mb-6">
			<p class="font-semibold text-blue-800 dark:text-blue-200">SQLiteとは？</p>
			<div class="text-sm text-blue-700 dark:text-blue-300 mt-2">
				<p class="mb-2">
					世界で最も使われているデータベースエンジン。スマホアプリ、ブラウザ、OSなど至る所で使用されています。
				</p>
				<ul class="space-y-1">
					<li>・<strong>軽量</strong>：ファイル1つで完結</li>
					<li>・<strong>高速</strong>：シンプルな構造で高パフォーマンス</li>
					<li>・<strong>SQL対応</strong>：標準的なSQLが使える</li>
					<li>・<strong>サーバー不要</strong>：組み込み型なのでプロセスが不要</li>
				</ul>
			</div>
		</div>
	</section>

	<!-- できること一覧 -->
	<section class="mb-10">
		<h2 id="features" class="text-xl font-bold mb-4">D1の特徴</h2>
		<div class="grid grid-cols-1 md:grid-cols-2 gap-3">
			{#each features as feature}
				<FeatureCard {...feature} />
			{/each}
		</div>
	</section>

	<!-- Supabaseとの比較 -->
	<section class="mb-10">
		<h2 id="comparison" class="text-xl font-bold mb-4">Supabase vs D1</h2>

		<div class="overflow-x-auto">
			<table class="w-full text-sm border-collapse">
				<thead>
					<tr class="bg-gray-100 dark:bg-gray-800">
						<th class="border border-gray-300 dark:border-gray-600 px-4 py-2 text-left">項目</th>
						<th class="border border-gray-300 dark:border-gray-600 px-4 py-2 text-left">Supabase</th>
						<th class="border border-gray-300 dark:border-gray-600 px-4 py-2 text-left">Cloudflare D1</th>
					</tr>
				</thead>
				<tbody>
					<tr>
						<td class="border border-gray-300 dark:border-gray-600 px-4 py-2 font-medium">データベース</td>
						<td class="border border-gray-300 dark:border-gray-600 px-4 py-2">PostgreSQL</td>
						<td class="border border-gray-300 dark:border-gray-600 px-4 py-2">SQLite</td>
					</tr>
					<tr class="bg-gray-50 dark:bg-gray-800/50">
						<td class="border border-gray-300 dark:border-gray-600 px-4 py-2 font-medium">認証機能</td>
						<td class="border border-gray-300 dark:border-gray-600 px-4 py-2">組み込み</td>
						<td class="border border-gray-300 dark:border-gray-600 px-4 py-2">なし（自前実装）</td>
					</tr>
					<tr>
						<td class="border border-gray-300 dark:border-gray-600 px-4 py-2 font-medium">ストレージ</td>
						<td class="border border-gray-300 dark:border-gray-600 px-4 py-2">組み込み</td>
						<td class="border border-gray-300 dark:border-gray-600 px-4 py-2">R2で別途利用</td>
					</tr>
					<tr class="bg-gray-50 dark:bg-gray-800/50">
						<td class="border border-gray-300 dark:border-gray-600 px-4 py-2 font-medium">管理画面</td>
						<td class="border border-gray-300 dark:border-gray-600 px-4 py-2">リッチなUI</td>
						<td class="border border-gray-300 dark:border-gray-600 px-4 py-2">シンプル</td>
					</tr>
					<tr>
						<td class="border border-gray-300 dark:border-gray-600 px-4 py-2 font-medium">向いている用途</td>
						<td class="border border-gray-300 dark:border-gray-600 px-4 py-2">フルスタックアプリ</td>
						<td class="border border-gray-300 dark:border-gray-600 px-4 py-2">軽量・高速なアプリ</td>
					</tr>
					<tr class="bg-gray-50 dark:bg-gray-800/50">
						<td class="border border-gray-300 dark:border-gray-600 px-4 py-2 font-medium">学習コスト</td>
						<td class="border border-gray-300 dark:border-gray-600 px-4 py-2">低（SDK充実）</td>
						<td class="border border-gray-300 dark:border-gray-600 px-4 py-2">中（SQL知識必要）</td>
					</tr>
				</tbody>
			</table>
		</div>

		<div class="mt-4 p-4 rounded-lg bg-amber-50 dark:bg-amber-900/20 border border-amber-200 dark:border-amber-800">
			<p class="font-semibold text-amber-800 dark:text-amber-200 mb-2">どちらを選ぶ？</p>
			<div class="text-sm text-amber-700 dark:text-amber-300 space-y-2">
				<p><strong>Supabase向き：</strong>認証・ストレージも必要、管理画面でデータ操作したい、PostgreSQLの機能を使いたい</p>
				<p><strong>D1向き：</strong>シンプルなデータ保存だけ、とにかく高速にしたい、Cloudflare Workersを使っている</p>
			</div>
		</div>
	</section>

	<!-- コード例 -->
	<section class="mb-10">
		<h2 id="examples" class="text-xl font-bold mb-4">コード例</h2>

		<CodePreview
			title="テーブル作成"
			description="SQLでテーブルを定義"
			language="sql"
			code={`-- todosテーブルを作成
CREATE TABLE todos (
  id INTEGER PRIMARY KEY AUTOINCREMENT,
  title TEXT NOT NULL,
  completed INTEGER DEFAULT 0,
  created_at TEXT DEFAULT CURRENT_TIMESTAMP
);

-- インデックスを追加（検索を高速化）
CREATE INDEX idx_todos_completed ON todos(completed);`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div style="color:#569cd6;">CREATE TABLE</div><div style="color:#6a9955;">// 標準的なSQLでテーブル定義</div></div>`}
		/>

		<CodePreview
			title="データの取得（SvelteKit）"
			description="server.tsからD1にアクセス"
			language="typescript"
			code={`// src/routes/api/todos/+server.ts
import type { RequestHandler } from './$types';

export const GET: RequestHandler = async ({ platform }) => {
  // D1データベースにアクセス
  const db = platform?.env?.DB;

  // SQLを実行
  const { results } = await db
    .prepare('SELECT * FROM todos ORDER BY created_at DESC')
    .all();

  return Response.json(results);
};`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div>platform.env.<span style="color:#4ec9b0;">DB</span></div><div style="color:#6a9955;">// Cloudflare経由でD1にアクセス</div></div>`}
		/>

		<CodePreview
			title="データの追加・更新・削除"
			description="CRUD操作"
			language="typescript"
			code={`// データを追加（INSERT）
await db
  .prepare('INSERT INTO todos (title) VALUES (?)')
  .bind('買い物に行く')
  .run();

// データを更新（UPDATE）
await db
  .prepare('UPDATE todos SET completed = 1 WHERE id = ?')
  .bind(1)
  .run();

// データを削除（DELETE）
await db
  .prepare('DELETE FROM todos WHERE id = ?')
  .bind(1)
  .run();

// 複数の操作をまとめて実行
await db.batch([
  db.prepare('INSERT INTO todos (title) VALUES (?)').bind('タスク1'),
  db.prepare('INSERT INTO todos (title) VALUES (?)').bind('タスク2'),
]);`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div><span style="color:#dcdcaa;">.prepare()</span> → SQLを準備</div><div><span style="color:#dcdcaa;">.bind()</span> → パラメータを設定</div><div><span style="color:#dcdcaa;">.run()</span> → 実行</div></div>`}
		/>
	</section>

	<!-- 料金 -->
	<section class="mb-10">
		<h2 id="pricing" class="text-xl font-bold mb-4">料金</h2>

		<div class="grid md:grid-cols-2 gap-4">
			<div class="p-4 rounded-lg bg-gray-50 dark:bg-gray-800 border border-gray-200 dark:border-gray-700">
				<h3 class="font-bold text-lg mb-2">Free（無料）</h3>
				<ul class="text-sm text-gray-600 dark:text-gray-400 space-y-1">
					<li>・読み取り: 500万行/日</li>
					<li>・書き込み: 10万行/日</li>
					<li>・ストレージ: 5GB</li>
				</ul>
				<p class="mt-2 text-xs text-gray-500">小〜中規模アプリには十分！</p>
			</div>
			<div class="p-4 rounded-lg bg-orange-50 dark:bg-orange-900/20 border border-orange-200 dark:border-orange-800">
				<h3 class="font-bold text-lg mb-2">Workers Paid（$5/月〜）</h3>
				<ul class="text-sm text-gray-600 dark:text-gray-400 space-y-1">
					<li>・読み取り: 500億行/月</li>
					<li>・書き込み: 5000万行/月</li>
					<li>・ストレージ: 10GB（追加可）</li>
				</ul>
				<p class="mt-2 text-xs text-orange-600 dark:text-orange-400">大規模アプリ向け</p>
			</div>
		</div>
	</section>

	<!-- 始め方 -->
	<section class="mb-10">
		<h2 id="getting-started" class="text-xl font-bold mb-4">始め方</h2>

		<CodePreview
			title="Wrangler CLIでD1を作成"
			description="コマンドラインでデータベースを作成"
			language="bash"
			code={`# Wrangler CLIをインストール
npm install -g wrangler

# Cloudflareにログイン
wrangler login

# D1データベースを作成
wrangler d1 create my-database

# SQLを実行（ローカル）
wrangler d1 execute my-database --local --command="CREATE TABLE users (id INTEGER PRIMARY KEY, name TEXT)"

# SQLを実行（本番）
wrangler d1 execute my-database --remote --command="SELECT * FROM users"`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div style="color:#6a9955;"># CLIで簡単にDB操作</div><div>wrangler d1 create</div><div>wrangler d1 execute</div></div>`}
		/>
	</section>

	<!-- ナビゲーション -->
	<div class="flex justify-between pt-6 border-t border-gray-200 dark:border-gray-700">
		<a href="/cloudflare/intro" class="inline-flex items-center gap-2 px-4 py-2 rounded-lg border border-gray-300 dark:border-gray-600 hover:bg-gray-100 dark:hover:bg-gray-800 transition-colors">
			<svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
				<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 19l-7-7 7-7" />
			</svg>
			前へ：Cloudflare
		</a>
		<a href="/cloudflare/d1-setup" class="inline-flex items-center gap-2 px-4 py-2 rounded-lg bg-primary-600 text-white hover:bg-primary-700 transition-colors">
			次へ：D1 セットアップ
			<svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
				<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 5l7 7-7 7" />
			</svg>
		</a>
	</div>
</article>
