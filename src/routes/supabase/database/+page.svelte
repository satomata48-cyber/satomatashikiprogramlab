<script>
	import CodePreview from '$lib/components/CodePreview.svelte';
</script>

<svelte:head>
	<title>Supabase データベース操作 | さとまたラボ</title>
</svelte:head>

<article>
	<h1 class="text-3xl font-bold mb-2">データベース操作</h1>
	<p class="text-lg text-gray-600 dark:text-gray-400 mb-8">
		SupabaseでのCRUD操作を学ぶ
	</p>

	<!-- テーブル作成 -->
	<section class="mb-10">
		<h2 id="create-table" class="text-xl font-bold mb-4">テーブルを作成</h2>

		<div class="p-4 rounded-lg bg-emerald-50 dark:bg-emerald-900/20 border border-emerald-200 dark:border-emerald-800 mb-4">
			<p class="font-semibold text-emerald-800 dark:text-emerald-200">Supabaseダッシュボードで作成</p>
			<p class="text-sm text-emerald-700 dark:text-emerald-300 mt-1">
				Table Editor → New Table でGUIから簡単に作成できます。または SQL Editor でSQLを実行することも可能です。
			</p>
		</div>

		<CodePreview
			title="SQLでテーブル作成"
			description="SQL Editorで実行"
			language="sql"
			code={`-- todosテーブルを作成
CREATE TABLE todos (
  id BIGSERIAL PRIMARY KEY,
  title TEXT NOT NULL,
  completed BOOLEAN DEFAULT false,
  user_id UUID REFERENCES auth.users(id),
  created_at TIMESTAMPTZ DEFAULT NOW()
);

-- RLS（Row Level Security）を有効化
ALTER TABLE todos ENABLE ROW LEVEL SECURITY;

-- 自分のデータのみ見れるポリシーを作成
CREATE POLICY "Users can view own todos"
  ON todos FOR SELECT
  USING (auth.uid() = user_id);

CREATE POLICY "Users can insert own todos"
  ON todos FOR INSERT
  WITH CHECK (auth.uid() = user_id);`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div style="color:#6a9955;">-- PostgreSQLの標準的なSQL</div></div>`}
		/>
	</section>

	<!-- SELECT -->
	<section class="mb-10">
		<h2 id="select" class="text-xl font-bold mb-4">データを取得（SELECT）</h2>

		<CodePreview
			title="基本的な取得"
			description="select() でデータを取得"
			language="typescript"
			code={`// 全件取得
const { data, error } = await supabase
  .from('todos')
  .select('*')

// 特定のカラムだけ取得
const { data } = await supabase
  .from('todos')
  .select('id, title, completed')

// 1件だけ取得
const { data } = await supabase
  .from('todos')
  .select('*')
  .single()  // 1件だけ返す（なければエラー）

// 件数を取得
const { count } = await supabase
  .from('todos')
  .select('*', { count: 'exact', head: true })`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div><span style="color:#dcdcaa;">.select('*')</span> → 全カラム</div><div><span style="color:#dcdcaa;">.select('id, title')</span> → 指定カラム</div></div>`}
		/>

		<CodePreview
			title="フィルタリング"
			description="条件を指定して取得"
			language="typescript"
			code={`// 等しい（=）
const { data } = await supabase
  .from('todos')
  .select('*')
  .eq('completed', false)  // completed = false

// 等しくない（!=）
.neq('status', 'deleted')

// より大きい（>）/ 以上（>=）
.gt('price', 1000)   // price > 1000
.gte('price', 1000)  // price >= 1000

// より小さい（<）/ 以下（<=）
.lt('price', 5000)   // price < 5000
.lte('price', 5000)  // price <= 5000

// LIKE検索
.like('title', '%買い物%')      // タイトルに「買い物」を含む
.ilike('title', '%shopping%')   // 大文字小文字を区別しない

// IN句
.in('status', ['active', 'pending'])

// NULL判定
.is('deleted_at', null)     // deleted_at IS NULL
.not('deleted_at', 'is', null)  // deleted_at IS NOT NULL`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div style="color:#6a9955;">// SQLの WHERE 句に相当</div></div>`}
		/>

		<CodePreview
			title="ソートとページネーション"
			description="並び替えと件数制限"
			language="typescript"
			code={`// 並び替え
const { data } = await supabase
  .from('todos')
  .select('*')
  .order('created_at', { ascending: false })  // 新しい順

// 複数カラムでソート
.order('priority', { ascending: false })
.order('created_at', { ascending: true })

// 件数制限
.limit(10)  // 10件まで

// ページネーション
.range(0, 9)    // 1〜10件目（0始まり）
.range(10, 19)  // 11〜20件目`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div><span style="color:#dcdcaa;">.order()</span> → ORDER BY</div><div><span style="color:#dcdcaa;">.limit()</span> → LIMIT</div><div><span style="color:#dcdcaa;">.range()</span> → OFFSET + LIMIT</div></div>`}
		/>
	</section>

	<!-- INSERT -->
	<section class="mb-10">
		<h2 id="insert" class="text-xl font-bold mb-4">データを追加（INSERT）</h2>

		<CodePreview
			title="データを追加"
			description="insert() でデータを追加"
			language="typescript"
			code={`// 1件追加
const { data, error } = await supabase
  .from('todos')
  .insert({ title: '買い物に行く', completed: false })
  .select()  // 追加したデータを返す

// 複数件追加
const { data, error } = await supabase
  .from('todos')
  .insert([
    { title: 'タスク1' },
    { title: 'タスク2' },
    { title: 'タスク3' }
  ])
  .select()

// upsert（存在すれば更新、なければ追加）
const { data, error } = await supabase
  .from('todos')
  .upsert({ id: 1, title: '更新されたタイトル' })
  .select()`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div><span style="color:#dcdcaa;">.insert()</span> → 追加</div><div><span style="color:#dcdcaa;">.upsert()</span> → 追加 or 更新</div></div>`}
		/>
	</section>

	<!-- UPDATE -->
	<section class="mb-10">
		<h2 id="update" class="text-xl font-bold mb-4">データを更新（UPDATE）</h2>

		<CodePreview
			title="データを更新"
			description="update() でデータを更新"
			language="typescript"
			code={`// 条件を指定して更新
const { data, error } = await supabase
  .from('todos')
  .update({ completed: true })
  .eq('id', 1)  // id = 1 のレコードを更新
  .select()

// 複数カラムを更新
const { data, error } = await supabase
  .from('todos')
  .update({
    title: '新しいタイトル',
    completed: true,
    updated_at: new Date().toISOString()
  })
  .eq('id', 1)
  .select()

// 複数レコードを一括更新
const { data, error } = await supabase
  .from('todos')
  .update({ completed: true })
  .in('id', [1, 2, 3])  // id が 1, 2, 3 のレコード
  .select()`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div style="color:#f14c4c;">⚠️ .eq() などの条件を忘れずに！</div><div style="color:#6a9955;">// 条件なしだと全レコード更新</div></div>`}
		/>
	</section>

	<!-- DELETE -->
	<section class="mb-10">
		<h2 id="delete" class="text-xl font-bold mb-4">データを削除（DELETE）</h2>

		<CodePreview
			title="データを削除"
			description="delete() でデータを削除"
			language="typescript"
			code={`// 条件を指定して削除
const { error } = await supabase
  .from('todos')
  .delete()
  .eq('id', 1)  // id = 1 のレコードを削除

// 複数レコードを削除
const { error } = await supabase
  .from('todos')
  .delete()
  .eq('completed', true)  // 完了済みを全削除

// 削除したデータを取得
const { data, error } = await supabase
  .from('todos')
  .delete()
  .eq('id', 1)
  .select()  // 削除前のデータを返す`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div style="color:#f14c4c;">⚠️ 削除は取り消せない！</div><div style="color:#6a9955;">// 論理削除を検討しよう</div></div>`}
		/>

		<div class="mt-4 p-4 rounded-lg bg-amber-50 dark:bg-amber-900/20 border border-amber-200 dark:border-amber-800">
			<p class="font-semibold text-amber-800 dark:text-amber-200">論理削除 vs 物理削除</p>
			<div class="text-sm text-amber-700 dark:text-amber-300 mt-2">
				<p><strong>物理削除</strong>：<code>DELETE</code> でデータを完全に消す</p>
				<p><strong>論理削除</strong>：<code>deleted_at</code> カラムを追加し、削除日時をセットする</p>
				<p class="mt-2">大事なデータは論理削除がおすすめ。復元が可能になります。</p>
			</div>
		</div>
	</section>

	<!-- リレーション -->
	<section class="mb-10">
		<h2 id="relations" class="text-xl font-bold mb-4">リレーション（テーブル結合）</h2>

		<CodePreview
			title="関連テーブルを一緒に取得"
			description="外部キーで関連付けたデータを取得"
			language="typescript"
			code={`// postsテーブルとusersテーブルがある場合
// posts.user_id → users.id で紐づいている

// 投稿と一緒にユーザー情報も取得
const { data } = await supabase
  .from('posts')
  .select(\`
    id,
    title,
    content,
    users (
      id,
      name,
      avatar_url
    )
  \`)

// 結果:
// [
//   {
//     id: 1,
//     title: "投稿タイトル",
//     content: "本文...",
//     users: { id: 1, name: "田中", avatar_url: "..." }
//   }
// ]`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div style="color:#6a9955;">// JOIN せずに関連データを取得</div></div>`}
		/>
	</section>

	<!-- ナビゲーション -->
	<div class="flex justify-between pt-6 border-t border-gray-200 dark:border-gray-700">
		<a href="/supabase/setup" class="inline-flex items-center gap-2 px-4 py-2 rounded-lg border border-gray-300 dark:border-gray-600 hover:bg-gray-100 dark:hover:bg-gray-800 transition-colors">
			<svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
				<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 19l-7-7 7-7" />
			</svg>
			前へ：セットアップ
		</a>
		<a href="/supabase/auth" class="inline-flex items-center gap-2 px-4 py-2 rounded-lg bg-primary-600 text-white hover:bg-primary-700 transition-colors">
			次へ：認証
			<svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
				<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 5l7 7-7 7" />
			</svg>
		</a>
	</div>
</article>
