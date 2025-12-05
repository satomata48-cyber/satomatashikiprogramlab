<script>
	import CodePreview from '$lib/components/CodePreview.svelte';
</script>

<svelte:head>
	<title>D1 SQLの基本 | さとまたラボ</title>
</svelte:head>

<article>
	<h1 class="text-3xl font-bold mb-2">SQLの基本</h1>
	<p class="text-lg text-gray-600 dark:text-gray-400 mb-8">
		D1で使うSQLiteのSQL文を学ぶ
	</p>

	<!-- SQLとは -->
	<section class="mb-10">
		<h2 id="what-is-sql" class="text-xl font-bold mb-4">SQLとは</h2>

		<div class="p-6 rounded-xl bg-orange-50 dark:bg-orange-900/20 border border-orange-200 dark:border-orange-800 mb-6">
			<p class="text-orange-800 dark:text-orange-200 mb-4">
				<strong>Structured Query Language</strong>（構造化問い合わせ言語）
			</p>
			<p class="text-sm text-orange-700 dark:text-orange-300">
				データベースとやり取りするための言語。SELECT, INSERT, UPDATE, DELETE の4つを覚えればほぼOK！
			</p>
		</div>
	</section>

	<!-- CREATE TABLE -->
	<section class="mb-10">
		<h2 id="create" class="text-xl font-bold mb-4">テーブルを作る（CREATE TABLE）</h2>

		<CodePreview
			title="CREATE TABLE"
			description="テーブルを定義する"
			language="sql"
			code={`-- 基本的なテーブル作成
CREATE TABLE users (
  id INTEGER PRIMARY KEY AUTOINCREMENT,
  name TEXT NOT NULL,
  email TEXT UNIQUE,
  age INTEGER,
  created_at TEXT DEFAULT CURRENT_TIMESTAMP
);

-- IF NOT EXISTS で既に存在してもエラーにならない
CREATE TABLE IF NOT EXISTS users (
  id INTEGER PRIMARY KEY AUTOINCREMENT,
  name TEXT NOT NULL
);`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div style="color:#569cd6;">CREATE TABLE</div><div style="color:#6a9955;">// テーブルの設計図を作る</div></div>`}
		/>

		<div class="mt-4 p-4 rounded-lg bg-gray-100 dark:bg-gray-800">
			<p class="font-semibold text-gray-800 dark:text-gray-200 mb-2">主なデータ型</p>
			<div class="grid md:grid-cols-2 gap-2 text-sm">
				<div><code>INTEGER</code> - 整数</div>
				<div><code>REAL</code> - 小数</div>
				<div><code>TEXT</code> - 文字列</div>
				<div><code>BLOB</code> - バイナリデータ</div>
			</div>
			<p class="font-semibold text-gray-800 dark:text-gray-200 mb-2 mt-4">主な制約</p>
			<div class="grid md:grid-cols-2 gap-2 text-sm">
				<div><code>PRIMARY KEY</code> - 主キー（一意の識別子）</div>
				<div><code>NOT NULL</code> - NULLを許可しない</div>
				<div><code>UNIQUE</code> - 重複を許可しない</div>
				<div><code>DEFAULT</code> - デフォルト値</div>
			</div>
		</div>
	</section>

	<!-- SELECT -->
	<section class="mb-10">
		<h2 id="select" class="text-xl font-bold mb-4">データを取得する（SELECT）</h2>

		<CodePreview
			title="SELECT の基本"
			description="データを取得する"
			language="sql"
			code={`-- 全データを取得
SELECT * FROM users;

-- 特定のカラムだけ取得
SELECT name, email FROM users;

-- 条件を指定（WHERE）
SELECT * FROM users WHERE age >= 20;

-- 並び替え（ORDER BY）
SELECT * FROM users ORDER BY created_at DESC;

-- 件数制限（LIMIT）
SELECT * FROM users LIMIT 10;

-- ページネーション（LIMIT + OFFSET）
SELECT * FROM users LIMIT 10 OFFSET 20;  -- 21〜30件目`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div><span style="color:#569cd6;">SELECT</span> カラム <span style="color:#569cd6;">FROM</span> テーブル</div></div>`}
		/>

		<CodePreview
			title="WHERE の条件"
			description="様々な条件の書き方"
			language="sql"
			code={`-- 等しい
SELECT * FROM users WHERE name = '田中';

-- 等しくない
SELECT * FROM users WHERE status != 'deleted';

-- 比較
SELECT * FROM users WHERE age > 20;
SELECT * FROM users WHERE age >= 20;
SELECT * FROM users WHERE age < 30;
SELECT * FROM users WHERE age <= 30;

-- 範囲
SELECT * FROM users WHERE age BETWEEN 20 AND 30;

-- 含む
SELECT * FROM users WHERE status IN ('active', 'pending');

-- あいまい検索（LIKE）
SELECT * FROM users WHERE name LIKE '田%';    -- 田で始まる
SELECT * FROM users WHERE name LIKE '%郎';    -- 郎で終わる
SELECT * FROM users WHERE name LIKE '%中%';   -- 中を含む

-- NULL判定
SELECT * FROM users WHERE deleted_at IS NULL;
SELECT * FROM users WHERE deleted_at IS NOT NULL;

-- 複数条件（AND / OR）
SELECT * FROM users WHERE age >= 20 AND status = 'active';
SELECT * FROM users WHERE age < 20 OR age > 60;`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div style="color:#6a9955;">// 条件を組み合わせて絞り込む</div></div>`}
		/>
	</section>

	<!-- INSERT -->
	<section class="mb-10">
		<h2 id="insert" class="text-xl font-bold mb-4">データを追加する（INSERT）</h2>

		<CodePreview
			title="INSERT"
			description="新しいデータを追加"
			language="sql"
			code={`-- 1件追加
INSERT INTO users (name, email, age) VALUES ('田中太郎', 'tanaka@example.com', 25);

-- 複数件追加
INSERT INTO users (name, email, age) VALUES
  ('鈴木花子', 'suzuki@example.com', 30),
  ('佐藤次郎', 'sato@example.com', 28);

-- 存在しなければ追加（SQLite固有）
INSERT OR IGNORE INTO users (id, name) VALUES (1, '田中太郎');

-- 存在すれば更新、なければ追加（UPSERT）
INSERT INTO users (id, name, email)
VALUES (1, '田中太郎', 'tanaka@example.com')
ON CONFLICT(id) DO UPDATE SET
  name = excluded.name,
  email = excluded.email;`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div><span style="color:#569cd6;">INSERT INTO</span> テーブル (カラム) <span style="color:#569cd6;">VALUES</span> (値)</div></div>`}
		/>
	</section>

	<!-- UPDATE -->
	<section class="mb-10">
		<h2 id="update" class="text-xl font-bold mb-4">データを更新する（UPDATE）</h2>

		<CodePreview
			title="UPDATE"
			description="既存のデータを変更"
			language="sql"
			code={`-- 特定のレコードを更新
UPDATE users SET name = '山田太郎' WHERE id = 1;

-- 複数カラムを更新
UPDATE users
SET
  name = '山田太郎',
  email = 'yamada@example.com',
  updated_at = CURRENT_TIMESTAMP
WHERE id = 1;

-- 条件に合う全レコードを更新
UPDATE users SET status = 'inactive' WHERE last_login < '2024-01-01';`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div><span style="color:#569cd6;">UPDATE</span> テーブル <span style="color:#569cd6;">SET</span> カラム = 値 <span style="color:#569cd6;">WHERE</span> 条件</div><div style="color:#f14c4c;">⚠️ WHEREを忘れると全件更新！</div></div>`}
		/>

		<div class="mt-4 p-4 rounded-lg bg-red-50 dark:bg-red-900/20 border border-red-200 dark:border-red-800">
			<p class="font-semibold text-red-800 dark:text-red-200">WHERE を忘れないで！</p>
			<p class="text-sm text-red-700 dark:text-red-300 mt-1">
				<code>WHERE</code> を書き忘れると、テーブルの全レコードが更新されてしまいます。
			</p>
		</div>
	</section>

	<!-- DELETE -->
	<section class="mb-10">
		<h2 id="delete" class="text-xl font-bold mb-4">データを削除する（DELETE）</h2>

		<CodePreview
			title="DELETE"
			description="データを削除"
			language="sql"
			code={`-- 特定のレコードを削除
DELETE FROM users WHERE id = 1;

-- 条件に合う全レコードを削除
DELETE FROM users WHERE status = 'deleted';

-- 全件削除（注意！）
DELETE FROM users;`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div><span style="color:#569cd6;">DELETE FROM</span> テーブル <span style="color:#569cd6;">WHERE</span> 条件</div><div style="color:#f14c4c;">⚠️ WHEREを忘れると全件削除！</div></div>`}
		/>
	</section>

	<!-- 集計関数 -->
	<section class="mb-10">
		<h2 id="aggregate" class="text-xl font-bold mb-4">集計関数</h2>

		<CodePreview
			title="集計関数"
			description="データを集計する"
			language="sql"
			code={`-- 件数を数える
SELECT COUNT(*) FROM users;

-- 条件付きで数える
SELECT COUNT(*) FROM users WHERE status = 'active';

-- 合計
SELECT SUM(age) FROM users;

-- 平均
SELECT AVG(age) FROM users;

-- 最大・最小
SELECT MAX(age), MIN(age) FROM users;

-- グループ化
SELECT status, COUNT(*) as count
FROM users
GROUP BY status;

-- 結果:
-- | status   | count |
-- | active   | 100   |
-- | inactive | 50    |
-- | deleted  | 10    |`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div><span style="color:#dcdcaa;">COUNT()</span> <span style="color:#dcdcaa;">SUM()</span> <span style="color:#dcdcaa;">AVG()</span></div></div>`}
		/>
	</section>

	<!-- テーブル結合 -->
	<section class="mb-10">
		<h2 id="join" class="text-xl font-bold mb-4">テーブル結合（JOIN）</h2>

		<CodePreview
			title="JOIN"
			description="複数のテーブルを結合"
			language="sql"
			code={`-- postsテーブルとusersテーブルを結合
-- posts.user_id = users.id で紐づけ

SELECT
  posts.id,
  posts.title,
  users.name as author_name
FROM posts
INNER JOIN users ON posts.user_id = users.id;

-- LEFT JOIN（該当がなくてもpostsは全部取得）
SELECT
  posts.id,
  posts.title,
  users.name as author_name
FROM posts
LEFT JOIN users ON posts.user_id = users.id;`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div><span style="color:#569cd6;">JOIN</span> で複数テーブルを結合</div></div>`}
		/>
	</section>

	<!-- ナビゲーション -->
	<div class="flex justify-between pt-6 border-t border-gray-200 dark:border-gray-700">
		<a href="/cloudflare/d1-setup" class="inline-flex items-center gap-2 px-4 py-2 rounded-lg border border-gray-300 dark:border-gray-600 hover:bg-gray-100 dark:hover:bg-gray-800 transition-colors">
			<svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
				<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 19l-7-7 7-7" />
			</svg>
			前へ：D1 セットアップ
		</a>
		<a href="/cloudflare/d1-sveltekit" class="inline-flex items-center gap-2 px-4 py-2 rounded-lg bg-primary-600 text-white hover:bg-primary-700 transition-colors">
			次へ：D1 SvelteKit連携
			<svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
				<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 5l7 7-7 7" />
			</svg>
		</a>
	</div>
</article>
