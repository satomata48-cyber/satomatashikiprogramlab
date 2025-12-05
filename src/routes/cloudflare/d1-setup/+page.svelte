<script>
	import CodePreview from '$lib/components/CodePreview.svelte';
</script>

<svelte:head>
	<title>D1 セットアップ | さとまたラボ</title>
</svelte:head>

<article>
	<h1 class="text-3xl font-bold mb-2">D1 セットアップ</h1>
	<p class="text-lg text-gray-600 dark:text-gray-400 mb-8">
		Cloudflare D1をSvelteKitで使う準備
	</p>

	<!-- 事前準備 -->
	<section class="mb-10">
		<h2 id="prerequisites" class="text-xl font-bold mb-4">1. 事前準備</h2>

		<div class="space-y-4">
			<div class="p-4 rounded-lg bg-gray-50 dark:bg-gray-800 border-l-4 border-orange-500">
				<p class="font-bold text-orange-600 dark:text-orange-400">Cloudflareアカウント</p>
				<p class="text-sm text-gray-600 dark:text-gray-400 mt-1">
					<a href="https://dash.cloudflare.com/sign-up" target="_blank" class="text-orange-600 hover:underline">cloudflare.com</a> で無料アカウントを作成
				</p>
			</div>

			<div class="p-4 rounded-lg bg-gray-50 dark:bg-gray-800 border-l-4 border-orange-500">
				<p class="font-bold text-orange-600 dark:text-orange-400">Wrangler CLI</p>
				<p class="text-sm text-gray-600 dark:text-gray-400 mt-1">
					Cloudflareの公式CLIツール。D1の作成・管理に使用します。
				</p>
			</div>
		</div>
	</section>

	<!-- Wranglerインストール -->
	<section class="mb-10">
		<h2 id="wrangler" class="text-xl font-bold mb-4">2. Wrangler CLIをインストール</h2>

		<CodePreview
			title="Wranglerをインストール"
			description="グローバルにインストール"
			language="bash"
			code={`# グローバルにインストール
npm install -g wrangler

# プロジェクトローカルにインストール（推奨）
npm install -D wrangler

# バージョン確認
wrangler --version`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div style="color:#6a9955;"># Cloudflare公式CLI</div></div>`}
		/>

		<CodePreview
			title="Cloudflareにログイン"
			description="認証を行う"
			language="bash"
			code={`# ブラウザが開いて認証
wrangler login

# 認証確認
wrangler whoami`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div style="color:#6a9955;"># ブラウザで認証</div></div>`}
		/>
	</section>

	<!-- D1作成 -->
	<section class="mb-10">
		<h2 id="create-d1" class="text-xl font-bold mb-4">3. D1データベースを作成</h2>

		<CodePreview
			title="D1データベースを作成"
			description="wrangler d1 create コマンド"
			language="bash"
			code={`# D1データベースを作成
wrangler d1 create my-database

# 出力例:
# ✅ Successfully created DB 'my-database'
#
# [[d1_databases]]
# binding = "DB"
# database_name = "my-database"
# database_id = "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div style="color:#4ec9b0;">database_id</div><div style="color:#6a9955;">// この値を控えておく</div></div>`}
		/>

		<div class="mt-4 p-4 rounded-lg bg-amber-50 dark:bg-amber-900/20 border border-amber-200 dark:border-amber-800">
			<p class="font-semibold text-amber-800 dark:text-amber-200">出力された設定をメモ！</p>
			<p class="text-sm text-amber-700 dark:text-amber-300 mt-1">
				<code>database_id</code> は後で <code>wrangler.toml</code> に記載します。
			</p>
		</div>
	</section>

	<!-- wrangler.toml設定 -->
	<section class="mb-10">
		<h2 id="config" class="text-xl font-bold mb-4">4. wrangler.tomlを設定</h2>

		<CodePreview
			title="wrangler.toml"
			description="プロジェクトルートに作成"
			language="toml"
			code={`name = "my-sveltekit-app"
compatibility_date = "2024-01-01"
pages_build_output_dir = ".svelte-kit/cloudflare"

# D1データベースの設定
[[d1_databases]]
binding = "DB"  # コード内で使う名前
database_name = "my-database"
database_id = "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"  # 実際のIDに置き換え`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div>binding = <span style="color:#ce9178;">"DB"</span></div><div style="color:#6a9955;">// platform.env.DB でアクセス</div></div>`}
		/>
	</section>

	<!-- テーブル作成 -->
	<section class="mb-10">
		<h2 id="create-table" class="text-xl font-bold mb-4">5. テーブルを作成</h2>

		<CodePreview
			title="schema.sql を作成"
			description="SQLファイルにスキーマを定義"
			language="sql"
			code={`-- schema.sql
CREATE TABLE IF NOT EXISTS todos (
  id INTEGER PRIMARY KEY AUTOINCREMENT,
  title TEXT NOT NULL,
  completed INTEGER DEFAULT 0,
  created_at TEXT DEFAULT CURRENT_TIMESTAMP
);

-- インデックス（検索を高速化）
CREATE INDEX IF NOT EXISTS idx_todos_completed ON todos(completed);`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div style="color:#6a9955;">// SQLiteの標準SQL</div></div>`}
		/>

		<CodePreview
			title="SQLを実行"
			description="ローカルと本番に適用"
			language="bash"
			code={`# ローカル環境に適用
wrangler d1 execute my-database --local --file=./schema.sql

# 本番環境に適用
wrangler d1 execute my-database --remote --file=./schema.sql

# 単一のSQLを実行
wrangler d1 execute my-database --local --command="SELECT * FROM todos"`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div><span style="color:#569cd6;">--local</span> → ローカル</div><div><span style="color:#569cd6;">--remote</span> → 本番</div></div>`}
		/>
	</section>

	<!-- SvelteKit設定 -->
	<section class="mb-10">
		<h2 id="sveltekit-config" class="text-xl font-bold mb-4">6. SvelteKitの設定</h2>

		<CodePreview
			title="Cloudflareアダプターをインストール"
			description="デプロイに必要"
			language="bash"
			code={`npm install -D @sveltejs/adapter-cloudflare`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div style="color:#6a9955;"># Cloudflare Pages用アダプター</div></div>`}
		/>

		<CodePreview
			title="svelte.config.js"
			description="アダプターを設定"
			language="javascript"
			code={`import adapter from '@sveltejs/adapter-cloudflare';
import { vitePreprocess } from '@sveltejs/vite-plugin-svelte';

/** @type {import('@sveltejs/kit').Config} */
const config = {
  preprocess: vitePreprocess(),
  kit: {
    adapter: adapter({
      routes: {
        include: ['/*'],
        exclude: ['<all>']
      }
    })
  }
};

export default config;`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div style="color:#6a9955;">// adapter-cloudflare に変更</div></div>`}
		/>

		<CodePreview
			title="src/app.d.ts"
			description="型定義を追加"
			language="typescript"
			code={`// src/app.d.ts
declare global {
  namespace App {
    interface Platform {
      env: {
        DB: D1Database;  // wrangler.toml の binding と同じ名前
      };
    }
  }
}

export {};`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div style="color:#6a9955;">// TypeScriptの型定義</div></div>`}
		/>
	</section>

	<!-- ローカル開発 -->
	<section class="mb-10">
		<h2 id="local-dev" class="text-xl font-bold mb-4">7. ローカル開発</h2>

		<CodePreview
			title="ローカルでD1を使って開発"
			description="wrangler pages dev コマンド"
			language="bash"
			code={`# ビルドしてローカルでD1を使って実行
npm run build && wrangler pages dev .svelte-kit/cloudflare

# package.json に追加すると便利
# "scripts": {
#   "dev:cf": "npm run build && wrangler pages dev .svelte-kit/cloudflare"
# }`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div style="color:#6a9955;">// D1にアクセスできる開発環境</div></div>`}
		/>

		<div class="mt-4 p-4 rounded-lg bg-blue-50 dark:bg-blue-900/20 border border-blue-200 dark:border-blue-800">
			<p class="font-semibold text-blue-800 dark:text-blue-200">通常の npm run dev では</p>
			<p class="text-sm text-blue-700 dark:text-blue-300 mt-1">
				<code>platform.env</code> が <code>undefined</code> になります。D1を使う場合は <code>wrangler pages dev</code> を使用してください。
			</p>
		</div>
	</section>

	<!-- ナビゲーション -->
	<div class="flex justify-between pt-6 border-t border-gray-200 dark:border-gray-700">
		<a href="/cloudflare/d1" class="inline-flex items-center gap-2 px-4 py-2 rounded-lg border border-gray-300 dark:border-gray-600 hover:bg-gray-100 dark:hover:bg-gray-800 transition-colors">
			<svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
				<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 19l-7-7 7-7" />
			</svg>
			前へ：D1 データベース
		</a>
		<a href="/cloudflare/d1-sql" class="inline-flex items-center gap-2 px-4 py-2 rounded-lg bg-primary-600 text-white hover:bg-primary-700 transition-colors">
			次へ：D1 SQLの基本
			<svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
				<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 5l7 7-7 7" />
			</svg>
		</a>
	</div>
</article>
