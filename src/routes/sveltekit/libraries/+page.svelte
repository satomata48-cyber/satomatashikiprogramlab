<script>
	import CodePreview from '$lib/components/CodePreview.svelte';
</script>

<svelte:head>
	<title>SvelteKit ライブラリ | さとまたラボ</title>
</svelte:head>

<article>
	<h1 class="text-3xl font-bold mb-2">おすすめライブラリ</h1>
	<p class="text-lg text-gray-600 dark:text-gray-400 mb-8">
		SvelteKitでよく使われる便利なライブラリ
	</p>

	<!-- ライブラリとは -->
	<section class="mb-10">
		<h2 id="what-is" class="text-xl font-bold mb-4">ライブラリとは？</h2>

		<div class="p-6 rounded-xl bg-blue-50 dark:bg-blue-900/20 border border-blue-200 dark:border-blue-800 mb-6">
			<p class="text-blue-800 dark:text-blue-200 mb-4">
				<strong>日常での例え：</strong>料理の「素」
			</p>
			<div class="grid grid-cols-1 md:grid-cols-2 gap-4 text-sm">
				<div class="p-3 bg-white dark:bg-gray-800 rounded-lg">
					<div class="font-semibold text-blue-700 dark:text-blue-300 mb-2">全部自分で作る</div>
					<p class="text-gray-600 dark:text-gray-400">
						カレーを最初から作る<br>
						→ スパイス調合から...大変
					</p>
				</div>
				<div class="p-3 bg-white dark:bg-gray-800 rounded-lg">
					<div class="font-semibold text-blue-700 dark:text-blue-300 mb-2">ライブラリを使う</div>
					<p class="text-gray-600 dark:text-gray-400">
						カレールーを使う<br>
						→ 誰でも美味しくできる
					</p>
				</div>
			</div>
		</div>

		<div class="p-4 rounded-lg bg-amber-50 dark:bg-amber-900/20 border border-amber-200 dark:border-amber-800 mb-6">
			<p class="font-semibold text-amber-800 dark:text-amber-200">なぜライブラリを使う？</p>
			<div class="text-sm text-amber-700 dark:text-amber-300 mt-2">
				<ul class="list-disc list-inside space-y-1">
					<li>車輪の再発明を避ける（すでに誰かが作ったものを活用）</li>
					<li>バグが少ない（多くの人がテスト済み）</li>
					<li>開発時間を短縮できる</li>
					<li>セキュリティが考慮されている（特に認証系）</li>
				</ul>
			</div>
		</div>
	</section>

	<!-- フォーム系 -->
	<section class="mb-10">
		<h2 id="forms" class="text-xl font-bold mb-4">フォーム処理</h2>

		<div class="p-4 rounded-lg border border-gray-200 dark:border-gray-700 mb-6">
			<div class="flex items-center gap-3 mb-3">
				<span class="text-2xl">📝</span>
				<div>
					<h3 class="font-bold text-lg">Superforms</h3>
					<p class="text-sm text-gray-500">フォーム処理の決定版</p>
				</div>
			</div>
			<p class="text-sm text-gray-600 dark:text-gray-400 mb-4">
				バリデーション、エラー処理、ローディング状態など、フォームに必要な機能がすべて揃っています。
			</p>
			<div class="flex flex-wrap gap-2 mb-4">
				<span class="px-2 py-1 bg-green-100 dark:bg-green-900 text-green-700 dark:text-green-300 rounded text-xs">バリデーション</span>
				<span class="px-2 py-1 bg-blue-100 dark:bg-blue-900 text-blue-700 dark:text-blue-300 rounded text-xs">Zod対応</span>
				<span class="px-2 py-1 bg-purple-100 dark:bg-purple-900 text-purple-700 dark:text-purple-300 rounded text-xs">TypeScript</span>
			</div>
		</div>

		<CodePreview
			title="Superforms の使い方"
			description="Zodでバリデーション"
			language="typescript"
			code={`// インストール
npm install sveltekit-superforms zod

// src/routes/contact/+page.server.ts
import { z } from 'zod';
import { superValidate, fail } from 'sveltekit-superforms';
import { zod } from 'sveltekit-superforms/adapters';

// バリデーションスキーマ
const schema = z.object({
  name: z.string().min(1, '名前は必須です'),
  email: z.string().email('正しいメールアドレスを入力してください'),
  message: z.string().min(10, '10文字以上入力してください')
});

export const load = async () => {
  const form = await superValidate(zod(schema));
  return { form };
};

export const actions = {
  default: async ({ request }) => {
    const form = await superValidate(request, zod(schema));

    if (!form.valid) {
      return fail(400, { form });
    }

    // 送信処理...
    return { form };
  }
};`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div style="color:#6a9955;">// Zodで型安全なバリデーション</div><div style="color:#6a9955;">// エラーメッセージも日本語で設定可能</div></div>`}
		/>

		<CodePreview
			title="Superforms のフォーム側"
			description="自動エラー表示"
			language="svelte"
			code={`<!-- src/routes/contact/+page.svelte -->
<script>
  import { superForm } from 'sveltekit-superforms';

  let { data } = $props();

  const { form, errors, enhance, submitting } = superForm(data.form);
</script>

<form method="POST" use:enhance>
  <label>
    名前
    <input name="name" bind:value={$form.name} />
    {#if $errors.name}
      <span class="error">{$errors.name}</span>
    {/if}
  </label>

  <label>
    メール
    <input name="email" type="email" bind:value={$form.email} />
    {#if $errors.email}
      <span class="error">{$errors.email}</span>
    {/if}
  </label>

  <label>
    メッセージ
    <textarea name="message" bind:value={$form.message}></textarea>
    {#if $errors.message}
      <span class="error">{$errors.message}</span>
    {/if}
  </label>

  <button disabled={$submitting}>
    {$submitting ? '送信中...' : '送信'}
  </button>
</form>`}
			previewHtml={`<form style="display:flex;flex-direction:column;gap:12px;max-width:300px;"><label style="font-size:14px;">名前<input style="width:100%;padding:8px;border:1px solid #d1d5db;border-radius:4px;margin-top:4px;"></label><label style="font-size:14px;">メール<input style="width:100%;padding:8px;border:1px solid #ef4444;border-radius:4px;margin-top:4px;"><span style="color:#ef4444;font-size:12px;">正しいメールアドレスを入力してください</span></label><button style="padding:8px 16px;background:#ff3e00;color:white;border:none;border-radius:4px;">送信</button></form>`}
		/>
	</section>

	<!-- 認証系 -->
	<section class="mb-10">
		<h2 id="auth" class="text-xl font-bold mb-4">認証（ログイン）</h2>

		<div class="p-4 rounded-lg border border-gray-200 dark:border-gray-700 mb-6">
			<div class="flex items-center gap-3 mb-3">
				<span class="text-2xl">🔐</span>
				<div>
					<h3 class="font-bold text-lg">Lucia</h3>
					<p class="text-sm text-gray-500">シンプルで柔軟な認証ライブラリ</p>
				</div>
			</div>
			<p class="text-sm text-gray-600 dark:text-gray-400 mb-4">
				セッション管理、OAuth（Google/GitHubログイン）、パスワード認証など。軽量で自由度が高い。
			</p>
			<div class="flex flex-wrap gap-2 mb-4">
				<span class="px-2 py-1 bg-green-100 dark:bg-green-900 text-green-700 dark:text-green-300 rounded text-xs">セッション管理</span>
				<span class="px-2 py-1 bg-blue-100 dark:bg-blue-900 text-blue-700 dark:text-blue-300 rounded text-xs">OAuth対応</span>
				<span class="px-2 py-1 bg-orange-100 dark:bg-orange-900 text-orange-700 dark:text-orange-300 rounded text-xs">軽量</span>
			</div>
		</div>

		<div class="p-4 rounded-lg border border-gray-200 dark:border-gray-700 mb-6">
			<div class="flex items-center gap-3 mb-3">
				<span class="text-2xl">🛡️</span>
				<div>
					<h3 class="font-bold text-lg">Auth.js (NextAuth)</h3>
					<p class="text-sm text-gray-500">多機能な認証ソリューション</p>
				</div>
			</div>
			<p class="text-sm text-gray-600 dark:text-gray-400 mb-4">
				多くのOAuthプロバイダーに対応。Next.jsで有名だがSvelteKitでも使用可能。
			</p>
			<div class="flex flex-wrap gap-2">
				<span class="px-2 py-1 bg-green-100 dark:bg-green-900 text-green-700 dark:text-green-300 rounded text-xs">50+プロバイダー</span>
				<span class="px-2 py-1 bg-purple-100 dark:bg-purple-900 text-purple-700 dark:text-purple-300 rounded text-xs">JWT/Session</span>
			</div>
		</div>

		<CodePreview
			title="Lucia の基本"
			description="セッション管理"
			language="typescript"
			code={`// インストール
npm install lucia

// src/lib/server/auth.ts
import { Lucia } from 'lucia';
import { dev } from '$app/environment';

const adapter = /* データベースアダプター */;

export const lucia = new Lucia(adapter, {
  sessionCookie: {
    attributes: {
      secure: !dev
    }
  }
});

// src/hooks.server.ts
import { lucia } from '$lib/server/auth';

export const handle = async ({ event, resolve }) => {
  const sessionId = event.cookies.get(lucia.sessionCookieName);

  if (!sessionId) {
    event.locals.user = null;
    event.locals.session = null;
    return resolve(event);
  }

  const { session, user } = await lucia.validateSession(sessionId);

  if (session?.fresh) {
    const cookie = lucia.createSessionCookie(session.id);
    event.cookies.set(cookie.name, cookie.value, cookie.attributes);
  }

  event.locals.user = user;
  event.locals.session = session;

  return resolve(event);
};`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div style="color:#6a9955;">// Luciaはセキュリティを考慮した</div><div style="color:#6a9955;">// セッション管理を提供</div></div>`}
		/>
	</section>

	<!-- データベース系 -->
	<section class="mb-10">
		<h2 id="database" class="text-xl font-bold mb-4">データベース（ORM）</h2>

		<div class="p-4 rounded-lg bg-blue-50 dark:bg-blue-900/20 border border-blue-200 dark:border-blue-800 mb-6">
			<p class="font-semibold text-blue-800 dark:text-blue-200 mb-2">ORMとは？</p>
			<p class="text-sm text-blue-700 dark:text-blue-300">
				<strong>Object-Relational Mapping</strong>：データベースをJavaScriptのオブジェクトのように操作できるツール。<br>
				SQLを書かなくても、<code>db.user.findMany()</code> のような直感的なコードでデータを取得できます。
			</p>
		</div>

		<div class="grid grid-cols-1 md:grid-cols-2 gap-4 mb-6">
			<div class="p-4 rounded-lg border border-gray-200 dark:border-gray-700">
				<div class="flex items-center gap-3 mb-3">
					<span class="text-2xl">💧</span>
					<div>
						<h3 class="font-bold">Drizzle ORM</h3>
						<p class="text-xs text-gray-500">軽量・高速</p>
					</div>
				</div>
				<p class="text-sm text-gray-600 dark:text-gray-400 mb-3">
					TypeScript完全対応。SQLに近い書き方で学習コストが低い。
				</p>
				<div class="flex flex-wrap gap-1">
					<span class="px-2 py-0.5 bg-green-100 dark:bg-green-900 text-green-700 dark:text-green-300 rounded text-xs">軽量</span>
					<span class="px-2 py-0.5 bg-blue-100 dark:bg-blue-900 text-blue-700 dark:text-blue-300 rounded text-xs">高速</span>
				</div>
			</div>

			<div class="p-4 rounded-lg border border-gray-200 dark:border-gray-700">
				<div class="flex items-center gap-3 mb-3">
					<span class="text-2xl">🔷</span>
					<div>
						<h3 class="font-bold">Prisma</h3>
						<p class="text-xs text-gray-500">人気No.1</p>
					</div>
				</div>
				<p class="text-sm text-gray-600 dark:text-gray-400 mb-3">
					スキーマファーストで直感的。豊富なドキュメントとコミュニティ。
				</p>
				<div class="flex flex-wrap gap-1">
					<span class="px-2 py-0.5 bg-purple-100 dark:bg-purple-900 text-purple-700 dark:text-purple-300 rounded text-xs">人気</span>
					<span class="px-2 py-0.5 bg-orange-100 dark:bg-orange-900 text-orange-700 dark:text-orange-300 rounded text-xs">ドキュメント充実</span>
				</div>
			</div>
		</div>

		<CodePreview
			title="Drizzle ORM"
			description="型安全なデータベース操作"
			language="typescript"
			code={`// インストール
npm install drizzle-orm better-sqlite3
npm install -D drizzle-kit @types/better-sqlite3

// src/lib/server/db/schema.ts
import { sqliteTable, text, integer } from 'drizzle-orm/sqlite-core';

export const users = sqliteTable('users', {
  id: integer('id').primaryKey({ autoIncrement: true }),
  name: text('name').notNull(),
  email: text('email').notNull().unique(),
  createdAt: integer('created_at', { mode: 'timestamp' })
    .notNull()
    .default(sql\`CURRENT_TIMESTAMP\`)
});

// src/lib/server/db/index.ts
import { drizzle } from 'drizzle-orm/better-sqlite3';
import Database from 'better-sqlite3';

const sqlite = new Database('sqlite.db');
export const db = drizzle(sqlite);

// 使い方
import { db } from '$lib/server/db';
import { users } from '$lib/server/db/schema';
import { eq } from 'drizzle-orm';

// 全ユーザー取得
const allUsers = db.select().from(users).all();

// 条件で検索
const user = db.select().from(users).where(eq(users.id, 1)).get();

// 新規作成
db.insert(users).values({ name: '田中', email: 'tanaka@example.com' }).run();`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div style="color:#dcdcaa;">db.select()</div><div style="color:#dcdcaa;">db.insert()</div><div style="color:#dcdcaa;">db.update()</div><div style="color:#dcdcaa;">db.delete()</div></div>`}
		/>

		<CodePreview
			title="Prisma"
			description="スキーマファーストORM"
			language="typescript"
			code={`// インストール
npm install prisma @prisma/client
npx prisma init

// prisma/schema.prisma
generator client {
  provider = "prisma-client-js"
}

datasource db {
  provider = "sqlite"
  url      = "file:./dev.db"
}

model User {
  id        Int      @id @default(autoincrement())
  name      String
  email     String   @unique
  posts     Post[]
  createdAt DateTime @default(now())
}

model Post {
  id        Int      @id @default(autoincrement())
  title     String
  content   String?
  author    User     @relation(fields: [authorId], references: [id])
  authorId  Int
}

// マイグレーション実行
npx prisma migrate dev

// 使い方
import { PrismaClient } from '@prisma/client';
const prisma = new PrismaClient();

// 全ユーザー取得
const users = await prisma.user.findMany();

// 関連データも一緒に取得
const usersWithPosts = await prisma.user.findMany({
  include: { posts: true }
});

// 新規作成
await prisma.user.create({
  data: { name: '田中', email: 'tanaka@example.com' }
});`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div style="color:#dcdcaa;">prisma.user.findMany()</div><div style="color:#dcdcaa;">prisma.user.create()</div><div style="color:#dcdcaa;">prisma.user.update()</div><div style="color:#dcdcaa;">prisma.user.delete()</div></div>`}
		/>
	</section>

	<!-- UI系 -->
	<section class="mb-10">
		<h2 id="ui" class="text-xl font-bold mb-4">UIコンポーネント</h2>

		<div class="grid grid-cols-1 md:grid-cols-2 gap-4 mb-6">
			<div class="p-4 rounded-lg border border-gray-200 dark:border-gray-700">
				<div class="flex items-center gap-3 mb-3">
					<span class="text-2xl">🎨</span>
					<div>
						<h3 class="font-bold">shadcn-svelte</h3>
						<p class="text-xs text-gray-500">美しいUIコンポーネント</p>
					</div>
				</div>
				<p class="text-sm text-gray-600 dark:text-gray-400 mb-3">
					Radix UIベース。コピペでカスタマイズ可能なコンポーネント集。
				</p>
				<code class="text-xs bg-gray-100 dark:bg-gray-800 px-2 py-1 rounded">npx shadcn-svelte@latest init</code>
			</div>

			<div class="p-4 rounded-lg border border-gray-200 dark:border-gray-700">
				<div class="flex items-center gap-3 mb-3">
					<span class="text-2xl">🧩</span>
					<div>
						<h3 class="font-bold">Bits UI</h3>
						<p class="text-xs text-gray-500">ヘッドレスUIコンポーネント</p>
					</div>
				</div>
				<p class="text-sm text-gray-600 dark:text-gray-400 mb-3">
					スタイルなしのアクセシブルなコンポーネント。自由にデザイン可能。
				</p>
				<code class="text-xs bg-gray-100 dark:bg-gray-800 px-2 py-1 rounded">npm install bits-ui</code>
			</div>

			<div class="p-4 rounded-lg border border-gray-200 dark:border-gray-700">
				<div class="flex items-center gap-3 mb-3">
					<span class="text-2xl">🍞</span>
					<div>
						<h3 class="font-bold">svelte-sonner</h3>
						<p class="text-xs text-gray-500">トースト通知</p>
					</div>
				</div>
				<p class="text-sm text-gray-600 dark:text-gray-400 mb-3">
					美しいトースト通知。成功・エラー・警告などの表示に。
				</p>
				<code class="text-xs bg-gray-100 dark:bg-gray-800 px-2 py-1 rounded">npm install svelte-sonner</code>
			</div>

			<div class="p-4 rounded-lg border border-gray-200 dark:border-gray-700">
				<div class="flex items-center gap-3 mb-3">
					<span class="text-2xl">📊</span>
					<div>
						<h3 class="font-bold">Layerchart</h3>
						<p class="text-xs text-gray-500">グラフ・チャート</p>
					</div>
				</div>
				<p class="text-sm text-gray-600 dark:text-gray-400 mb-3">
					Svelte向けのチャートライブラリ。棒グラフ、折れ線など。
				</p>
				<code class="text-xs bg-gray-100 dark:bg-gray-800 px-2 py-1 rounded">npm install layerchart</code>
			</div>
		</div>

		<CodePreview
			title="svelte-sonner の使い方"
			description="トースト通知"
			language="svelte"
			code={`// インストール
npm install svelte-sonner

// src/routes/+layout.svelte
<script>
  import { Toaster } from 'svelte-sonner';
  let { children } = $props();
</script>

<Toaster richColors position="top-right" />
{@render children()}

// 使う側
<script>
  import { toast } from 'svelte-sonner';

  function handleSubmit() {
    // 処理...

    // 成功
    toast.success('保存しました！');

    // エラー
    toast.error('エラーが発生しました');

    // 情報
    toast.info('新しいメッセージがあります');

    // ローディング付き
    toast.promise(saveData(), {
      loading: '保存中...',
      success: '保存完了！',
      error: '保存に失敗しました'
    });
  }
</script>

<button onclick={handleSubmit}>保存</button>`}
			previewHtml={`<div style="display:flex;flex-direction:column;gap:8px;"><div style="padding:12px 16px;background:#dcfce7;border:1px solid #86efac;border-radius:8px;display:flex;align-items:center;gap:8px;"><span style="color:#16a34a;">✓</span><span style="color:#166534;">保存しました！</span></div><div style="padding:12px 16px;background:#fee2e2;border:1px solid #fca5a5;border-radius:8px;display:flex;align-items:center;gap:8px;"><span style="color:#dc2626;">✕</span><span style="color:#991b1b;">エラーが発生しました</span></div></div>`}
		/>
	</section>

	<!-- ユーティリティ -->
	<section class="mb-10">
		<h2 id="utils" class="text-xl font-bold mb-4">ユーティリティ</h2>

		<div class="grid grid-cols-1 md:grid-cols-3 gap-4 mb-6">
			<div class="p-4 rounded-lg border border-gray-200 dark:border-gray-700">
				<h3 class="font-bold mb-2">Zod</h3>
				<p class="text-sm text-gray-600 dark:text-gray-400 mb-2">
					型安全なバリデーション
				</p>
				<code class="text-xs bg-gray-100 dark:bg-gray-800 px-2 py-1 rounded">npm install zod</code>
			</div>

			<div class="p-4 rounded-lg border border-gray-200 dark:border-gray-700">
				<h3 class="font-bold mb-2">date-fns</h3>
				<p class="text-sm text-gray-600 dark:text-gray-400 mb-2">
					日付操作ライブラリ
				</p>
				<code class="text-xs bg-gray-100 dark:bg-gray-800 px-2 py-1 rounded">npm install date-fns</code>
			</div>

			<div class="p-4 rounded-lg border border-gray-200 dark:border-gray-700">
				<h3 class="font-bold mb-2">clsx</h3>
				<p class="text-sm text-gray-600 dark:text-gray-400 mb-2">
					条件付きクラス名
				</p>
				<code class="text-xs bg-gray-100 dark:bg-gray-800 px-2 py-1 rounded">npm install clsx</code>
			</div>
		</div>

		<CodePreview
			title="clsx の使い方"
			description="条件でクラスを切り替え"
			language="svelte"
			code={`<script>
  import clsx from 'clsx';

  let { variant = 'primary', disabled = false } = $props();

  // 条件に応じてクラスを組み合わせ
  const buttonClass = clsx(
    'px-4 py-2 rounded-lg font-medium',  // 常に適用
    {
      'bg-blue-600 text-white': variant === 'primary',
      'bg-gray-200 text-gray-800': variant === 'secondary',
      'bg-red-600 text-white': variant === 'danger',
      'opacity-50 cursor-not-allowed': disabled
    }
  );
</script>

<button class={buttonClass} {disabled}>
  ボタン
</button>`}
			previewHtml={`<div style="display:flex;gap:8px;"><button style="padding:8px 16px;background:#2563eb;color:white;border:none;border-radius:8px;">Primary</button><button style="padding:8px 16px;background:#e5e7eb;color:#1f2937;border:none;border-radius:8px;">Secondary</button><button style="padding:8px 16px;background:#dc2626;color:white;border:none;border-radius:8px;">Danger</button></div>`}
		/>
	</section>

	<!-- まとめ -->
	<section class="mb-10">
		<h2 id="summary" class="text-xl font-bold mb-4">おすすめの組み合わせ</h2>

		<div class="p-4 rounded-lg bg-gradient-to-r from-orange-50 to-red-50 dark:from-orange-900/20 dark:to-red-900/20 border border-orange-200 dark:border-orange-800">
			<p class="font-semibold text-orange-800 dark:text-orange-200 mb-3">初心者におすすめのスタック</p>
			<div class="text-sm text-orange-700 dark:text-orange-300 space-y-2">
				<p><strong>フォーム：</strong>Superforms + Zod</p>
				<p><strong>データベース：</strong>Drizzle（学習コスト低い）or Prisma（ドキュメント充実）</p>
				<p><strong>認証：</strong>Lucia（軽量）</p>
				<p><strong>UI：</strong>shadcn-svelte + svelte-sonner</p>
				<p><strong>スタイリング：</strong>Tailwind CSS + clsx</p>
			</div>
		</div>
	</section>

	<!-- ナビゲーション -->
	<div class="flex justify-between pt-6 border-t border-gray-200 dark:border-gray-700">
		<a href="/sveltekit/api" class="inline-flex items-center gap-2 px-4 py-2 rounded-lg border border-gray-300 dark:border-gray-600 hover:bg-gray-100 dark:hover:bg-gray-800 transition-colors">
			<svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
				<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 19l-7-7 7-7" />
			</svg>
			前へ：APIエンドポイント
		</a>
		<a href="/sveltekit/setup" class="inline-flex items-center gap-2 px-4 py-2 rounded-lg bg-primary-600 text-white hover:bg-primary-700 transition-colors">
			次へ：プロジェクト作成
			<svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
				<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 5l7 7-7 7" />
			</svg>
		</a>
	</div>
</article>
