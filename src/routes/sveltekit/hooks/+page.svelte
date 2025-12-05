<script>
	import CodePreview from '$lib/components/CodePreview.svelte';
</script>

<svelte:head>
	<title>SvelteKit Hooks | さとまたラボ</title>
</svelte:head>

<article>
	<h1 class="text-3xl font-bold mb-2">Hooks（フック）</h1>
	<p class="text-lg text-gray-600 dark:text-gray-400 mb-8">
		リクエストの処理をカスタマイズする
	</p>

	<!-- Hooksとは -->
	<section class="mb-10">
		<h2 id="what-is" class="text-xl font-bold mb-4">Hooksとは？</h2>

		<div class="p-6 rounded-xl bg-blue-50 dark:bg-blue-900/20 border border-blue-200 dark:border-blue-800 mb-6">
			<p class="text-blue-800 dark:text-blue-200 mb-4">
				<strong>日常での例え：</strong>建物の入口にいる警備員
			</p>
			<div class="grid grid-cols-1 md:grid-cols-2 gap-4 text-sm">
				<div class="p-3 bg-white dark:bg-gray-800 rounded-lg">
					<div class="font-semibold text-blue-700 dark:text-blue-300 mb-2">警備員の仕事</div>
					<p class="text-gray-600 dark:text-gray-400">
						・入館者の身分証チェック<br>
						・入館記録をつける<br>
						・不審者は入れない
					</p>
				</div>
				<div class="p-3 bg-white dark:bg-gray-800 rounded-lg">
					<div class="font-semibold text-blue-700 dark:text-blue-300 mb-2">Hooksの仕事</div>
					<p class="text-gray-600 dark:text-gray-400">
						・ユーザーの認証チェック<br>
						・リクエストのログを取る<br>
						・未認証ユーザーをリダイレクト
					</p>
				</div>
			</div>
		</div>

		<div class="p-4 rounded-lg bg-amber-50 dark:bg-amber-900/20 border border-amber-200 dark:border-amber-800 mb-6">
			<p class="font-semibold text-amber-800 dark:text-amber-200">なぜHooksが必要？</p>
			<div class="text-sm text-amber-700 dark:text-amber-300 mt-2">
				<p class="mb-2"><strong>Hooksがないと困ること：</strong></p>
				<ul class="list-disc list-inside space-y-1 mb-3">
					<li>ログイン確認を全ページに書く必要がある（同じコードを何十回も...）</li>
					<li>「誰がいつアクセスしたか」のログを取る場所がない</li>
					<li>エラーが起きても原因が分からない</li>
				</ul>
				<p><strong>Hooksがあれば：</strong>1箇所に書くだけで、全ページに適用される！</p>
			</div>
		</div>

		<div class="p-4 rounded-lg bg-green-50 dark:bg-green-900/20 border border-green-200 dark:border-green-800 mb-6">
			<p class="font-semibold text-green-800 dark:text-green-200">Hooksでできること</p>
			<div class="text-sm text-green-700 dark:text-green-300 mt-2">
				<ul class="list-disc list-inside space-y-2">
					<li>
						<strong>handle</strong>：すべてのリクエストを傍受・加工<br>
						<span class="text-green-600 dark:text-green-400">→ 例：ログインチェック、アクセスログ記録</span>
					</li>
					<li>
						<strong>handleFetch</strong>：サーバーでのfetch（データ取得）をカスタマイズ<br>
						<span class="text-green-600 dark:text-green-400">→ 例：外部APIへの認証ヘッダー自動追加</span>
					</li>
					<li>
						<strong>handleError</strong>：エラーを捕まえて処理<br>
						<span class="text-green-600 dark:text-green-400">→ 例：エラーをSlackに通知、ユーザーには優しいメッセージ</span>
					</li>
				</ul>
			</div>
		</div>

		<div class="p-4 rounded-lg bg-gray-100 dark:bg-gray-800 mb-6">
			<p class="font-semibold text-gray-800 dark:text-gray-200 mb-2">ファイルの場所</p>
			<div class="text-sm text-gray-700 dark:text-gray-300">
				<code class="bg-gray-200 dark:bg-gray-700 px-2 py-1 rounded">src/hooks.server.ts</code>
				<p class="mt-2">このファイルにhook関数を定義します</p>
			</div>
		</div>

		<div class="p-4 rounded-lg bg-purple-50 dark:bg-purple-900/20 border border-purple-200 dark:border-purple-800 mb-6">
			<p class="font-semibold text-purple-800 dark:text-purple-200 mb-2">用語解説</p>
			<div class="text-sm text-purple-700 dark:text-purple-300 space-y-2">
				<p><strong>リクエスト</strong>：ブラウザからサーバーへの「このページください」という要求</p>
				<p><strong>レスポンス</strong>：サーバーからブラウザへの「はい、どうぞ」という返答</p>
				<p><strong>Cookie（クッキー）</strong>：ブラウザに保存される小さなデータ。「ログイン中」などの情報を覚えておく</p>
				<p><strong>セッション</strong>：ユーザーがサイトを訪れている間の「会話」のようなもの。誰がログイン中かを識別</p>
				<p><strong>リダイレクト</strong>：別のページに自動で移動させること（例：未ログイン→ログインページへ）</p>
			</div>
		</div>
	</section>

	<!-- handle -->
	<section class="mb-10">
		<h2 id="handle" class="text-xl font-bold mb-4">handle フック</h2>

		<CodePreview
			title="基本的なhandle"
			description="すべてのリクエストを処理"
			language="typescript"
			code={`// src/hooks.server.ts
import type { Handle } from '@sveltejs/kit';

export const handle: Handle = async ({ event, resolve }) => {
  // リクエスト処理の前に実行
  console.log('リクエスト:', event.url.pathname);

  // デフォルトの処理を実行
  const response = await resolve(event);

  // レスポンスを返す前に実行
  console.log('レスポンス:', response.status);

  return response;
};`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div style="color:#6a9955;">// リクエスト → handle → ページ処理 → handle → レスポンス</div><div style="color:#6a9955;">// すべてのリクエストがここを通る</div></div>`}
		/>

		<CodePreview
			title="認証チェック"
			description="ログインしていないユーザーをリダイレクト"
			language="typescript"
			code={`// src/hooks.server.ts
import { redirect } from '@sveltejs/kit';
import type { Handle } from '@sveltejs/kit';

export const handle: Handle = async ({ event, resolve }) => {
  // Cookieからセッションを取得
  const session = event.cookies.get('session');

  // ユーザー情報をevent.localsに保存
  if (session) {
    const user = await getUserFromSession(session);
    event.locals.user = user;
  }

  // 保護されたページへのアクセスをチェック
  if (event.url.pathname.startsWith('/dashboard')) {
    if (!event.locals.user) {
      // 未ログインならログインページへ
      throw redirect(303, '/login');
    }
  }

  return resolve(event);
};`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div>/dashboard/* へのアクセス</div><div style="margin-left:10px;">├─ ログイン済み → ページ表示</div><div style="margin-left:10px;">└─ 未ログイン → /login へリダイレクト</div></div>`}
		/>

		<CodePreview
			title="event.localsとは"
			description="リクエスト間でデータを共有"
			language="typescript"
			code={`// src/hooks.server.ts
export const handle: Handle = async ({ event, resolve }) => {
  // localsにデータを保存（このリクエスト内で共有される）
  event.locals.user = { id: 1, name: '田中' };
  event.locals.startTime = Date.now();

  return resolve(event);
};

// src/routes/+page.server.ts
export function load({ locals }) {
  // handleで設定したlocalsを使える！
  console.log(locals.user);  // { id: 1, name: '田中' }

  return {
    user: locals.user
  };
}

// src/app.d.ts で型定義
declare global {
  namespace App {
    interface Locals {
      user: { id: number; name: string } | null;
      startTime: number;
    }
  }
}`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div style="color:#4ec9b0;">event.locals</div><div style="color:#6a9955;">// hooks → load → actions で共有</div><div style="color:#6a9955;">// リクエストごとにリセット</div></div>`}
		/>
	</section>

	<!-- sequence -->
	<section class="mb-10">
		<h2 id="sequence" class="text-xl font-bold mb-4">複数のhookを組み合わせる</h2>

		<CodePreview
			title="sequence関数"
			description="hookを順番に実行"
			language="typescript"
			code={`// src/hooks.server.ts
import { sequence } from '@sveltejs/kit/hooks';
import type { Handle } from '@sveltejs/kit';

// 認証hook
const authHandle: Handle = async ({ event, resolve }) => {
  const session = event.cookies.get('session');
  event.locals.user = session ? await getUser(session) : null;
  return resolve(event);
};

// ロギングhook
const loggingHandle: Handle = async ({ event, resolve }) => {
  const start = Date.now();
  const response = await resolve(event);
  const duration = Date.now() - start;

  console.log(\`\${event.request.method} \${event.url.pathname} - \${duration}ms\`);
  return response;
};

// 順番に実行
export const handle = sequence(authHandle, loggingHandle);`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div><span style="color:#dcdcaa;">sequence</span>(hook1, hook2, hook3)</div><div style="color:#6a9955;">// 順番に実行される</div><div style="color:#6a9955;">// 各hookは単一責任で書ける</div></div>`}
		/>
	</section>

	<!-- handleFetch -->
	<section class="mb-10">
		<h2 id="handleFetch" class="text-xl font-bold mb-4">handleFetch フック</h2>

		<div class="p-4 rounded-lg bg-blue-50 dark:bg-blue-900/20 border border-blue-200 dark:border-blue-800 mb-6">
			<p class="font-semibold text-blue-800 dark:text-blue-200 mb-2">handleFetchとは？</p>
			<p class="text-sm text-blue-700 dark:text-blue-300">
				load関数などでfetch()を使うとき、そのリクエストをカスタマイズできます。<br>
				外部APIへの認証ヘッダー追加などに使います。
			</p>
		</div>

		<CodePreview
			title="fetchにヘッダーを追加"
			description="外部APIへの認証"
			language="typescript"
			code={`// src/hooks.server.ts
import type { HandleFetch } from '@sveltejs/kit';

export const handleFetch: HandleFetch = async ({ request, fetch, event }) => {
  // 特定のAPIへのリクエストにヘッダーを追加
  if (request.url.startsWith('https://api.example.com')) {
    request = new Request(request, {
      headers: {
        ...Object.fromEntries(request.headers),
        'Authorization': 'Bearer ' + event.locals.apiToken
      }
    });
  }

  return fetch(request);
};`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div style="color:#6a9955;">// load関数でfetch()するとき</div><div style="color:#6a9955;">// 自動でAuthorizationヘッダーが付く</div></div>`}
		/>
	</section>

	<!-- handleError -->
	<section class="mb-10">
		<h2 id="handleError" class="text-xl font-bold mb-4">handleError フック</h2>

		<CodePreview
			title="エラーのログと変換"
			description="予期しないエラーを処理"
			language="typescript"
			code={`// src/hooks.server.ts
import type { HandleServerError } from '@sveltejs/kit';

export const handleError: HandleServerError = async ({ error, event, status, message }) => {
  // エラーをログに記録
  console.error('サーバーエラー:', error);

  // エラートラッキングサービスに送信（Sentryなど）
  // await Sentry.captureException(error);

  // ユーザーに表示するエラー情報を返す
  // （詳細なエラー情報は見せない）
  return {
    message: 'サーバーでエラーが発生しました',
    code: 'INTERNAL_ERROR'
  };
};`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div style="color:#6a9955;">// エラー発生時</div><div style="color:#6a9955;">// 1. ログに記録</div><div style="color:#6a9955;">// 2. 安全なメッセージをユーザーに返す</div></div>`}
		/>
	</section>

	<!-- 実践例 -->
	<section class="mb-10">
		<h2 id="practical" class="text-xl font-bold mb-4">実践的な例</h2>

		<CodePreview
			title="完全な認証フロー"
			description="セッション管理の全体像"
			language="typescript"
			code={`// src/hooks.server.ts
import { redirect } from '@sveltejs/kit';
import type { Handle } from '@sveltejs/kit';
import { db } from '$lib/server/db';

export const handle: Handle = async ({ event, resolve }) => {
  // 1. セッションCookieを取得
  const sessionId = event.cookies.get('session_id');

  if (sessionId) {
    // 2. DBからセッションを検証
    const session = await db.session.findUnique({
      where: { id: sessionId },
      include: { user: true }
    });

    if (session && session.expiresAt > new Date()) {
      // 3. 有効なセッション → ユーザー情報をセット
      event.locals.user = session.user;
    } else {
      // 4. 無効なセッション → Cookie削除
      event.cookies.delete('session_id', { path: '/' });
    }
  }

  // 5. 保護ルートのチェック
  const protectedRoutes = ['/dashboard', '/settings', '/profile'];
  const isProtected = protectedRoutes.some(route =>
    event.url.pathname.startsWith(route)
  );

  if (isProtected && !event.locals.user) {
    throw redirect(303, '/login?redirect=' + event.url.pathname);
  }

  return resolve(event);
};`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div style="color:#6a9955;">// 認証フローの全体</div><div>1. Cookie取得</div><div>2. セッション検証</div><div>3. ユーザー情報セット</div><div>4. 保護ルートチェック</div></div>`}
		/>
	</section>

	<!-- ナビゲーション -->
	<div class="flex justify-between pt-6 border-t border-gray-200 dark:border-gray-700">
		<a href="/sveltekit/forms" class="inline-flex items-center gap-2 px-4 py-2 rounded-lg border border-gray-300 dark:border-gray-600 hover:bg-gray-100 dark:hover:bg-gray-800 transition-colors">
			<svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
				<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 19l-7-7 7-7" />
			</svg>
			前へ：フォームアクション
		</a>
		<a href="/sveltekit/state" class="inline-flex items-center gap-2 px-4 py-2 rounded-lg bg-primary-600 text-white hover:bg-primary-700 transition-colors">
			次へ：状態管理
			<svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
				<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 5l7 7-7 7" />
			</svg>
		</a>
	</div>
</article>
