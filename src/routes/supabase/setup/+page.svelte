<script>
	import CodePreview from '$lib/components/CodePreview.svelte';
</script>

<svelte:head>
	<title>Supabase セットアップ | さとまたラボ</title>
</svelte:head>

<article>
	<h1 class="text-3xl font-bold mb-2">Supabase セットアップ</h1>
	<p class="text-lg text-gray-600 dark:text-gray-400 mb-8">
		SvelteKitプロジェクトでSupabaseを使う準備
	</p>

	<!-- プロジェクト作成 -->
	<section class="mb-10">
		<h2 id="create-project" class="text-xl font-bold mb-4">1. Supabaseプロジェクトを作成</h2>

		<div class="space-y-4">
			<div class="p-4 rounded-lg bg-gray-50 dark:bg-gray-800 border-l-4 border-emerald-500">
				<p class="font-bold text-emerald-600 dark:text-emerald-400">Step 1: アカウント作成</p>
				<p class="text-sm text-gray-600 dark:text-gray-400 mt-1">
					<a href="https://supabase.com" target="_blank" class="text-emerald-600 hover:underline">supabase.com</a> にアクセスし、「Start your project」をクリック。GitHubアカウントでサインアップできます。
				</p>
			</div>

			<div class="p-4 rounded-lg bg-gray-50 dark:bg-gray-800 border-l-4 border-emerald-500">
				<p class="font-bold text-emerald-600 dark:text-emerald-400">Step 2: New Project</p>
				<p class="text-sm text-gray-600 dark:text-gray-400 mt-1">
					ダッシュボードで「New Project」をクリックし、以下を入力：
				</p>
				<ul class="text-sm text-gray-600 dark:text-gray-400 mt-2 space-y-1">
					<li>・<strong>Name</strong>：プロジェクト名（例：my-todo-app）</li>
					<li>・<strong>Database Password</strong>：データベースのパスワード（忘れずにメモ！）</li>
					<li>・<strong>Region</strong>：Northeast Asia (Tokyo) がおすすめ</li>
				</ul>
			</div>

			<div class="p-4 rounded-lg bg-gray-50 dark:bg-gray-800 border-l-4 border-emerald-500">
				<p class="font-bold text-emerald-600 dark:text-emerald-400">Step 3: APIキーを取得</p>
				<p class="text-sm text-gray-600 dark:text-gray-400 mt-1">
					プロジェクト作成後、Settings → API から以下をコピー：
				</p>
				<ul class="text-sm text-gray-600 dark:text-gray-400 mt-2 space-y-1">
					<li>・<strong>Project URL</strong>：https://xxxxx.supabase.co</li>
					<li>・<strong>anon public</strong>：公開APIキー（フロントエンドで使用）</li>
					<li>・<strong>service_role</strong>：秘密キー（サーバーサイドのみで使用）</li>
				</ul>
			</div>
		</div>
	</section>

	<!-- SvelteKitにインストール -->
	<section class="mb-10">
		<h2 id="install" class="text-xl font-bold mb-4">2. SvelteKitにインストール</h2>

		<CodePreview
			title="パッケージのインストール"
			description="Supabase JavaScript クライアント"
			language="bash"
			code={`# Supabaseクライアントをインストール
npm install @supabase/supabase-js

# SSR用のヘルパー（推奨）
npm install @supabase/ssr`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div style="color:#6a9955;"># 2つのパッケージをインストール</div></div>`}
		/>
	</section>

	<!-- 環境変数 -->
	<section class="mb-10">
		<h2 id="env" class="text-xl font-bold mb-4">3. 環境変数を設定</h2>

		<CodePreview
			title=".env ファイルを作成"
			description="プロジェクトルートに作成"
			language="bash"
			code={`# .env
PUBLIC_SUPABASE_URL=https://あなたのプロジェクト.supabase.co
PUBLIC_SUPABASE_ANON_KEY=あなたのanonキー

# サーバーサイドで使う場合（オプション）
SUPABASE_SERVICE_ROLE_KEY=あなたのservice_roleキー`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div style="color:#f14c4c;">⚠️ .gitignore に .env を追加！</div></div>`}
		/>

		<div class="mt-4 p-4 rounded-lg bg-red-50 dark:bg-red-900/20 border border-red-200 dark:border-red-800">
			<p class="font-semibold text-red-800 dark:text-red-200">重要：.gitignore を確認</p>
			<p class="text-sm text-red-700 dark:text-red-300 mt-1">
				<code>.env</code> ファイルは必ず <code>.gitignore</code> に追加してください。APIキーが公開されると悪用されます！
			</p>
		</div>
	</section>

	<!-- クライアント設定 -->
	<section class="mb-10">
		<h2 id="client" class="text-xl font-bold mb-4">4. Supabaseクライアントを作成</h2>

		<CodePreview
			title="src/lib/supabase.ts"
			description="Supabaseクライアントの初期化"
			language="typescript"
			code={`import { createClient } from '@supabase/supabase-js'
import { PUBLIC_SUPABASE_URL, PUBLIC_SUPABASE_ANON_KEY } from '$env/static/public'

// Supabaseクライアントを作成
export const supabase = createClient(
  PUBLIC_SUPABASE_URL,
  PUBLIC_SUPABASE_ANON_KEY
)

// 型定義（オプション）
export type Database = {
  public: {
    Tables: {
      todos: {
        Row: {
          id: number
          title: string
          completed: boolean
          created_at: string
        }
        Insert: {
          title: string
          completed?: boolean
        }
        Update: {
          title?: string
          completed?: boolean
        }
      }
    }
  }
}`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div style="color:#6a9955;">// これで supabase を使える</div><div>import &#123; supabase &#125; from '$lib/supabase'</div></div>`}
		/>
	</section>

	<!-- SSR対応 -->
	<section class="mb-10">
		<h2 id="ssr" class="text-xl font-bold mb-4">5. SSR対応（推奨）</h2>

		<div class="p-4 rounded-lg bg-amber-50 dark:bg-amber-900/20 border border-amber-200 dark:border-amber-800 mb-4">
			<p class="font-semibold text-amber-800 dark:text-amber-200">なぜSSR対応が必要？</p>
			<p class="text-sm text-amber-700 dark:text-amber-300 mt-1">
				SvelteKitはサーバーでもクライアントでもコードが実行されます。認証状態をサーバーとクライアントで同期するために、<code>@supabase/ssr</code> を使います。
			</p>
		</div>

		<CodePreview
			title="src/hooks.server.ts"
			description="サーバーサイドでSupabaseを初期化"
			language="typescript"
			code={`import { PUBLIC_SUPABASE_URL, PUBLIC_SUPABASE_ANON_KEY } from '$env/static/public'
import { createServerClient } from '@supabase/ssr'
import type { Handle } from '@sveltejs/kit'

export const handle: Handle = async ({ event, resolve }) => {
  // サーバー用Supabaseクライアントを作成
  event.locals.supabase = createServerClient(
    PUBLIC_SUPABASE_URL,
    PUBLIC_SUPABASE_ANON_KEY,
    {
      cookies: {
        getAll: () => event.cookies.getAll(),
        setAll: (cookiesToSet) => {
          cookiesToSet.forEach(({ name, value, options }) => {
            event.cookies.set(name, value, { ...options, path: '/' })
          })
        },
      },
    }
  )

  // 現在のセッションを取得
  event.locals.getSession = async () => {
    const { data: { session } } = await event.locals.supabase.auth.getSession()
    return session
  }

  return resolve(event)
}`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div style="color:#6a9955;">// サーバーサイドで認証状態を管理</div></div>`}
		/>

		<CodePreview
			title="src/app.d.ts"
			description="型定義を追加"
			language="typescript"
			code={`import type { SupabaseClient, Session } from '@supabase/supabase-js'

declare global {
  namespace App {
    interface Locals {
      supabase: SupabaseClient
      getSession: () => Promise<Session | null>
    }
  }
}

export {}`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div style="color:#6a9955;">// TypeScriptの型を定義</div></div>`}
		/>
	</section>

	<!-- 使ってみる -->
	<section class="mb-10">
		<h2 id="usage" class="text-xl font-bold mb-4">6. 使ってみる</h2>

		<CodePreview
			title="src/routes/+page.svelte"
			description="データを取得して表示"
			language="svelte"
			code={`<script lang="ts">
  import { supabase } from '$lib/supabase'
  import { onMount } from 'svelte'

  let todos = $state([])
  let loading = $state(true)

  onMount(async () => {
    const { data, error } = await supabase
      .from('todos')
      .select('*')
      .order('created_at', { ascending: false })

    if (data) todos = data
    loading = false
  })
</script>

{#if loading}
  <p>読み込み中...</p>
{:else}
  <ul>
    {#each todos as todo}
      <li>{todo.title}</li>
    {/each}
  </ul>
{/if}`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div style="color:#6a9955;">// データベースからデータを取得</div></div>`}
		/>
	</section>

	<!-- ナビゲーション -->
	<div class="flex justify-between pt-6 border-t border-gray-200 dark:border-gray-700">
		<a href="/supabase/intro" class="inline-flex items-center gap-2 px-4 py-2 rounded-lg border border-gray-300 dark:border-gray-600 hover:bg-gray-100 dark:hover:bg-gray-800 transition-colors">
			<svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
				<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 19l-7-7 7-7" />
			</svg>
			前へ：はじめに
		</a>
		<a href="/supabase/database" class="inline-flex items-center gap-2 px-4 py-2 rounded-lg bg-primary-600 text-white hover:bg-primary-700 transition-colors">
			次へ：データベース操作
			<svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
				<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 5l7 7-7 7" />
			</svg>
		</a>
	</div>
</article>
