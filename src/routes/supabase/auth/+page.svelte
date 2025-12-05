<script>
	import CodePreview from '$lib/components/CodePreview.svelte';
</script>

<svelte:head>
	<title>Supabase 認証 | さとまたラボ</title>
</svelte:head>

<article>
	<h1 class="text-3xl font-bold mb-2">認証（Auth）</h1>
	<p class="text-lg text-gray-600 dark:text-gray-400 mb-8">
		Supabaseでユーザー認証を実装する
	</p>

	<!-- 認証の概要 -->
	<section class="mb-10">
		<h2 id="overview" class="text-xl font-bold mb-4">Supabase Authとは</h2>

		<div class="p-6 rounded-xl bg-emerald-50 dark:bg-emerald-900/20 border border-emerald-200 dark:border-emerald-800 mb-6">
			<p class="text-emerald-800 dark:text-emerald-200 mb-4">
				<strong>対応している認証方法：</strong>
			</p>
			<div class="grid grid-cols-2 md:grid-cols-4 gap-3 text-sm">
				<div class="p-2 bg-white dark:bg-gray-800 rounded text-center">メール/パスワード</div>
				<div class="p-2 bg-white dark:bg-gray-800 rounded text-center">マジックリンク</div>
				<div class="p-2 bg-white dark:bg-gray-800 rounded text-center">Google</div>
				<div class="p-2 bg-white dark:bg-gray-800 rounded text-center">GitHub</div>
				<div class="p-2 bg-white dark:bg-gray-800 rounded text-center">Twitter/X</div>
				<div class="p-2 bg-white dark:bg-gray-800 rounded text-center">Discord</div>
				<div class="p-2 bg-white dark:bg-gray-800 rounded text-center">Apple</div>
				<div class="p-2 bg-white dark:bg-gray-800 rounded text-center">電話番号（SMS）</div>
			</div>
		</div>
	</section>

	<!-- メール認証 -->
	<section class="mb-10">
		<h2 id="email" class="text-xl font-bold mb-4">メール/パスワード認証</h2>

		<CodePreview
			title="サインアップ（新規登録）"
			description="メールアドレスとパスワードで登録"
			language="typescript"
			code={`const { data, error } = await supabase.auth.signUp({
  email: 'user@example.com',
  password: 'securepassword123',
  options: {
    // メール確認後のリダイレクト先
    emailRedirectTo: 'http://localhost:5173/auth/callback',
    // ユーザーメタデータ（オプション）
    data: {
      full_name: '田中太郎',
      avatar_url: 'https://...'
    }
  }
})

if (error) {
  console.error('サインアップエラー:', error.message)
} else {
  console.log('確認メールを送信しました')
}`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div style="color:#6a9955;">// 確認メールが送られる</div></div>`}
		/>

		<CodePreview
			title="ログイン"
			description="メールアドレスとパスワードでログイン"
			language="typescript"
			code={`const { data, error } = await supabase.auth.signInWithPassword({
  email: 'user@example.com',
  password: 'securepassword123'
})

if (error) {
  console.error('ログインエラー:', error.message)
} else {
  console.log('ログイン成功！', data.user)
}`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div style="color:#6a9955;">// セッションが自動的に管理される</div></div>`}
		/>
	</section>

	<!-- OAuth -->
	<section class="mb-10">
		<h2 id="oauth" class="text-xl font-bold mb-4">ソーシャルログイン（OAuth）</h2>

		<div class="p-4 rounded-lg bg-amber-50 dark:bg-amber-900/20 border border-amber-200 dark:border-amber-800 mb-4">
			<p class="font-semibold text-amber-800 dark:text-amber-200">事前設定が必要</p>
			<p class="text-sm text-amber-700 dark:text-amber-300 mt-1">
				Supabaseダッシュボード → Authentication → Providers で各プロバイダーを有効化し、Client IDとSecretを設定してください。
			</p>
		</div>

		<CodePreview
			title="Googleでログイン"
			description="OAuthプロバイダーでログイン"
			language="typescript"
			code={`// Googleでログイン
const { data, error } = await supabase.auth.signInWithOAuth({
  provider: 'google',
  options: {
    redirectTo: 'http://localhost:5173/auth/callback'
  }
})

// GitHubでログイン
await supabase.auth.signInWithOAuth({
  provider: 'github'
})

// Discordでログイン
await supabase.auth.signInWithOAuth({
  provider: 'discord'
})`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div style="color:#6a9955;">// 外部サイトにリダイレクト</div></div>`}
		/>

		<CodePreview
			title="コールバック処理"
			description="src/routes/auth/callback/+server.ts"
			language="typescript"
			code={`import { redirect } from '@sveltejs/kit'
import type { RequestHandler } from './$types'

export const GET: RequestHandler = async ({ url, locals }) => {
  const code = url.searchParams.get('code')

  if (code) {
    // 認証コードをセッションに交換
    await locals.supabase.auth.exchangeCodeForSession(code)
  }

  // ホームにリダイレクト
  throw redirect(303, '/')
}`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div style="color:#6a9955;">// OAuth後のリダイレクト先</div></div>`}
		/>
	</section>

	<!-- セッション管理 -->
	<section class="mb-10">
		<h2 id="session" class="text-xl font-bold mb-4">セッション管理</h2>

		<CodePreview
			title="現在のユーザーを取得"
			description="ログイン中のユーザー情報"
			language="typescript"
			code={`// ユーザー情報を取得
const { data: { user } } = await supabase.auth.getUser()

if (user) {
  console.log('ユーザーID:', user.id)
  console.log('メール:', user.email)
  console.log('メタデータ:', user.user_metadata)
} else {
  console.log('ログインしていません')
}

// セッションを取得
const { data: { session } } = await supabase.auth.getSession()

if (session) {
  console.log('アクセストークン:', session.access_token)
  console.log('有効期限:', session.expires_at)
}`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div><span style="color:#dcdcaa;">getUser()</span> → ユーザー情報</div><div><span style="color:#dcdcaa;">getSession()</span> → セッション情報</div></div>`}
		/>

		<CodePreview
			title="ログアウト"
			description="セッションを終了"
			language="typescript"
			code={`const { error } = await supabase.auth.signOut()

if (error) {
  console.error('ログアウトエラー:', error.message)
} else {
  console.log('ログアウトしました')
}`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div style="color:#6a9955;">// Cookie等も自動削除</div></div>`}
		/>
	</section>

	<!-- 認証状態の監視 -->
	<section class="mb-10">
		<h2 id="listener" class="text-xl font-bold mb-4">認証状態の監視</h2>

		<CodePreview
			title="リアルタイムで認証状態を監視"
			description="ログイン/ログアウトを検知"
			language="typescript"
			code={`// 認証状態の変化を監視
const { data: { subscription } } = supabase.auth.onAuthStateChange(
  (event, session) => {
    console.log('認証イベント:', event)
    // event: 'SIGNED_IN', 'SIGNED_OUT', 'TOKEN_REFRESHED' など

    if (session) {
      console.log('ログイン中:', session.user.email)
    } else {
      console.log('ログアウト状態')
    }
  }
)

// 監視を解除（クリーンアップ）
// subscription.unsubscribe()`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div style="color:#6a9955;">// ログイン/ログアウトを自動検知</div></div>`}
		/>
	</section>

	<!-- SvelteKitでの実装例 -->
	<section class="mb-10">
		<h2 id="sveltekit-example" class="text-xl font-bold mb-4">SvelteKitでの実装例</h2>

		<CodePreview
			title="ログインフォーム"
			description="src/routes/login/+page.svelte"
			language="svelte"
			code={`<script lang="ts">
  import { supabase } from '$lib/supabase'
  import { goto } from '$app/navigation'

  let email = $state('')
  let password = $state('')
  let loading = $state(false)
  let error = $state('')

  async function handleLogin() {
    loading = true
    error = ''

    const { error: authError } = await supabase.auth.signInWithPassword({
      email,
      password
    })

    if (authError) {
      error = authError.message
    } else {
      goto('/')  // ホームにリダイレクト
    }

    loading = false
  }
</script>

<form onsubmit={handleLogin}>
  <input type="email" bind:value={email} placeholder="メールアドレス" />
  <input type="password" bind:value={password} placeholder="パスワード" />

  {#if error}
    <p class="text-red-500">{error}</p>
  {/if}

  <button type="submit" disabled={loading}>
    {loading ? 'ログイン中...' : 'ログイン'}
  </button>
</form>`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div style="color:#6a9955;">// シンプルなログインフォーム</div></div>`}
		/>
	</section>

	<!-- ナビゲーション -->
	<div class="flex justify-between pt-6 border-t border-gray-200 dark:border-gray-700">
		<a href="/supabase/database" class="inline-flex items-center gap-2 px-4 py-2 rounded-lg border border-gray-300 dark:border-gray-600 hover:bg-gray-100 dark:hover:bg-gray-800 transition-colors">
			<svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
				<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 19l-7-7 7-7" />
			</svg>
			前へ：データベース操作
		</a>
		<a href="/supabase/storage" class="inline-flex items-center gap-2 px-4 py-2 rounded-lg bg-primary-600 text-white hover:bg-primary-700 transition-colors">
			次へ：ストレージ
			<svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
				<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 5l7 7-7 7" />
			</svg>
		</a>
	</div>
</article>
