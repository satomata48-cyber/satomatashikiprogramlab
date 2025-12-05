<script>
	import CodePreview from '$lib/components/CodePreview.svelte';
	import FeatureCard from '$lib/components/FeatureCard.svelte';

	const features = [
		{ icon: '🗄️', title: 'PostgreSQL', description: 'パワフルなリレーショナルDB', tag: 'データベース' },
		{ icon: '🔐', title: '認証', description: 'ログイン機能を簡単実装', tag: '認証' },
		{ icon: '📁', title: 'ストレージ', description: '画像・ファイルの保存', tag: 'ストレージ' },
		{ icon: '⚡', title: 'リアルタイム', description: 'データ変更を即座に反映', tag: 'リアルタイム' },
		{ icon: '🔧', title: 'Edge Functions', description: 'サーバーレス関数', tag: '機能' },
		{ icon: '🆓', title: '無料枠', description: '個人開発に十分な容量', tag: '料金' }
	];
</script>

<svelte:head>
	<title>Supabase はじめに | さとまたラボ</title>
</svelte:head>

<article>
	<h1 class="text-3xl font-bold mb-2">Supabase</h1>
	<p class="text-lg text-gray-600 dark:text-gray-400 mb-8">
		オープンソースのFirebase代替 - バックエンドを簡単に構築
	</p>

	<!-- Supabaseとは -->
	<section class="mb-10">
		<h2 id="what-is" class="text-xl font-bold mb-4">Supabaseとは？</h2>

		<div class="p-6 rounded-xl bg-emerald-50 dark:bg-emerald-900/20 border border-emerald-200 dark:border-emerald-800 mb-6">
			<p class="text-emerald-800 dark:text-emerald-200 mb-4">
				<strong>一言で言うと：</strong>「バックエンド機能をまとめて提供してくれるサービス」
			</p>
			<div class="grid grid-cols-1 md:grid-cols-2 gap-4 text-sm">
				<div class="p-3 bg-white dark:bg-gray-800 rounded-lg">
					<div class="font-semibold text-emerald-700 dark:text-emerald-300 mb-2">自分で作ると大変...</div>
					<ul class="text-gray-600 dark:text-gray-400 space-y-1">
						<li>・データベースサーバーの構築</li>
						<li>・ユーザー認証システムの実装</li>
						<li>・ファイルアップロード機能</li>
						<li>・APIの設計と実装</li>
					</ul>
				</div>
				<div class="p-3 bg-white dark:bg-gray-800 rounded-lg">
					<div class="font-semibold text-emerald-700 dark:text-emerald-300 mb-2">Supabaseなら...</div>
					<ul class="text-gray-600 dark:text-gray-400 space-y-1">
						<li>・クリックでDB作成、自動でAPI生成</li>
						<li>・認証機能が数行のコードで完成</li>
						<li>・ストレージもすぐ使える</li>
						<li>・管理画面で簡単に操作</li>
					</ul>
				</div>
			</div>
		</div>

		<div class="p-4 rounded-lg bg-amber-50 dark:bg-amber-900/20 border border-amber-200 dark:border-amber-800 mb-6">
			<p class="font-semibold text-amber-800 dark:text-amber-200">Firebaseとの違い</p>
			<div class="text-sm text-amber-700 dark:text-amber-300 mt-2">
				<div class="grid md:grid-cols-2 gap-4">
					<div>
						<p class="font-medium mb-1">Firebase (Google)</p>
						<ul class="space-y-1">
							<li>・NoSQL（ドキュメント型）</li>
							<li>・クローズドソース</li>
							<li>・独自のクエリ言語</li>
						</ul>
					</div>
					<div>
						<p class="font-medium mb-1">Supabase</p>
						<ul class="space-y-1">
							<li>・PostgreSQL（リレーショナル）</li>
							<li>・オープンソース</li>
							<li>・標準的なSQL</li>
						</ul>
					</div>
				</div>
			</div>
		</div>
	</section>

	<!-- できること一覧 -->
	<section class="mb-10">
		<h2 id="features" class="text-xl font-bold mb-4">Supabaseでできること</h2>
		<div class="grid grid-cols-1 md:grid-cols-2 gap-3">
			{#each features as feature}
				<FeatureCard {...feature} />
			{/each}
		</div>
	</section>

	<!-- コード例 -->
	<section class="mb-10">
		<h2 id="examples" class="text-xl font-bold mb-4">コード例</h2>

		<CodePreview
			title="データの取得"
			description="テーブルからデータを取得"
			language="typescript"
			code={`import { createClient } from '@supabase/supabase-js'

// Supabaseクライアントの初期化
const supabase = createClient(
  'https://あなたのプロジェクト.supabase.co',
  'あなたのAPIキー'
)

// todosテーブルから全データを取得
const { data, error } = await supabase
  .from('todos')
  .select('*')

// 条件付きで取得
const { data: activeTodos } = await supabase
  .from('todos')
  .select('*')
  .eq('completed', false)  // completed = false のものだけ
  .order('created_at', { ascending: false })  // 新しい順`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div style="color:#6a9955;">// SQLを書かなくてもOK</div><div>supabase.from('todos').select('*')</div><div style="color:#6a9955;">// ↑ これだけでデータ取得！</div></div>`}
		/>

		<CodePreview
			title="データの追加・更新・削除"
			description="CRUD操作"
			language="typescript"
			code={`// データを追加（INSERT）
const { data, error } = await supabase
  .from('todos')
  .insert({ title: '買い物', completed: false })
  .select()  // 追加したデータを返す

// データを更新（UPDATE）
await supabase
  .from('todos')
  .update({ completed: true })
  .eq('id', 1)  // id = 1 のレコードを更新

// データを削除（DELETE）
await supabase
  .from('todos')
  .delete()
  .eq('id', 1)  // id = 1 のレコードを削除`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div><span style="color:#4ec9b0;">.insert()</span> → 追加</div><div><span style="color:#4ec9b0;">.update()</span> → 更新</div><div><span style="color:#4ec9b0;">.delete()</span> → 削除</div></div>`}
		/>

		<CodePreview
			title="ユーザー認証"
			description="サインアップとログイン"
			language="typescript"
			code={`// メールでサインアップ
const { data, error } = await supabase.auth.signUp({
  email: 'user@example.com',
  password: 'password123'
})

// ログイン
const { data, error } = await supabase.auth.signInWithPassword({
  email: 'user@example.com',
  password: 'password123'
})

// Googleでログイン
await supabase.auth.signInWithOAuth({
  provider: 'google'
})

// ログアウト
await supabase.auth.signOut()

// 現在のユーザーを取得
const { data: { user } } = await supabase.auth.getUser()`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div style="color:#6a9955;">// 認証機能が数行で実装できる</div><div>supabase.auth.<span style="color:#dcdcaa;">signUp</span>()</div><div>supabase.auth.<span style="color:#dcdcaa;">signIn</span>()</div><div>supabase.auth.<span style="color:#dcdcaa;">signOut</span>()</div></div>`}
		/>
	</section>

	<!-- アーキテクチャ -->
	<section class="mb-10">
		<h2 id="architecture" class="text-xl font-bold mb-4">Supabaseの構成</h2>

		<div class="p-4 rounded-lg bg-gray-100 dark:bg-gray-800">
			<pre class="text-sm overflow-x-auto"><code>┌─────────────────────────────────────────────────┐
│                  あなたのアプリ                    │
│              (SvelteKit / Next.js)               │
└───────────────────────┬─────────────────────────┘
                        │ API呼び出し
                        ▼
┌─────────────────────────────────────────────────┐
│                   Supabase                       │
├─────────────┬─────────────┬─────────────────────┤
│  Database   │    Auth     │     Storage         │
│ (PostgreSQL)│   (認証)     │    (ファイル)        │
├─────────────┴─────────────┴─────────────────────┤
│              Realtime (リアルタイム同期)           │
├─────────────────────────────────────────────────┤
│              Edge Functions (サーバーレス)        │
└─────────────────────────────────────────────────┘</code></pre>
		</div>

		<div class="mt-4 p-4 rounded-lg bg-blue-50 dark:bg-blue-900/20 border border-blue-200 dark:border-blue-800">
			<p class="font-semibold text-blue-800 dark:text-blue-200 mb-2">ポイント</p>
			<ul class="text-sm text-blue-700 dark:text-blue-300 space-y-1">
				<li>・<strong>PostgREST</strong>：PostgreSQLテーブルから自動でREST APIを生成</li>
				<li>・<strong>GoTrue</strong>：認証サービス（JWT発行、OAuthなど）</li>
				<li>・<strong>Realtime</strong>：WebSocketでデータ変更をリアルタイム配信</li>
				<li>・<strong>Storage</strong>：S3互換のオブジェクトストレージ</li>
			</ul>
		</div>
	</section>

	<!-- 料金 -->
	<section class="mb-10">
		<h2 id="pricing" class="text-xl font-bold mb-4">料金プラン</h2>

		<div class="grid md:grid-cols-2 gap-4">
			<div class="p-4 rounded-lg bg-gray-50 dark:bg-gray-800 border border-gray-200 dark:border-gray-700">
				<h3 class="font-bold text-lg mb-2">Free（無料）</h3>
				<ul class="text-sm text-gray-600 dark:text-gray-400 space-y-1">
					<li>・データベース: 500MB</li>
					<li>・ストレージ: 1GB</li>
					<li>・帯域: 2GB/月</li>
					<li>・Edge Functions: 500,000回/月</li>
					<li>・プロジェクト: 2個まで</li>
				</ul>
				<p class="mt-2 text-xs text-gray-500">個人開発・学習には十分！</p>
			</div>
			<div class="p-4 rounded-lg bg-emerald-50 dark:bg-emerald-900/20 border border-emerald-200 dark:border-emerald-800">
				<h3 class="font-bold text-lg mb-2">Pro（$25/月〜）</h3>
				<ul class="text-sm text-gray-600 dark:text-gray-400 space-y-1">
					<li>・データベース: 8GB</li>
					<li>・ストレージ: 100GB</li>
					<li>・帯域: 250GB/月</li>
					<li>・毎日の自動バックアップ</li>
					<li>・7日間のログ保持</li>
				</ul>
				<p class="mt-2 text-xs text-emerald-600 dark:text-emerald-400">本番環境向け</p>
			</div>
		</div>
	</section>

	<!-- 始め方 -->
	<section class="mb-10">
		<h2 id="getting-started" class="text-xl font-bold mb-4">始め方（3ステップ）</h2>

		<div class="space-y-4">
			<div class="p-4 rounded-lg bg-gray-50 dark:bg-gray-800 border-l-4 border-emerald-500">
				<p class="font-bold text-emerald-600 dark:text-emerald-400">Step 1: アカウント作成</p>
				<p class="text-sm text-gray-600 dark:text-gray-400 mt-1">
					<a href="https://supabase.com" target="_blank" class="text-emerald-600 hover:underline">supabase.com</a> でGitHubアカウントでサインアップ
				</p>
			</div>

			<div class="p-4 rounded-lg bg-gray-50 dark:bg-gray-800 border-l-4 border-emerald-500">
				<p class="font-bold text-emerald-600 dark:text-emerald-400">Step 2: プロジェクト作成</p>
				<p class="text-sm text-gray-600 dark:text-gray-400 mt-1">
					「New Project」でプロジェクト名とデータベースパスワードを設定
				</p>
			</div>

			<div class="p-4 rounded-lg bg-gray-50 dark:bg-gray-800 border-l-4 border-emerald-500">
				<p class="font-bold text-emerald-600 dark:text-emerald-400">Step 3: APIキー取得</p>
				<p class="text-sm text-gray-600 dark:text-gray-400 mt-1">
					Settings → API から「Project URL」と「anon key」をコピー
				</p>
			</div>
		</div>
	</section>

	<!-- ナビゲーション -->
	<div class="flex justify-between pt-6 border-t border-gray-200 dark:border-gray-700">
		<a href="/tailwind/customize" class="inline-flex items-center gap-2 px-4 py-2 rounded-lg border border-gray-300 dark:border-gray-600 hover:bg-gray-100 dark:hover:bg-gray-800 transition-colors">
			<svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
				<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 19l-7-7 7-7" />
			</svg>
			前へ：Tailwind
		</a>
		<a href="/supabase/setup" class="inline-flex items-center gap-2 px-4 py-2 rounded-lg bg-primary-600 text-white hover:bg-primary-700 transition-colors">
			次へ：セットアップ
			<svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
				<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 5l7 7-7 7" />
			</svg>
		</a>
	</div>
</article>
