<script>
	import CodePreview from '$lib/components/CodePreview.svelte';
</script>

<svelte:head>
	<title>個人開発 SvelteKit + D1 ベストプラクティス | さとまたラボ</title>
</svelte:head>

<article>
	<h1 class="text-3xl font-bold mb-2">個人開発のための SvelteKit + D1 ベストプラクティス</h1>
	<p class="text-lg text-gray-600 dark:text-gray-400 mb-8">
		SvelteKit + Tailwind + Cloudflare D1 で効率よく個人開発を進めるためのガイド（2025年版）
	</p>

	<!-- 概要 -->
	<section class="mb-12">
		<h2 id="overview" class="text-xl font-bold mb-4">このガイドについて</h2>

		<div class="p-6 rounded-xl bg-gradient-to-r from-orange-50 to-blue-50 dark:from-orange-900/20 dark:to-blue-900/20 border border-orange-200 dark:border-orange-800 mb-6">
			<p class="text-lg text-orange-800 dark:text-orange-200 mb-4">
				<strong>個人開発者のための</strong>実践的ガイド
			</p>
			<p class="text-sm text-orange-700 dark:text-orange-300">
				時間もリソースも限られた個人開発では、効率化が命。
				このガイドでは、SvelteKit + Tailwind + D1 の技術スタックで
				<strong>スピード重視</strong>で開発を進めながら、<strong>最低限の品質</strong>を担保する方法を紹介します。
			</p>
		</div>

		<div class="grid md:grid-cols-4 gap-3 mb-6">
			<div class="p-3 rounded-lg bg-orange-50 dark:bg-orange-900/20 border border-orange-200 dark:border-orange-800 text-center">
				<span class="text-2xl">🔥</span>
				<p class="text-sm font-medium text-orange-800 dark:text-orange-200 mt-1">SvelteKit</p>
			</div>
			<div class="p-3 rounded-lg bg-cyan-50 dark:bg-cyan-900/20 border border-cyan-200 dark:border-cyan-800 text-center">
				<span class="text-2xl">💨</span>
				<p class="text-sm font-medium text-cyan-800 dark:text-cyan-200 mt-1">Tailwind v4</p>
			</div>
			<div class="p-3 rounded-lg bg-blue-50 dark:bg-blue-900/20 border border-blue-200 dark:border-blue-800 text-center">
				<span class="text-2xl">🗄️</span>
				<p class="text-sm font-medium text-blue-800 dark:text-blue-200 mt-1">D1</p>
			</div>
			<div class="p-3 rounded-lg bg-gray-50 dark:bg-gray-800 border border-gray-200 dark:border-gray-700 text-center">
				<span class="text-2xl">☁️</span>
				<p class="text-sm font-medium text-gray-800 dark:text-gray-200 mt-1">Cloudflare</p>
			</div>
		</div>

		<!-- 個人開発のメリット -->
		<div class="p-4 rounded-lg bg-emerald-50 dark:bg-emerald-900/20 border border-emerald-200 dark:border-emerald-800">
			<p class="font-semibold text-emerald-800 dark:text-emerald-200 mb-2">この技術スタックが個人開発に最適な理由</p>
			<ul class="text-sm text-emerald-700 dark:text-emerald-300 space-y-1">
				<li>・<strong>無料枠が充実</strong>：D1は1日5,000,000読み取り・100,000書き込み無料</li>
				<li>・<strong>サーバー管理不要</strong>：Cloudflare Edgeで自動スケール</li>
				<li>・<strong>フロントとバックが同居</strong>：SvelteKitで一元管理</li>
				<li>・<strong>世界中で高速</strong>：エッジで実行されるので低レイテンシ</li>
			</ul>
		</div>
	</section>

	<!-- 個人開発の心構え -->
	<section class="mb-12">
		<h2 id="mindset" class="text-xl font-bold mb-4">個人開発の心構え（2025年版）</h2>

		<div class="space-y-4 mb-6">
			<div class="p-4 rounded-lg bg-purple-50 dark:bg-purple-900/20 border border-purple-200 dark:border-purple-800">
				<p class="font-semibold text-purple-800 dark:text-purple-200 mb-2">1. 完璧を求めない</p>
				<p class="text-sm text-purple-700 dark:text-purple-300">
					「伸びないプロダクトほど完成度が高い」という逆説があります。
					β版でいいから<strong>とにかく出す</strong>ことが重要。完成より拡散導線に力を入れましょう。
				</p>
			</div>

			<div class="p-4 rounded-lg bg-blue-50 dark:bg-blue-900/20 border border-blue-200 dark:border-blue-800">
				<p class="font-semibold text-blue-800 dark:text-blue-200 mb-2">2. AIを積極活用</p>
				<p class="text-sm text-blue-700 dark:text-blue-300">
					2025年の個人開発では、AIをうまく活用することが成功の鍵。
					Claude Code、GitHub Copilot、Cursor などを使って
					「考えるべきこと」に集中しましょう。
				</p>
			</div>

			<div class="p-4 rounded-lg bg-amber-50 dark:bg-amber-900/20 border border-amber-200 dark:border-amber-800">
				<p class="font-semibold text-amber-800 dark:text-amber-200 mb-2">3. シンプルに保つ</p>
				<p class="text-sm text-amber-700 dark:text-amber-300">
					チーム開発の複雑なワークフローは不要。Git Flow より GitHub Flow、
					複雑な CI/CD より Cloudflare の自動デプロイ。個人開発に合った規模感で。
				</p>
			</div>
		</div>
	</section>

	<!-- 環境構築 -->
	<section class="mb-12">
		<h2 id="setup" class="text-xl font-bold mb-4">プロジェクトセットアップ（2025年最新）</h2>

		<CodePreview
			title="1. SvelteKit プロジェクト作成"
			description="Tailwindを含めて一発で"
			language="bash"
			code={`# SvelteKit + Tailwind を一発でセットアップ
npx sv create my-app
cd my-app
npm install

# Cloudflare アダプターを追加
npm i -D @sveltejs/adapter-cloudflare`}
		/>

		<div class="mt-4 p-4 rounded-lg bg-amber-50 dark:bg-amber-900/20 border border-amber-200 dark:border-amber-800">
			<p class="font-semibold text-amber-800 dark:text-amber-200 mb-2">注意: adapter-cloudflare を使う</p>
			<p class="text-sm text-amber-700 dark:text-amber-300">
				<code>adapter-cloudflare-workers</code> は非推奨です。
				新規プロジェクトでは <code>adapter-cloudflare</code> を使いましょう。
			</p>
		</div>

		<CodePreview
			title="2. svelte.config.js"
			description="Cloudflare アダプター設定"
			language="javascript"
			code={`import adapter from '@sveltejs/adapter-cloudflare';
import { vitePreprocess } from '@sveltejs/vite-plugin-svelte';

export default {
  preprocess: vitePreprocess(),
  kit: {
    adapter: adapter({
      routes: {
        include: ['/*'],
        exclude: ['<all>']
      },
      platformProxy: {
        configPath: 'wrangler.json',
        persist: true  // ローカルDBを永続化
      }
    })
  }
};`}
		/>

		<CodePreview
			title="3. wrangler.json（推奨形式）"
			description="tomlより新しいJSON形式"
			language="json"
			code={`{
  "name": "my-app",
  "compatibility_date": "2025-01-01",
  "pages_build_output_dir": ".svelte-kit/cloudflare",
  "d1_databases": [
    {
      "binding": "DB",
      "database_name": "my-app-db",
      "database_id": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
      "migrations_dir": "migrations"
    }
  ]
}`}
		/>

		<CodePreview
			title="4. src/app.d.ts"
			description="D1の型定義"
			language="typescript"
			code={`declare global {
  namespace App {
    interface Platform {
      env: {
        DB: D1Database;
      };
      context: {
        waitUntil(promise: Promise<unknown>): void;
      };
    }
  }
}

export {};`}
		/>
	</section>

	<!-- Tailwind v4 設定 -->
	<section class="mb-12">
		<h2 id="tailwind" class="text-xl font-bold mb-4">Tailwind CSS v4（2025年最新）</h2>

		<div class="p-4 rounded-lg bg-cyan-50 dark:bg-cyan-900/20 border border-cyan-200 dark:border-cyan-800 mb-4">
			<p class="font-semibold text-cyan-800 dark:text-cyan-200 mb-2">v4 の大きな変更点</p>
			<ul class="text-sm text-cyan-700 dark:text-cyan-300 space-y-1">
				<li>・<code>tailwind.config.js</code> 不要 → CSSで直接テーマ設定</li>
				<li>・<code>@tailwind base/components/utilities</code> 廃止 → <code>@import "tailwindcss"</code> のみ</li>
				<li>・Vite プラグインで設定: <code>@tailwindcss/vite</code></li>
			</ul>
		</div>

		<CodePreview
			title="vite.config.ts"
			description="Tailwind v4 プラグイン設定"
			language="typescript"
			code={`import { sveltekit } from '@sveltejs/kit/vite';
import tailwindcss from '@tailwindcss/vite';
import { defineConfig } from 'vite';

export default defineConfig({
  plugins: [
    tailwindcss(),
    sveltekit()
  ]
});`}
		/>

		<CodePreview
			title="src/app.css"
			description="Tailwind v4 スタイル"
			language="css"
			code={`@import "tailwindcss";

/* v4ではCSSでテーマをカスタマイズ */
@theme {
  --color-primary-500: #3b82f6;
  --color-primary-600: #2563eb;
  --font-sans: 'Noto Sans JP', sans-serif;
}`}
		/>

		<div class="mt-4 p-4 rounded-lg bg-amber-50 dark:bg-amber-900/20 border border-amber-200 dark:border-amber-800">
			<p class="font-semibold text-amber-800 dark:text-amber-200 mb-2">互換性に注意</p>
			<p class="text-sm text-amber-700 dark:text-amber-300">
				Tailwind v4 は Safari 16.4+、Chrome 111+、Firefox 128+ が必要です。
				古いブラウザをサポートする場合は v3.4 を使いましょう。
			</p>
		</div>
	</section>

	<!-- プロジェクト構成 -->
	<section class="mb-12">
		<h2 id="structure" class="text-xl font-bold mb-4">個人開発向けプロジェクト構成</h2>

		<p class="text-gray-700 dark:text-gray-300 mb-4">
			個人開発では<strong>シンプルさ</strong>が重要。必要最小限の構成から始めましょう。
		</p>

		<CodePreview
			title="ディレクトリ構造"
			description="シンプルで拡張しやすい構成"
			language="text"
			code={`my-app/
├── src/
│   ├── lib/
│   │   ├── components/      # UIコンポーネント
│   │   │   ├── Button.svelte
│   │   │   └── Modal.svelte
│   │   ├── server/          # サーバー専用コード
│   │   │   └── db.ts        # D1ヘルパー
│   │   └── utils/           # ユーティリティ
│   │       └── validation.ts
│   ├── routes/
│   │   ├── +layout.svelte
│   │   ├── +page.svelte
│   │   ├── +page.server.ts
│   │   └── api/
│   │       └── +server.ts
│   ├── app.css
│   └── app.d.ts
├── migrations/               # D1マイグレーション
│   └── 0001_initial.sql
├── wrangler.json
├── svelte.config.js
└── vite.config.ts`}
		/>

		<div class="mt-4 p-4 rounded-lg bg-blue-50 dark:bg-blue-900/20 border border-blue-200 dark:border-blue-800">
			<p class="font-semibold text-blue-800 dark:text-blue-200 mb-2">個人開発のコツ</p>
			<p class="text-sm text-blue-700 dark:text-blue-300">
				最初から複雑な構成にしない。機能が増えたら徐々に整理する。
				<code>lib/server/</code> はサーバー専用コードを置くと、
				クライアントに漏れる心配がなくなります。
			</p>
		</div>
	</section>

	<!-- Drizzle ORM -->
	<section class="mb-12">
		<h2 id="drizzle" class="text-xl font-bold mb-4">Drizzle ORM の活用（推奨）</h2>

		<div class="p-4 rounded-lg bg-emerald-50 dark:bg-emerald-900/20 border border-emerald-200 dark:border-emerald-800 mb-4">
			<p class="font-semibold text-emerald-800 dark:text-emerald-200 mb-2">なぜ Drizzle？</p>
			<ul class="text-sm text-emerald-700 dark:text-emerald-300 space-y-1">
				<li>・<strong>依存関係ゼロ</strong>：サーバーレス環境に最適</li>
				<li>・<strong>型安全</strong>：TypeScript との相性抜群</li>
				<li>・<strong>SQLに近い</strong>：学習コストが低い</li>
				<li>・<strong>D1対応</strong>：公式サポート</li>
			</ul>
		</div>

		<CodePreview
			title="インストール"
			description=""
			language="bash"
			code={`npm install drizzle-orm
npm install -D drizzle-kit`}
		/>

		<CodePreview
			title="src/lib/server/schema.ts"
			description="Drizzle スキーマ定義"
			language="typescript"
			code={`import { sqliteTable, text, integer } from 'drizzle-orm/sqlite-core';

export const todos = sqliteTable('todos', {
  id: integer('id').primaryKey({ autoIncrement: true }),
  title: text('title').notNull(),
  completed: integer('completed', { mode: 'boolean' }).default(false),
  createdAt: text('created_at').default('CURRENT_TIMESTAMP')
});

export type Todo = typeof todos.$inferSelect;
export type NewTodo = typeof todos.$inferInsert;`}
		/>

		<CodePreview
			title="src/lib/server/db.ts"
			description="Drizzle + D1 接続"
			language="typescript"
			code={`import { drizzle } from 'drizzle-orm/d1';
import * as schema from './schema';

export function getDB(platform: App.Platform | undefined) {
  if (!platform?.env?.DB) {
    throw new Error('Database not available');
  }
  return drizzle(platform.env.DB, { schema });
}

// 使用例
export async function getTodos(platform: App.Platform) {
  const db = getDB(platform);
  return await db.select().from(schema.todos).all();
}

export async function createTodo(platform: App.Platform, title: string) {
  const db = getDB(platform);
  return await db.insert(schema.todos).values({ title }).returning();
}`}
		/>

		<CodePreview
			title="+page.server.ts での使用"
			description="シンプルなCRUD"
			language="typescript"
			code={`import type { PageServerLoad, Actions } from './$types';
import { getTodos, createTodo } from '$lib/server/db';
import { fail } from '@sveltejs/kit';

export const load: PageServerLoad = async ({ platform }) => {
  const todos = await getTodos(platform);
  return { todos };
};

export const actions: Actions = {
  create: async ({ request, platform }) => {
    const formData = await request.formData();
    const title = formData.get('title') as string;

    if (!title?.trim()) {
      return fail(400, { error: 'タイトルは必須です' });
    }

    await createTodo(platform, title.trim());
    return { success: true };
  }
};`}
		/>
	</section>

	<!-- マイグレーション -->
	<section class="mb-12">
		<h2 id="migrations" class="text-xl font-bold mb-4">D1 マイグレーション管理</h2>

		<p class="text-gray-700 dark:text-gray-300 mb-4">
			wrangler 3.33.0 以降、マイグレーションコマンドはデフォルトでローカルDBを使用します。
			本番に適用するには <code>--remote</code> フラグが必要です。
		</p>

		<CodePreview
			title="migrations/0001_initial.sql"
			description="初期テーブル"
			language="sql"
			code={`-- 0001_initial.sql
CREATE TABLE IF NOT EXISTS todos (
  id INTEGER PRIMARY KEY AUTOINCREMENT,
  title TEXT NOT NULL,
  completed INTEGER DEFAULT 0,
  created_at TEXT DEFAULT CURRENT_TIMESTAMP
);

CREATE INDEX IF NOT EXISTS idx_todos_created ON todos(created_at);`}
		/>

		<CodePreview
			title="マイグレーション実行"
			description="ローカルと本番"
			language="bash"
			code={`# マイグレーションファイル作成
npx wrangler d1 migrations create my-app-db add_users

# ローカルに適用（デフォルト）
npx wrangler d1 migrations apply my-app-db

# 本番に適用（--remote 必須）
npx wrangler d1 migrations apply my-app-db --remote`}
		/>

		<div class="mt-4 p-4 rounded-lg bg-amber-50 dark:bg-amber-900/20 border border-amber-200 dark:border-amber-800">
			<p class="font-semibold text-amber-800 dark:text-amber-200 mb-2">個人開発のマイグレーションTips</p>
			<ul class="text-sm text-amber-700 dark:text-amber-300 space-y-1">
				<li>・本番適用前に必ずローカルでテスト</li>
				<li>・一度適用したファイルは変更しない</li>
				<li>・binding名より database_name を使う（変更されないため安全）</li>
				<li>・外部キー制約を変更する場合は <code>PRAGMA defer_foreign_keys = true</code></li>
			</ul>
		</div>
	</section>

	<!-- ローカル開発 -->
	<section class="mb-12">
		<h2 id="local-dev" class="text-xl font-bold mb-4">ローカル開発環境</h2>

		<p class="text-gray-700 dark:text-gray-300 mb-4">
			SvelteKit + Cloudflare の魅力は、<strong>Miniflare</strong>で本番とほぼ同じ環境をローカルで再現できること。
		</p>

		<div class="grid md:grid-cols-2 gap-4 mb-4">
			<div class="p-4 rounded-lg bg-blue-50 dark:bg-blue-900/20 border border-blue-200 dark:border-blue-800">
				<p class="font-semibold text-blue-800 dark:text-blue-200 mb-2">npm run dev</p>
				<p class="text-sm text-blue-700 dark:text-blue-300">
					Vite の開発サーバー。高速だがD1は使えない。
					UI開発やスタイリング作業に最適。
				</p>
			</div>
			<div class="p-4 rounded-lg bg-green-50 dark:bg-green-900/20 border border-green-200 dark:border-green-800">
				<p class="font-semibold text-green-800 dark:text-green-200 mb-2">wrangler pages dev</p>
				<p class="text-sm text-green-700 dark:text-green-300">
					Miniflare で本番環境を再現。D1にアクセス可能。
					DB連携の開発・テストに使用。
				</p>
			</div>
		</div>

		<CodePreview
			title="package.json スクリプト"
			description="個人開発向け最小構成"
			language="json"
			code={`{
  "scripts": {
    "dev": "vite dev",
    "dev:full": "npm run build && wrangler pages dev .svelte-kit/cloudflare",
    "build": "vite build",
    "preview": "wrangler pages dev .svelte-kit/cloudflare",
    "deploy": "npm run build && wrangler pages deploy .svelte-kit/cloudflare",
    "db:migrate": "wrangler d1 migrations apply my-app-db",
    "db:migrate:prod": "wrangler d1 migrations apply my-app-db --remote",
    "db:reset": "rm -rf .wrangler && npm run db:migrate"
  }
}`}
		/>

		<div class="mt-4 p-4 rounded-lg bg-purple-50 dark:bg-purple-900/20 border border-purple-200 dark:border-purple-800">
			<p class="font-semibold text-purple-800 dark:text-purple-200 mb-2">開発フロー</p>
			<ol class="text-sm text-purple-700 dark:text-purple-300 space-y-1 list-decimal list-inside">
				<li>UI作業は <code>npm run dev</code> で高速開発</li>
				<li>DB連携が必要になったら <code>npm run dev:full</code></li>
				<li>デプロイ前に <code>npm run preview</code> で確認</li>
				<li><code>npm run deploy</code> で本番へ</li>
			</ol>
		</div>
	</section>

	<!-- バリデーション -->
	<section class="mb-12">
		<h2 id="validation" class="text-xl font-bold mb-4">入力バリデーション（Zod）</h2>

		<p class="text-gray-700 dark:text-gray-300 mb-4">
			個人開発でも入力チェックは必須。Zod を使えば型安全に書けます。
		</p>

		<CodePreview
			title="src/lib/utils/validation.ts"
			description="シンプルなバリデーション"
			language="typescript"
			code={`import { z } from 'zod';

export const todoSchema = z.object({
  title: z
    .string()
    .min(1, 'タイトルは必須です')
    .max(100, '100文字以内で入力してください')
    .trim()
});

// フォームデータをパース
export function parseForm<T>(
  formData: FormData,
  schema: z.ZodSchema<T>
) {
  const raw: Record<string, unknown> = {};
  for (const [key, value] of formData.entries()) {
    raw[key] = value;
  }

  const result = schema.safeParse(raw);
  if (result.success) {
    return { ok: true as const, data: result.data };
  }

  const errors: Record<string, string> = {};
  for (const err of result.error.errors) {
    errors[err.path.join('.')] = err.message;
  }
  return { ok: false as const, errors };
}`}
		/>
	</section>

	<!-- デプロイ前のテスト -->
	<section class="mb-12">
		<h2 id="testing" class="text-xl font-bold mb-4">AIに任せるテスト戦略</h2>

		<div class="p-4 rounded-lg bg-gradient-to-r from-purple-50 to-blue-50 dark:from-purple-900/20 dark:to-blue-900/20 border border-purple-200 dark:border-purple-800 mb-6">
			<p class="text-lg text-purple-800 dark:text-purple-200 mb-2">
				<strong>テストもAIに丸投げ</strong>する時代
			</p>
			<p class="text-sm text-purple-700 dark:text-purple-300">
				Claude Code はテストコードの自動生成が得意。プロンプトを打つだけで、
				人間が忘れがちなエッジケースまでカバーしてくれます。
				<strong>自分でテストを書く必要はありません。</strong>
			</p>
		</div>

		<!-- Claude Code でテスト生成 -->
		<h3 class="text-lg font-semibold mb-3">Claude Code にテストを書かせる</h3>

		<div class="p-4 rounded-lg bg-blue-50 dark:bg-blue-900/20 border border-blue-200 dark:border-blue-800 mb-4">
			<p class="font-semibold text-blue-800 dark:text-blue-200 mb-2">Claude Code のテスト生成能力</p>
			<p class="text-sm text-blue-700 dark:text-blue-300">
				Claude Code は単にテストを速く書くだけでなく、<strong>人間が書き忘れるテストを書いてくれます</strong>。
				関数を指定すると、正常系・異常系・境界値・エッジケースを自動で分析してテストを生成します。
			</p>
		</div>

		<CodePreview
			title="プロンプト例：ユニットテスト生成"
			description="Claude Code に投げるだけ"
			language="text"
			code={`# バリデーション関数のテストを生成
src/lib/utils/validation.ts のテストを書いて。
正常系、異常系、境界値テストを含めて。

# 特定の関数のテストを生成
getTodos 関数のユニットテストを書いて。
モックを使ってD1への依存を切り離して。

# カバレッジ80%を目指す
src/lib/server/ 配下のすべての関数に対して
テストを生成して。カバレッジ80%以上を目指して。`}
		/>

		<CodePreview
			title="プロンプト例：テスト実行と修正"
			description="実行→修正もAIに任せる"
			language="text"
			code={`# テスト実行して失敗を修正
npm run test を実行して、失敗したテストがあれば修正して。

# 型エラーも一緒に直す
npm run check と npm run test を実行して、
エラーがあればすべて修正して。`}
		/>

		<!-- Playwright MCP -->
		<h3 class="text-lg font-semibold mb-3 mt-6">Playwright MCP でE2Eテストも自動化</h3>

		<div class="p-4 rounded-lg bg-gradient-to-r from-orange-50 to-red-50 dark:from-orange-900/20 dark:to-red-900/20 border border-orange-200 dark:border-orange-800 mb-4">
			<p class="font-semibold text-orange-800 dark:text-orange-200 mb-2">Claude Code が「目」を持つ</p>
			<p class="text-sm text-orange-700 dark:text-orange-300">
				<strong>Playwright MCP Server</strong> を使うと、Claude Code が実際のブラウザを操作できます。
				「ログインページを開いて、フォームに入力して、送信ボタンを押して」と
				日本語で指示するだけでE2Eテストが実行されます。
			</p>
		</div>

		<CodePreview
			title="Playwright MCP のセットアップ"
			description="Claude Code に MCP サーバーを追加"
			language="bash"
			code={`# Microsoft 公式の Playwright MCP をインストール
claude mcp add playwright -- npx @anthropic-ai/mcp-server-playwright

# または ExecuteAutomation 版
claude mcp add playwright -- npx @executeautomation/playwright-mcp-server`}
		/>

		<CodePreview
			title="プロンプト例：E2Eテスト実行"
			description="日本語で指示するだけ"
			language="text"
			code={`# ブラウザを開いてテスト
Playwright MCP を使って http://localhost:5173 を開いて、
Todo追加フォームに「テストタスク」と入力して送信ボタンを押して。
追加されたか確認して。

# ログインフローをテスト
Playwright MCP でログインページを開いて。
メールアドレスに test@example.com、パスワードに password123 を入力して
ログインボタンを押して。ダッシュボードに遷移したか確認して。

# スクリーンショットを撮る
現在のページのスクリーンショットを撮って、UIに問題がないか確認して。`}
		/>

		<div class="mt-4 p-4 rounded-lg bg-green-50 dark:bg-green-900/20 border border-green-200 dark:border-green-800">
			<p class="font-semibold text-green-800 dark:text-green-200 mb-2">Playwright MCP のメリット</p>
			<ul class="text-sm text-green-700 dark:text-green-300 space-y-1">
				<li>・<strong>自然言語でテスト</strong>：コードを書かずに日本語で指示</li>
				<li>・<strong>視覚的な確認</strong>：Claude がページを「見て」判断</li>
				<li>・<strong>探索的テスト</strong>：「このページで問題を探して」も可能</li>
				<li>・<strong>認証も簡単</strong>：ブラウザが見えるので自分でログインしてから続行</li>
			</ul>
		</div>

		<!-- 自動テスト生成のワークフロー -->
		<h3 class="text-lg font-semibold mb-3 mt-6">AIテストの実践ワークフロー</h3>

		<div class="space-y-3">
			<div class="flex items-start gap-3 p-3 rounded-lg bg-gray-50 dark:bg-gray-800">
				<span class="flex-shrink-0 w-8 h-8 flex items-center justify-center rounded-full bg-blue-500 text-white font-bold">1</span>
				<div>
					<p class="font-semibold">機能を実装したら</p>
					<p class="text-sm text-gray-600 dark:text-gray-400">
						Claude Code に「この関数のテストを書いて」と依頼
					</p>
				</div>
			</div>
			<div class="flex items-start gap-3 p-3 rounded-lg bg-gray-50 dark:bg-gray-800">
				<span class="flex-shrink-0 w-8 h-8 flex items-center justify-center rounded-full bg-blue-500 text-white font-bold">2</span>
				<div>
					<p class="font-semibold">テスト実行</p>
					<p class="text-sm text-gray-600 dark:text-gray-400">
						「npm run test を実行して、失敗があれば修正して」
					</p>
				</div>
			</div>
			<div class="flex items-start gap-3 p-3 rounded-lg bg-gray-50 dark:bg-gray-800">
				<span class="flex-shrink-0 w-8 h-8 flex items-center justify-center rounded-full bg-blue-500 text-white font-bold">3</span>
				<div>
					<p class="font-semibold">E2Eテスト（重要な機能のみ）</p>
					<p class="text-sm text-gray-600 dark:text-gray-400">
						Playwright MCP で「ログインフローをテストして」
					</p>
				</div>
			</div>
			<div class="flex items-start gap-3 p-3 rounded-lg bg-gray-50 dark:bg-gray-800">
				<span class="flex-shrink-0 w-8 h-8 flex items-center justify-center rounded-full bg-green-500 text-white font-bold">4</span>
				<div>
					<p class="font-semibold">デプロイ</p>
					<p class="text-sm text-gray-600 dark:text-gray-400">
						「ビルドしてデプロイして」で完了
					</p>
				</div>
			</div>
		</div>

		<!-- 最小限のセットアップ -->
		<h3 class="text-lg font-semibold mb-3 mt-6">最小限のテスト環境セットアップ</h3>

		<CodePreview
			title="Vitest インストール"
			description="Claude Code がテストを書くための準備"
			language="bash"
			code={`npm install -D vitest`}
		/>

		<CodePreview
			title="vite.config.ts に追加"
			description="最小限の設定"
			language="typescript"
			code={`export default defineConfig({
  plugins: [tailwindcss(), sveltekit()],
  test: {
    include: ['src/**/*.{test,spec}.ts']
  }
});`}
		/>

		<CodePreview
			title="package.json"
			description="テストスクリプト"
			language="json"
			code={`{
  "scripts": {
    "test": "vitest run",
    "test:watch": "vitest"
  }
}`}
		/>

		<!-- プロンプト集 -->
		<h3 class="text-lg font-semibold mb-3 mt-6">コピペで使えるプロンプト集</h3>

		<div class="space-y-3">
			<div class="p-3 rounded-lg bg-purple-50 dark:bg-purple-900/20 border border-purple-200 dark:border-purple-800">
				<p class="font-mono text-sm text-purple-800 dark:text-purple-200">
					「src/lib/server/ 配下のすべての関数にユニットテストを書いて。<br/>
					正常系・異常系・境界値を含めて。」
				</p>
			</div>
			<div class="p-3 rounded-lg bg-purple-50 dark:bg-purple-900/20 border border-purple-200 dark:border-purple-800">
				<p class="font-mono text-sm text-purple-800 dark:text-purple-200">
					「npm run test を実行して、失敗したテストをすべて修正して。」
				</p>
			</div>
			<div class="p-3 rounded-lg bg-purple-50 dark:bg-purple-900/20 border border-purple-200 dark:border-purple-800">
				<p class="font-mono text-sm text-purple-800 dark:text-purple-200">
					「npm run check && npm run build && npm run test を実行して、<br/>
					エラーがあればすべて修正してからデプロイして。」
				</p>
			</div>
			<div class="p-3 rounded-lg bg-orange-50 dark:bg-orange-900/20 border border-orange-200 dark:border-orange-800">
				<p class="font-mono text-sm text-orange-800 dark:text-orange-200">
					「Playwright MCP で http://localhost:5173 を開いて、<br/>
					主要な機能をテストして問題がないか確認して。」
				</p>
			</div>
		</div>

		<div class="mt-6 p-4 rounded-lg bg-amber-50 dark:bg-amber-900/20 border border-amber-200 dark:border-amber-800">
			<p class="font-semibold text-amber-800 dark:text-amber-200 mb-2">注意点</p>
			<ul class="text-sm text-amber-700 dark:text-amber-300 space-y-1">
				<li>・AIが生成したテストは<strong>必ず結果を確認</strong>する（意味のないテストになっている場合がある）</li>
				<li>・すべてをモックするテストは避ける（実際の動作を確認できない）</li>
				<li>・<strong>最終的にはプレビューデプロイで実際に触る</strong>のが一番確実</li>
			</ul>
		</div>
	</section>

	<!-- Git ワークフロー -->
	<section class="mb-12">
		<h2 id="git" class="text-xl font-bold mb-4">個人開発の Git ワークフロー</h2>

		<p class="text-gray-700 dark:text-gray-300 mb-4">
			個人開発では GitHub Flow をさらにシンプルにした運用がおすすめ。
		</p>

		<CodePreview
			title="シンプル Git フロー"
			description="個人開発に最適"
			language="bash"
			code={`# 1. 機能開発を始める
git checkout -b feature/add-profile

# 2. こまめにコミット（AIと一緒に開発中）
git add .
git commit -m "feat: プロフィール画面を追加"

# 3. プッシュ → Cloudflare がプレビューURLを生成
git push origin feature/add-profile

# 4. プレビューURLで動作確認 → OK なら main へ
git checkout main
git merge feature/add-profile
git push origin main  # 自動で本番デプロイ

# 5. ブランチ削除
git branch -d feature/add-profile`}
		/>

		<div class="mt-4 p-4 rounded-lg bg-green-50 dark:bg-green-900/20 border border-green-200 dark:border-green-800">
			<p class="font-semibold text-green-800 dark:text-green-200 mb-2">Cloudflare Pages の魅力</p>
			<ul class="text-sm text-green-700 dark:text-green-300 space-y-1">
				<li>・<strong>プレビューデプロイ</strong>：main以外のブランチは自動でプレビューURLが発行</li>
				<li>・<strong>本番デプロイ</strong>：mainにマージすると自動デプロイ</li>
				<li>・<strong>ロールバック</strong>：管理画面から1クリックで前のバージョンに戻せる</li>
			</ul>
		</div>
	</section>

	<!-- AIツール活用 -->
	<section class="mb-12">
		<h2 id="ai-tools" class="text-xl font-bold mb-4">AI ツールの活用（2025年必須）</h2>

		<div class="p-4 rounded-lg bg-gradient-to-r from-purple-50 to-blue-50 dark:from-purple-900/20 dark:to-blue-900/20 border border-purple-200 dark:border-purple-800 mb-4">
			<p class="text-lg text-purple-800 dark:text-purple-200 mb-2">
				<strong>Vibe Coding</strong>の時代
			</p>
			<p class="text-sm text-purple-700 dark:text-purple-300">
				Y Combinator によると、一部のスタートアップではコードの最大90%がAI生成。
				個人開発者こそ AI を味方につけて、生産性を劇的に上げましょう。
			</p>
		</div>

		<div class="grid md:grid-cols-2 gap-4">
			<div class="p-4 rounded-lg bg-blue-50 dark:bg-blue-900/20 border border-blue-200 dark:border-blue-800">
				<p class="font-semibold text-blue-800 dark:text-blue-200 mb-2">Claude Code</p>
				<p class="text-sm text-blue-700 dark:text-blue-300">
					ターミナルで動くAIアシスタント。プロジェクト全体を理解してコードを書いてくれる。
					個人開発との相性抜群。
				</p>
			</div>
			<div class="p-4 rounded-lg bg-green-50 dark:bg-green-900/20 border border-green-200 dark:border-green-800">
				<p class="font-semibold text-green-800 dark:text-green-200 mb-2">Cursor / Windsurf</p>
				<p class="text-sm text-green-700 dark:text-green-300">
					AIが組み込まれたコードエディタ。
					コード補完からリファクタリングまでAIがサポート。
				</p>
			</div>
		</div>

		<div class="mt-4 p-4 rounded-lg bg-amber-50 dark:bg-amber-900/20 border border-amber-200 dark:border-amber-800">
			<p class="font-semibold text-amber-800 dark:text-amber-200 mb-2">AI活用のコツ</p>
			<ul class="text-sm text-amber-700 dark:text-amber-300 space-y-1">
				<li>・要件を明確に伝える（曖昧な指示は曖昧な結果に）</li>
				<li>・生成されたコードは必ずレビューする</li>
				<li>・セキュリティに関わる部分は特に注意</li>
				<li>・AIに任せる作業と自分でやる作業を分ける</li>
			</ul>
		</div>
	</section>

	<!-- 料金 -->
	<section class="mb-12">
		<h2 id="pricing" class="text-xl font-bold mb-4">Cloudflare 無料枠（2025年2月〜）</h2>

		<div class="p-4 rounded-lg bg-orange-50 dark:bg-orange-900/20 border border-orange-200 dark:border-orange-800 mb-4">
			<p class="font-semibold text-orange-800 dark:text-orange-200 mb-2">D1 無料枠（Workers Free プラン）</p>
			<ul class="text-sm text-orange-700 dark:text-orange-300 space-y-1">
				<li>・<strong>読み取り</strong>：1日 5,000,000 回</li>
				<li>・<strong>書き込み</strong>：1日 100,000 回</li>
				<li>・<strong>ストレージ</strong>：5GB</li>
			</ul>
			<p class="text-xs text-orange-600 dark:text-orange-400 mt-2">
				※ 2025年2月10日から制限が適用。超過するとエラーが返ります（00:00 UTC にリセット）
			</p>
		</div>

		<div class="p-4 rounded-lg bg-blue-50 dark:bg-blue-900/20 border border-blue-200 dark:border-blue-800">
			<p class="font-semibold text-blue-800 dark:text-blue-200 mb-2">個人開発なら十分</p>
			<p class="text-sm text-blue-700 dark:text-blue-300">
				1日500万読み取りは、かなりのトラフィックをさばける量。
				個人プロジェクトなら無料枠で十分運用できます。
				有料プラン（$5/月〜）に上げればさらに余裕。
			</p>
		</div>
	</section>

	<!-- まとめ -->
	<section class="mb-10">
		<h2 id="summary" class="text-xl font-bold mb-4">まとめ</h2>

		<div class="space-y-4">
			<div class="p-4 rounded-lg bg-orange-50 dark:bg-orange-900/20 border border-orange-200 dark:border-orange-800">
				<p class="font-semibold text-orange-800 dark:text-orange-200">スピード重視</p>
				<p class="text-sm text-orange-700 dark:text-orange-300">
					完璧を求めない。β版でいいから出す。改善は後から。
				</p>
			</div>
			<div class="p-4 rounded-lg bg-blue-50 dark:bg-blue-900/20 border border-blue-200 dark:border-blue-800">
				<p class="font-semibold text-blue-800 dark:text-blue-200">AI を味方に</p>
				<p class="text-sm text-blue-700 dark:text-blue-300">
					Claude Code や Cursor を活用して、「考えるべきこと」に集中。
				</p>
			</div>
			<div class="p-4 rounded-lg bg-green-50 dark:bg-green-900/20 border border-green-200 dark:border-green-800">
				<p class="font-semibold text-green-800 dark:text-green-200">シンプルに保つ</p>
				<p class="text-sm text-green-700 dark:text-green-300">
					複雑な構成は不要。Cloudflare の自動デプロイに任せる。
				</p>
			</div>
			<div class="p-4 rounded-lg bg-purple-50 dark:bg-purple-900/20 border border-purple-200 dark:border-purple-800">
				<p class="font-semibold text-purple-800 dark:text-purple-200">無料でスタート</p>
				<p class="text-sm text-purple-700 dark:text-purple-300">
					D1の無料枠で十分。サーバー管理不要で世界中で高速。
				</p>
			</div>
		</div>

		<div class="mt-6 p-4 rounded-lg bg-gray-100 dark:bg-gray-800 text-sm text-gray-600 dark:text-gray-400">
			<p class="font-semibold mb-2">参考リンク</p>
			<ul class="space-y-1">
				<li>・<a href="https://developers.cloudflare.com/d1/" class="text-blue-600 dark:text-blue-400 hover:underline" target="_blank" rel="noopener">Cloudflare D1 公式ドキュメント</a></li>
				<li>・<a href="https://kit.svelte.dev/docs/adapter-cloudflare" class="text-blue-600 dark:text-blue-400 hover:underline" target="_blank" rel="noopener">SvelteKit Cloudflare アダプター</a></li>
				<li>・<a href="https://orm.drizzle.team/docs/get-started-sqlite#cloudflare-d1" class="text-blue-600 dark:text-blue-400 hover:underline" target="_blank" rel="noopener">Drizzle ORM D1 ガイド</a></li>
				<li>・<a href="https://tailwindcss.com/docs/installation/vite" class="text-blue-600 dark:text-blue-400 hover:underline" target="_blank" rel="noopener">Tailwind CSS v4 インストール</a></li>
				<li>・<a href="https://github.com/microsoft/playwright-mcp" class="text-blue-600 dark:text-blue-400 hover:underline" target="_blank" rel="noopener">Playwright MCP Server（Microsoft公式）</a></li>
				<li>・<a href="https://github.com/executeautomation/mcp-playwright" class="text-blue-600 dark:text-blue-400 hover:underline" target="_blank" rel="noopener">MCP Playwright（ExecuteAutomation版）</a></li>
				<li>・<a href="https://vitest.dev/" class="text-blue-600 dark:text-blue-400 hover:underline" target="_blank" rel="noopener">Vitest 公式サイト</a></li>
			</ul>
		</div>
	</section>

	<!-- ナビゲーション -->
	<div class="flex justify-between pt-6 border-t border-gray-200 dark:border-gray-700">
		<a href="/dev/best-practices" class="inline-flex items-center gap-2 px-4 py-2 rounded-lg border border-gray-300 dark:border-gray-600 hover:bg-gray-100 dark:hover:bg-gray-800 transition-colors">
			<svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
				<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 19l-7-7 7-7" />
			</svg>
			前へ：ベストプラクティス
		</a>
		<a href="/" class="inline-flex items-center gap-2 px-4 py-2 rounded-lg bg-primary-600 text-white hover:bg-primary-700 transition-colors">
			ホームに戻る
			<svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
				<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M3 12l2-2m0 0l7-7 7 7M5 10v10a1 1 0 001 1h3m10-11l2 2m-2-2v10a1 1 0 01-1 1h-3m-6 0a1 1 0 001-1v-4a1 1 0 011-1h2a1 1 0 011 1v4a1 1 0 001 1m-6 0h6" />
			</svg>
		</a>
	</div>
</article>
