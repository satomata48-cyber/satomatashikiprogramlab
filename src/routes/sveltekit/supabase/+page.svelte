<script>
	import CodePreview from '$lib/components/CodePreview.svelte';
</script>

<svelte:head>
	<title>SvelteKit × Supabase連携 | さとまたラボ</title>
</svelte:head>

<article>
	<h1 class="text-3xl font-bold mb-2">Supabase連携</h1>
	<p class="text-lg text-gray-600 dark:text-gray-400 mb-8">
		SvelteKitでSupabaseを使ったフルスタック開発
	</p>

	<!-- Supabaseとは -->
	<section class="mb-10">
		<h2 id="what-is-supabase" class="text-xl font-bold mb-4">Supabaseとは何か？</h2>

		<div class="p-6 rounded-xl bg-emerald-50 dark:bg-emerald-900/20 border border-emerald-200 dark:border-emerald-800 mb-6">
			<p class="text-emerald-800 dark:text-emerald-200 mb-4">
				<strong>Supabase = データベース + 認証 + ストレージ が一体になったサービス</strong>
			</p>
			<div class="grid md:grid-cols-3 gap-4 text-sm text-emerald-700 dark:text-emerald-300">
				<div class="p-3 bg-white/50 dark:bg-black/20 rounded">
					<strong>PostgreSQL</strong><br>
					データを保存するデータベース。Todoのタイトルや完了状態を保存
				</div>
				<div class="p-3 bg-white/50 dark:bg-black/20 rounded">
					<strong>Authentication</strong><br>
					ユーザー登録・ログイン機能。メール認証やGoogle認証
				</div>
				<div class="p-3 bg-white/50 dark:bg-black/20 rounded">
					<strong>Storage</strong><br>
					画像やファイルを保存。プロフィール画像のアップロードなど
				</div>
			</div>
		</div>

		<div class="p-4 rounded-lg bg-blue-50 dark:bg-blue-900/20 border border-blue-200 dark:border-blue-800 mb-6">
			<p class="font-semibold text-blue-800 dark:text-blue-200">なぜSupabaseを使うのか？</p>
			<ul class="text-sm text-blue-700 dark:text-blue-300 mt-2 space-y-1">
				<li>・自分でサーバーを用意しなくていい（Firebase的なBaaS）</li>
				<li>・PostgreSQLなのでSQLが使える（Firebaseより直感的）</li>
				<li>・RLS（Row Level Security）で自動的にアクセス制御</li>
				<li>・無料枠が充実（個人開発には十分）</li>
			</ul>
		</div>
	</section>

	<!-- データの流れ -->
	<section class="mb-10">
		<h2 id="data-flow" class="text-xl font-bold mb-4">データの流れを理解する</h2>

		<div class="p-4 rounded-lg bg-gray-100 dark:bg-gray-800 mb-6">
			<p class="text-sm text-gray-600 dark:text-gray-400 mb-4">
				<strong>SvelteKit + Supabaseでは、データは以下のように流れます：</strong>
			</p>
			<div class="flex flex-wrap items-center justify-center gap-2 text-center font-mono text-sm">
				<div class="px-3 py-2 bg-emerald-100 dark:bg-emerald-900 rounded">Supabase DB</div>
				<span>→</span>
				<div class="px-3 py-2 bg-blue-100 dark:bg-blue-900 rounded">load関数</div>
				<span>→</span>
				<div class="px-3 py-2 bg-purple-100 dark:bg-purple-900 rounded">$props()</div>
				<span>→</span>
				<div class="px-3 py-2 bg-orange-100 dark:bg-orange-900 rounded">UI表示</div>
			</div>
		</div>

		<CodePreview
			title="データの流れを追ってみる"
			description="サーバー → クライアントへ"
			language="svelte"
			code={`// ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
// ① +page.server.ts（サーバー側で実行される）
// ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
export const load = async ({ locals }) => {
  // locals.supabase = hooks.server.tsで準備したSupabaseクライアント
  // .from('todos') = todosテーブルを指定
  // .select('*') = 全カラムを取得
  const { data: todos } = await locals.supabase
    .from('todos')
    .select('*')

  // return したオブジェクトがクライアントに渡される
  return { todos: todos ?? [] }
}

// ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
// ② +page.svelte（ブラウザで実行される）
// ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
<script>
  // $props() でサーバーからのデータを受け取る
  // data.todos に load関数で return した todos が入っている
  let { data } = $props()

  // $derived = 元のデータから計算される値
  // data.todos が変わると自動で再計算される
  let completedCount = $derived(
    data.todos.filter(t => t.completed).length
  )
</script>

<!-- data.todos をループして表示 -->
{#each data.todos as todo}
  <div>{todo.title}</div>
{/each}

<p>完了済み: {completedCount}件</p>`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:16px;border-radius:6px;font-size:13px;"><div style="color:#6a9955;">// サーバーで取得 → クライアントで表示</div><div style="margin-top:8px;padding:8px;background:#2d2d2d;border-radius:4px;">□ 買い物に行く<br>✓ メール返信<br>□ レポート作成</div><div style="margin-top:8px;">完了済み: <span style="color:#4ec9b0;">1</span>件</div></div>`}
		/>
	</section>

	<!-- セットアップ -->
	<section class="mb-10">
		<h2 id="setup" class="text-xl font-bold mb-4">1. セットアップ</h2>

		<div class="p-4 rounded-lg bg-amber-50 dark:bg-amber-900/20 border border-amber-200 dark:border-amber-800 mb-4">
			<p class="font-semibold text-amber-800 dark:text-amber-200">必要なパッケージは2つ</p>
			<ul class="text-sm text-amber-700 dark:text-amber-300 mt-2 space-y-1">
				<li><code>@supabase/supabase-js</code> - Supabase本体のクライアント</li>
				<li><code>@supabase/ssr</code> - SSR（サーバーサイドレンダリング）対応用ヘルパー</li>
			</ul>
		</div>

		<CodePreview
			title="パッケージインストール"
			description="ターミナルで実行"
			language="bash"
			code={`# @supabase/supabase-js = Supabaseと通信するためのライブラリ
# @supabase/ssr = SvelteKitのSSRでSupabaseを使うためのヘルパー
npm install @supabase/supabase-js @supabase/ssr`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div style="color:#6a9955;"># なぜ2つ必要？</div><div style="color:#ce9178;">supabase-js だけだとSSR時にCookieが扱えない</div></div>`}
		/>

		<CodePreview
			title=".env - 環境変数ファイル"
			description="プロジェクトルートに作成"
			language="bash"
			code={`# PUBLIC_ で始まる = ブラウザからもアクセスできる
# Supabaseダッシュボード → Settings → API から取得

# プロジェクトのURL（どのSupabaseプロジェクトか）
PUBLIC_SUPABASE_URL=https://あなたのプロジェクト.supabase.co

# anon key（匿名ユーザー用の公開キー）
# このキーは公開しても大丈夫（RLSで保護されるため）
PUBLIC_SUPABASE_ANON_KEY=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div style="color:#f14c4c;">⚠️ .gitignore に .env を追加！</div><div style="color:#6a9955;">// GitHubにキーをアップしない</div></div>`}
		/>

		<div class="p-4 rounded-lg bg-gray-100 dark:bg-gray-800 my-4">
			<p class="font-semibold text-gray-800 dark:text-gray-200 mb-2">anon key とは？</p>
			<p class="text-sm text-gray-600 dark:text-gray-400">
				anon key は「認証されていないユーザー」として API にアクセスするためのキーです。
				公開しても問題ないのは、RLS（Row Level Security）がデータを保護するからです。
				RLSを設定しないと誰でもデータにアクセスできてしまうので注意！
			</p>
		</div>

		<CodePreview
			title="src/lib/supabase.ts - クライアント初期化"
			description="ブラウザ側で使うSupabaseクライアント"
			language="typescript"
			code={`// createClient = Supabaseと通信するためのオブジェクトを作る関数
import { createClient } from '@supabase/supabase-js'

// $env/static/public = .envファイルのPUBLIC_で始まる変数を読み込む
// SvelteKitの機能。process.envは使わない
import { PUBLIC_SUPABASE_URL, PUBLIC_SUPABASE_ANON_KEY } from '$env/static/public'

// supabase = このオブジェクトを使ってDBやAuthにアクセスする
// 例: supabase.from('todos').select('*')
// 例: supabase.auth.signIn({...})
export const supabase = createClient(
  PUBLIC_SUPABASE_URL,     // どのプロジェクトか
  PUBLIC_SUPABASE_ANON_KEY // 認証キー
)`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div style="color:#6a9955;">// このファイルを import して使う</div><div style="color:#ce9178;">import { supabase } from '$lib/supabase'</div></div>`}
		/>
	</section>

	<!-- Hooks設定 -->
	<section class="mb-10">
		<h2 id="hooks" class="text-xl font-bold mb-4">2. Hooksでセッション管理</h2>

		<div class="p-4 rounded-lg bg-amber-50 dark:bg-amber-900/20 border border-amber-200 dark:border-amber-800 mb-4">
			<p class="font-semibold text-amber-800 dark:text-amber-200">なぜHooksが必要なのか？</p>
			<div class="text-sm text-amber-700 dark:text-amber-300 mt-2 space-y-2">
				<p><strong>問題：</strong>SvelteKitはSSR（サーバーサイドレンダリング）を行うため、サーバー側でもユーザーのログイン状態を知る必要があります。</p>
				<p><strong>解決：</strong>Hooksを使って、すべてのリクエストに対して「このユーザーは誰か」を調べて準備します。</p>
			</div>
		</div>

		<div class="p-4 rounded-lg bg-gray-100 dark:bg-gray-800 mb-4">
			<p class="font-semibold text-gray-800 dark:text-gray-200 mb-2">Hooks（フック）とは？</p>
			<p class="text-sm text-gray-600 dark:text-gray-400">
				すべてのリクエストの「前処理」を行う場所です。例えば、ユーザーが <code>/todos</code> にアクセスしたとき、
				ページを表示する前に「ログイン中かどうか」を確認できます。
			</p>
		</div>

		<CodePreview
			title="src/hooks.server.ts"
			description="すべてのリクエストで実行される"
			language="typescript"
			code={`import { PUBLIC_SUPABASE_URL, PUBLIC_SUPABASE_ANON_KEY } from '$env/static/public'
import { createServerClient } from '@supabase/ssr'
import type { Handle } from '@sveltejs/kit'

// handle関数 = すべてのリクエストで最初に実行される
// event = リクエストの情報（URL、Cookie、ヘッダーなど）
// resolve = 次の処理（ページの表示など）に進む関数
export const handle: Handle = async ({ event, resolve }) => {

  // ━━━ ① サーバー用Supabaseクライアントを作成 ━━━
  // なぜ別に作る？ → サーバー側ではCookieの読み書きが必要だから
  event.locals.supabase = createServerClient(
    PUBLIC_SUPABASE_URL,
    PUBLIC_SUPABASE_ANON_KEY,
    {
      cookies: {
        // getAll = 現在のCookieをすべて取得
        // Supabaseはセッション情報をCookieに保存している
        getAll: () => event.cookies.getAll(),

        // setAll = Cookieを設定（ログイン時など）
        setAll: (cookiesToSet) => {
          cookiesToSet.forEach(({ name, value, options }) => {
            event.cookies.set(name, value, { ...options, path: '/' })
          })
        },
      },
    }
  )

  // ━━━ ② セッション取得用のヘルパー関数を追加 ━━━
  // 各ページで簡単にセッションを取得できるようにする
  event.locals.getSession = async () => {
    // getSession() = Cookieからセッション情報を復元
    const { data: { session } } = await event.locals.supabase.auth.getSession()
    // session = ログイン中ならユーザー情報、未ログインならnull
    return session
  }

  // ━━━ ③ 次の処理へ（ページの表示など）━━━
  return resolve(event, {
    // Supabase関連のヘッダーを許可
    filterSerializedResponseHeaders(name) {
      return name === 'content-range' || name === 'x-supabase-api-version'
    },
  })
}`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div style="color:#6a9955;">// これで全ページから使える</div><div>event.locals.<span style="color:#4ec9b0;">supabase</span> → DB操作</div><div>event.locals.<span style="color:#4ec9b0;">getSession()</span> → ログイン確認</div></div>`}
		/>

		<div class="p-4 rounded-lg bg-blue-50 dark:bg-blue-900/20 border border-blue-200 dark:border-blue-800 my-4">
			<p class="font-semibold text-blue-800 dark:text-blue-200">event.locals とは？</p>
			<p class="text-sm text-blue-700 dark:text-blue-300 mt-1">
				リクエスト中にデータを受け渡すための場所です。Hooksで設定した <code>locals.supabase</code> は、
				<code>+page.server.ts</code> や <code>+server.ts</code> から <code>event.locals.supabase</code> でアクセスできます。
			</p>
		</div>

		<CodePreview
			title="src/app.d.ts - 型定義"
			description="TypeScriptに locals の型を教える"
			language="typescript"
			code={`// このファイルは TypeScript に「localsにはこういうデータが入る」と教える
import type { SupabaseClient, Session } from '@supabase/supabase-js'

declare global {
  namespace App {
    // Locals = hooks.server.ts で設定するデータの型
    interface Locals {
      supabase: SupabaseClient              // DBアクセス用クライアント
      getSession: () => Promise<Session | null>  // セッション取得関数
    }
    // PageData = 全ページで受け取れるデータの型
    interface PageData {
      session: Session | null  // ログイン情報
    }
  }
}

export {}`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div style="color:#6a9955;">// 型定義ファイル</div><div style="color:#ce9178;">これがないとTypeScriptがエラーを出す</div></div>`}
		/>
	</section>

	<!-- ルートレイアウト -->
	<section class="mb-10">
		<h2 id="layout" class="text-xl font-bold mb-4">3. ルートレイアウトでセッションを配信</h2>

		<div class="p-4 rounded-lg bg-amber-50 dark:bg-amber-900/20 border border-amber-200 dark:border-amber-800 mb-4">
			<p class="font-semibold text-amber-800 dark:text-amber-200">なぜレイアウトでセッションを取得するのか？</p>
			<p class="text-sm text-amber-700 dark:text-amber-300 mt-1">
				ヘッダーに「ログイン中のユーザー名」を表示したい場合、すべてのページでセッションが必要です。
				ルートレイアウトで1回取得すれば、子ページすべてに配信されます。
			</p>
		</div>

		<CodePreview
			title="src/routes/+layout.server.ts"
			description="全ページにセッションを渡す"
			language="typescript"
			code={`import type { LayoutServerLoad } from './$types'

// LayoutServerLoad = レイアウト用のload関数の型
export const load: LayoutServerLoad = async ({ locals }) => {
  // locals.getSession() = hooks.server.ts で定義した関数
  const session = await locals.getSession()

  // return したデータは全ての子ページで使える
  // +page.svelte で data.session としてアクセス可能
  return {
    session  // null = 未ログイン、オブジェクト = ログイン中
  }
}`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div style="color:#6a9955;">// 全ページで data.session が使える</div></div>`}
		/>

		<CodePreview
			title="src/routes/+layout.svelte"
			description="ログイン状態に応じたUI"
			language="svelte"
			code={`<script lang="ts">
  import { invalidate } from '$app/navigation'
  import { onMount } from 'svelte'
  import { supabase } from '$lib/supabase'

  // data = +layout.server.ts から受け取ったデータ
  // children = このレイアウトの中に表示される子ページ
  let { data, children } = $props()

  onMount(() => {
    // ━━━ 認証状態の変化を監視 ━━━
    // ブラウザ側でログイン/ログアウトしたときに検知
    const { data: { subscription } } = supabase.auth.onAuthStateChange(
      (event) => {
        // 'SIGNED_IN' = ログインした
        // 'SIGNED_OUT' = ログアウトした
        if (event === 'SIGNED_IN' || event === 'SIGNED_OUT') {
          // invalidate = データを再取得してページを更新
          // 'supabase:auth' は任意のキー（識別用）
          invalidate('supabase:auth')
        }
      }
    )

    // コンポーネント破棄時に監視を解除（メモリリーク防止）
    return () => subscription.unsubscribe()
  })
</script>

<!-- ヘッダー部分 -->
<header class="p-4 border-b flex justify-between items-center">
  <h1 class="text-xl font-bold">My App</h1>

  <!-- data.session でログイン状態を判定 -->
  {#if data.session}
    <!-- ログイン中 -->
    <div class="flex items-center gap-4">
      <span>{data.session.user.email}</span>
      <form method="POST" action="/auth/logout">
        <button class="text-red-500">ログアウト</button>
      </form>
    </div>
  {:else}
    <!-- 未ログイン -->
    <a href="/auth/login" class="text-blue-500">ログイン</a>
  {/if}
</header>

<!-- メインコンテンツ（子ページがここに表示される）-->
<main class="p-4">
  {@render children()}
</main>`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div style="color:#6a9955;">// ログイン状態でUIを切り替え</div><div style="margin-top:8px;display:flex;justify-content:space-between;"><span>My App</span><span style="color:#3b82f6;">ログイン</span></div></div>`}
		/>
	</section>

	<!-- 認証ページ -->
	<section class="mb-10">
		<h2 id="auth" class="text-xl font-bold mb-4">4. 認証ページの実装</h2>

		<CodePreview
			title="src/routes/auth/login/+page.svelte"
			description="ログインページ"
			language="svelte"
			code={`<script lang="ts">
  import { supabase } from '$lib/supabase'
  import { goto } from '$app/navigation'

  // $state = Svelte 5 のリアクティブな変数
  // これらの値が変わるとUIが自動更新される
  let email = $state('')       // 入力されたメールアドレス
  let password = $state('')    // 入力されたパスワード
  let loading = $state(false)  // ログイン処理中かどうか
  let error = $state('')       // エラーメッセージ

  // ━━━ メール・パスワードでログイン ━━━
  async function handleLogin(e: Event) {
    e.preventDefault()  // フォームのデフォルト送信を防ぐ
    loading = true      // ローディング開始
    error = ''          // エラーをクリア

    // signInWithPassword = メールとパスワードでログイン
    const { error: authError } = await supabase.auth.signInWithPassword({
      email,
      password
    })

    if (authError) {
      // ログイン失敗 → エラーメッセージを表示
      error = authError.message
    } else {
      // ログイン成功 → トップページに移動
      goto('/')
    }

    loading = false  // ローディング終了
  }

  // ━━━ Googleでログイン ━━━
  async function handleGoogleLogin() {
    // signInWithOAuth = OAuth認証（Google, GitHubなど）
    await supabase.auth.signInWithOAuth({
      provider: 'google',  // 'github', 'twitter' なども可能
      options: {
        // 認証後に戻ってくるURL
        redirectTo: \`\${window.location.origin}/auth/callback\`
      }
    })
  }
</script>

<div class="max-w-md mx-auto mt-10">
  <h1 class="text-2xl font-bold mb-6">ログイン</h1>

  <form onsubmit={handleLogin} class="space-y-4">
    <div>
      <label class="block text-sm font-medium mb-1">メールアドレス</label>
      <!-- bind:value で入力値と変数を双方向バインド -->
      <input
        type="email"
        bind:value={email}
        class="w-full border rounded px-3 py-2"
        required
      />
    </div>

    <div>
      <label class="block text-sm font-medium mb-1">パスワード</label>
      <input
        type="password"
        bind:value={password}
        class="w-full border rounded px-3 py-2"
        required
      />
    </div>

    <!-- エラーがあれば表示 -->
    {#if error}
      <p class="text-red-500 text-sm">{error}</p>
    {/if}

    <button
      type="submit"
      disabled={loading}
      class="w-full bg-blue-500 text-white py-2 rounded hover:bg-blue-600 disabled:opacity-50"
    >
      {loading ? 'ログイン中...' : 'ログイン'}
    </button>
  </form>

  <div class="mt-4">
    <button
      onclick={handleGoogleLogin}
      class="w-full border py-2 rounded hover:bg-gray-50"
    >
      Googleでログイン
    </button>
  </div>
</div>`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div style="color:#6a9955;">// メール認証 + OAuth対応</div></div>`}
		/>

		<CodePreview
			title="src/routes/auth/logout/+page.server.ts"
			description="ログアウト処理"
			language="typescript"
			code={`import { redirect } from '@sveltejs/kit'
import type { Actions } from './$types'

export const actions: Actions = {
  // default = フォームのaction属性を指定しない場合に実行される
  default: async ({ locals }) => {
    // signOut = セッションを破棄してログアウト
    await locals.supabase.auth.signOut()

    // redirect(ステータスコード, 遷移先URL)
    // 303 = POST後のリダイレクトで使う標準的なコード
    throw redirect(303, '/')
  }
}`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div style="color:#6a9955;">// POSTでログアウト → トップへリダイレクト</div></div>`}
		/>

		<CodePreview
			title="src/routes/auth/callback/+server.ts"
			description="OAuth認証後のコールバック"
			language="typescript"
			code={`import { redirect } from '@sveltejs/kit'
import type { RequestHandler } from './$types'

// GET = このURLにGETリクエストが来たときの処理
// GoogleログインからリダイレクトされてくるURL
export const GET: RequestHandler = async ({ url, locals }) => {
  // URLパラメータから認証コードを取得
  // 例: /auth/callback?code=abc123...
  const code = url.searchParams.get('code')

  if (code) {
    // コードをセッションに交換
    // これでログイン完了（Cookieにセッション情報が保存される）
    await locals.supabase.auth.exchangeCodeForSession(code)
  }

  // トップページにリダイレクト
  throw redirect(303, '/')
}`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div style="color:#6a9955;">// Google認証後にここに戻ってくる</div></div>`}
		/>
	</section>

	<!-- Todoアプリ -->
	<section class="mb-10">
		<h2 id="todo" class="text-xl font-bold mb-4">5. 認証付きTodoアプリ</h2>

		<div class="p-4 rounded-lg bg-amber-50 dark:bg-amber-900/20 border border-amber-200 dark:border-amber-800 mb-4">
			<p class="font-semibold text-amber-800 dark:text-amber-200">RLS（Row Level Security）とは？</p>
			<p class="text-sm text-amber-700 dark:text-amber-300 mt-1">
				「自分のデータだけ見れる」を自動で実現する機能です。
				SQLに毎回 <code>WHERE user_id = 現在のユーザーID</code> を書かなくても、
				Supabase側で自動的にフィルタリングしてくれます。
			</p>
		</div>

		<CodePreview
			title="Supabaseでテーブル作成"
			description="ダッシュボードのSQL Editorで実行"
			language="sql"
			code={`-- ━━━ ① テーブル作成 ━━━
CREATE TABLE todos (
  -- id: 自動生成されるユニークなID（UUID形式）
  id UUID DEFAULT gen_random_uuid() PRIMARY KEY,

  -- user_id: このTodoを作成したユーザーのID
  -- auth.users(id) を参照 → 存在しないユーザーIDは登録できない
  -- ON DELETE CASCADE → ユーザー削除時にTodoも自動削除
  user_id UUID REFERENCES auth.users(id) ON DELETE CASCADE,

  -- title: Todoのタイトル（必須）
  title TEXT NOT NULL,

  -- completed: 完了したかどうか（デフォルトは未完了）
  completed BOOLEAN DEFAULT false,

  -- created_at: 作成日時（自動設定）
  created_at TIMESTAMPTZ DEFAULT NOW()
);

-- ━━━ ② RLSを有効化 ━━━
-- これがないとanon keyを持つ誰でもデータにアクセスできてしまう！
ALTER TABLE todos ENABLE ROW LEVEL SECURITY;

-- ━━━ ③ ポリシーを設定 ━━━
-- 「自分のTodoのみ全操作（SELECT, INSERT, UPDATE, DELETE）可能」
CREATE POLICY "Users can CRUD own todos"
  ON todos                      -- todosテーブルに対して
  FOR ALL                       -- 全操作（SELECT, INSERT, UPDATE, DELETE）
  USING (auth.uid() = user_id)  -- 読み取り条件：自分のデータのみ
  WITH CHECK (auth.uid() = user_id);  -- 書き込み条件：自分のデータのみ`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div style="color:#6a9955;">// auth.uid() = 現在ログイン中のユーザーID</div><div style="color:#4ec9b0;">RLSで自動フィルタリング！</div></div>`}
		/>

		<CodePreview
			title="src/routes/todos/+page.server.ts"
			description="Todo一覧取得とCRUD操作"
			language="typescript"
			code={`import { fail, redirect } from '@sveltejs/kit'
import type { PageServerLoad, Actions } from './$types'

// ━━━ データ取得（ページ読み込み時）━━━
export const load: PageServerLoad = async ({ locals }) => {
  // ① ログイン確認
  const session = await locals.getSession()
  if (!session) {
    // 未ログイン → ログインページへ強制リダイレクト
    throw redirect(303, '/auth/login')
  }

  // ② Todoを取得
  // RLSが効いているので、自動的に自分のTodoだけ取得される
  const { data: todos } = await locals.supabase
    .from('todos')            // todosテーブルから
    .select('*')              // 全カラムを
    .order('created_at', { ascending: false })  // 新しい順に

  // ③ クライアントに渡す
  return { todos: todos ?? [] }
}

// ━━━ フォームアクション（ボタンクリック時）━━━
export const actions: Actions = {
  // 【追加】action="?/create" のフォームで呼ばれる
  create: async ({ request, locals }) => {
    const session = await locals.getSession()
    if (!session) return fail(401)  // 未ログイン → 401エラー

    // フォームデータを取得
    const formData = await request.formData()
    const title = formData.get('title') as string

    // バリデーション
    if (!title?.trim()) {
      return fail(400, { message: 'タイトルは必須です' })
    }

    // DBに追加
    // user_id は RLS のために必須
    const { error } = await locals.supabase
      .from('todos')
      .insert({
        title: title.trim(),
        user_id: session.user.id  // 現在のユーザーID
      })

    if (error) return fail(500, { message: error.message })
    return { success: true }
  },

  // 【完了切り替え】action="?/toggle" のフォームで呼ばれる
  toggle: async ({ request, locals }) => {
    const session = await locals.getSession()
    if (!session) return fail(401)

    const formData = await request.formData()
    const id = formData.get('id') as string
    const completed = formData.get('completed') === 'true'

    // completedを反転（true→false, false→true）
    await locals.supabase
      .from('todos')
      .update({ completed: !completed })
      .eq('id', id)  // WHERE id = ?

    return { success: true }
  },

  // 【削除】action="?/delete" のフォームで呼ばれる
  delete: async ({ request, locals }) => {
    const session = await locals.getSession()
    if (!session) return fail(401)

    const formData = await request.formData()
    const id = formData.get('id') as string

    await locals.supabase
      .from('todos')
      .delete()
      .eq('id', id)

    return { success: true }
  }
}`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div style="color:#6a9955;">// load = ページ表示時に実行</div><div style="color:#6a9955;">// actions = フォーム送信時に実行</div></div>`}
		/>

		<CodePreview
			title="src/routes/todos/+page.svelte"
			description="TodoリストのUI"
			language="svelte"
			code={`<script lang="ts">
  // enhance = フォーム送信を非同期化（ページ遷移なしで更新）
  import { enhance } from '$app/forms'

  // data = +page.server.ts の load から受け取ったデータ
  let { data } = $props()
</script>

<div class="max-w-lg mx-auto">
  <h1 class="text-2xl font-bold mb-6">Todoリスト</h1>

  <!-- ━━━ 追加フォーム ━━━ -->
  <!-- method="POST" = サーバーに送信 -->
  <!-- action="?/create" = actionsのcreate関数を呼ぶ -->
  <!-- use:enhance = ページ遷移なしで送信（SPA的な動き）-->
  <form method="POST" action="?/create" use:enhance class="flex gap-2 mb-6">
    <input
      type="text"
      name="title"
      placeholder="新しいタスク..."
      class="flex-1 border rounded px-3 py-2"
    />
    <button class="bg-blue-500 text-white px-4 py-2 rounded">追加</button>
  </form>

  <!-- ━━━ Todoリスト ━━━ -->
  <ul class="space-y-2">
    <!-- data.todos をループして表示 -->
    {#each data.todos as todo}
      <li class="flex items-center gap-3 p-3 border rounded">

        <!-- 完了切り替えボタン -->
        <form method="POST" action="?/toggle" use:enhance>
          <!-- hidden = 画面に表示しないが送信するデータ -->
          <input type="hidden" name="id" value={todo.id} />
          <input type="hidden" name="completed" value={todo.completed} />
          <button class="text-xl">
            {todo.completed ? '✅' : '⬜'}
          </button>
        </form>

        <!-- タイトル（完了時は取り消し線）-->
        <span class:line-through={todo.completed} class="flex-1">
          {todo.title}
        </span>

        <!-- 削除ボタン -->
        <form method="POST" action="?/delete" use:enhance>
          <input type="hidden" name="id" value={todo.id} />
          <button class="text-red-500 hover:text-red-700">削除</button>
        </form>
      </li>
    {/each}
  </ul>

  {#if data.todos.length === 0}
    <p class="text-center text-gray-500">タスクがありません</p>
  {/if}
</div>`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div style="color:#6a9955;">// use:enhance で非同期更新</div><div style="margin-top:8px;padding:8px;background:#2d2d2d;border-radius:4px;">⬜ 買い物<br>✅ 掃除（取り消し線）<br>⬜ 料理</div></div>`}
		/>
	</section>

	<!-- ポイントまとめ -->
	<section class="mb-10">
		<h2 id="summary" class="text-xl font-bold mb-4">ポイントまとめ</h2>

		<div class="grid gap-4">
			<div class="p-4 rounded-lg bg-blue-50 dark:bg-blue-900/20 border border-blue-200 dark:border-blue-800">
				<p class="font-semibold text-blue-800 dark:text-blue-200">hooks.server.ts</p>
				<p class="text-sm text-blue-700 dark:text-blue-300">
					<strong>役割：</strong>すべてのリクエストの前処理<br>
					<strong>何をする：</strong>Supabaseクライアントを準備して <code>event.locals</code> に設定
				</p>
			</div>
			<div class="p-4 rounded-lg bg-green-50 dark:bg-green-900/20 border border-green-200 dark:border-green-800">
				<p class="font-semibold text-green-800 dark:text-green-200">+layout.server.ts</p>
				<p class="text-sm text-green-700 dark:text-green-300">
					<strong>役割：</strong>全ページ共通のデータ取得<br>
					<strong>何をする：</strong>セッションを取得して子ページに配信
				</p>
			</div>
			<div class="p-4 rounded-lg bg-purple-50 dark:bg-purple-900/20 border border-purple-200 dark:border-purple-800">
				<p class="font-semibold text-purple-800 dark:text-purple-200">RLS (Row Level Security)</p>
				<p class="text-sm text-purple-700 dark:text-purple-300">
					<strong>役割：</strong>データベースレベルのアクセス制御<br>
					<strong>何をする：</strong><code>auth.uid() = user_id</code> で自動的に自分のデータだけ取得
				</p>
			</div>
			<div class="p-4 rounded-lg bg-orange-50 dark:bg-orange-900/20 border border-orange-200 dark:border-orange-800">
				<p class="font-semibold text-orange-800 dark:text-orange-200">Form Actions + use:enhance</p>
				<p class="text-sm text-orange-700 dark:text-orange-300">
					<strong>役割：</strong>フォーム送信をサーバーで処理<br>
					<strong>何をする：</strong><code>action="?/create"</code> で対応する関数を呼び出し
				</p>
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
		<a href="/sveltekit/d1" class="inline-flex items-center gap-2 px-4 py-2 rounded-lg bg-primary-600 text-white hover:bg-primary-700 transition-colors">
			次へ：D1連携
			<svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
				<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 5l7 7-7 7" />
			</svg>
		</a>
	</div>
</article>
