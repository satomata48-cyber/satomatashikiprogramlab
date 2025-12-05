<script>
	import CodePreview from '$lib/components/CodePreview.svelte';
</script>

<svelte:head>
	<title>SvelteKit フォームアクション | さとまたラボ</title>
</svelte:head>

<article>
	<h1 class="text-3xl font-bold mb-2">フォームアクション</h1>
	<p class="text-lg text-gray-600 dark:text-gray-400 mb-8">
		サーバーサイドでフォームを処理する
	</p>

	<!-- フォームアクションとは -->
	<section class="mb-10">
		<h2 id="what-is" class="text-xl font-bold mb-4">フォームアクションとは？</h2>

		<div class="p-6 rounded-xl bg-blue-50 dark:bg-blue-900/20 border border-blue-200 dark:border-blue-800 mb-6">
			<p class="text-blue-800 dark:text-blue-200 mb-4">
				<strong>日常での例え：</strong>窓口での申請処理
			</p>
			<div class="text-sm text-blue-700 dark:text-blue-300 space-y-2">
				<p>申請書（フォーム）に記入して窓口に提出</p>
				<p>職員（サーバー）が内容をチェック・処理</p>
				<p>結果を返す（成功/エラー）</p>
			</div>
		</div>

		<div class="p-4 rounded-lg bg-amber-50 dark:bg-amber-900/20 border border-amber-200 dark:border-amber-800 mb-6">
			<p class="font-semibold text-amber-800 dark:text-amber-200">なぜフォームアクションが便利？</p>
			<div class="text-sm text-amber-700 dark:text-amber-300 mt-2">
				<p class="mb-2"><strong>従来の方法</strong>：fetch() で自分でAPIを呼び出す → コードが複雑に</p>
				<p class="mb-2"><strong>フォームアクション</strong>：HTMLの &lt;form&gt; を使うだけ！</p>
				<ul class="list-disc list-inside space-y-1">
					<li>JavaScriptが無効でも動作する（アクセシビリティ）</li>
					<li>バリデーションエラーと入力値の復元が簡単</li>
					<li>use:enhance でJSによる機能強化も可能</li>
				</ul>
			</div>
		</div>
	</section>

	<section class="mb-10">
		<h2 id="basic" class="text-xl font-bold mb-4">基本的なフォームアクション</h2>

		<CodePreview
			title="アクションの定義"
			description="+page.server.tsにactionsを定義"
			language="typescript"
			code={`// src/routes/login/+page.server.ts
export const actions = {
  default: async ({ request }) => {
    const data = await request.formData();
    const email = data.get('email');
    const password = data.get('password');

    // バリデーション
    if (!email || !password) {
      return { success: false, error: '入力してください' };
    }

    // ログイン処理...

    return { success: true };
  }
};`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div style="color:#6a9955;">// form の method="POST" で</div><div style="color:#6a9955;">// actions.default が呼ばれる</div></div>`}
		/>

		<CodePreview
			title="フォームの実装"
			description="method=POSTで送信"
			language="svelte"
			code={`<!-- src/routes/login/+page.svelte -->
<script>
  let { form } = $props();
</script>

<form method="POST">
  <input name="email" type="email" required>
  <input name="password" type="password" required>
  <button type="submit">ログイン</button>
</form>

{#if form?.error}
  <p class="error">{form.error}</p>
{/if}

{#if form?.success}
  <p class="success">ログイン成功！</p>
{/if}`}
			previewHtml={`<form style="display:flex;flex-direction:column;gap:8px;max-width:250px;"><input type="email" placeholder="メールアドレス" style="padding:8px;border:1px solid #d1d5db;border-radius:4px;"><input type="password" placeholder="パスワード" style="padding:8px;border:1px solid #d1d5db;border-radius:4px;"><button style="padding:8px 16px;background:#ff3e00;color:white;border:none;border-radius:4px;cursor:pointer;">ログイン</button></form>`}
		/>
	</section>

	<section class="mb-10">
		<h2 id="named" class="text-xl font-bold mb-4">名前付きアクション</h2>

		<CodePreview
			title="複数のアクション"
			description="action属性で指定"
			language="typescript"
			code={`// src/routes/posts/+page.server.ts
export const actions = {
  create: async ({ request }) => {
    const data = await request.formData();
    const title = data.get('title');
    await createPost({ title });
    return { success: true };
  },

  delete: async ({ request }) => {
    const data = await request.formData();
    const id = data.get('id');
    await deletePost(id);
    return { deleted: true };
  }
};`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div>actions.<span style="color:#4ec9b0;">create</span></div><div>actions.<span style="color:#4ec9b0;">delete</span></div></div>`}
		/>

		<CodePreview
			title="名前付きアクションの呼び出し"
			description="action=?/アクション名"
			language="svelte"
			code={`<!-- 投稿作成フォーム -->
<form method="POST" action="?/create">
  <input name="title" required>
  <button>投稿</button>
</form>

<!-- 削除フォーム -->
<form method="POST" action="?/delete">
  <input type="hidden" name="id" value={post.id}>
  <button>削除</button>
</form>`}
			previewHtml={`<div style="display:flex;flex-direction:column;gap:12px;"><form style="display:flex;gap:8px;"><input placeholder="タイトル" style="padding:8px;border:1px solid #d1d5db;border-radius:4px;flex:1;"><button style="padding:8px 16px;background:#22c55e;color:white;border:none;border-radius:4px;">投稿</button></form><button style="padding:8px 16px;background:#ef4444;color:white;border:none;border-radius:4px;width:fit-content;">削除</button></div>`}
		/>
	</section>

	<section class="mb-10">
		<h2 id="validation" class="text-xl font-bold mb-4">バリデーション</h2>

		<CodePreview
			title="fail関数でエラーを返す"
			description="入力値を保持してエラー表示"
			language="typescript"
			code={`// src/routes/register/+page.server.ts
import { fail } from '@sveltejs/kit';

export const actions = {
  default: async ({ request }) => {
    const data = await request.formData();
    const email = data.get('email')?.toString();
    const password = data.get('password')?.toString();

    // バリデーション
    if (!email?.includes('@')) {
      return fail(400, {
        email,  // 入力値を返す
        error: 'メールアドレスが無効です'
      });
    }

    if (password && password.length < 8) {
      return fail(400, {
        email,
        error: 'パスワードは8文字以上'
      });
    }

    // 登録処理...
    return { success: true };
  }
};`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div><span style="color:#dcdcaa;">fail</span>(400, &#123; error: '...' &#125;)</div><div style="color:#6a9955;">// ステータス400でエラーを返す</div><div style="color:#6a9955;">// 入力値も一緒に返せる</div></div>`}
		/>

		<CodePreview
			title="エラー表示とフォームの復元"
			description="form propsでアクセス"
			language="svelte"
			code={`<script>
  let { form } = $props();
</script>

<form method="POST">
  <label>
    メールアドレス
    <input
      name="email"
      type="email"
      value={form?.email ?? ''}
    >
  </label>

  <label>
    パスワード
    <input name="password" type="password">
  </label>

  {#if form?.error}
    <p class="error">{form.error}</p>
  {/if}

  <button>登録</button>
</form>`}
			previewHtml={`<form style="display:flex;flex-direction:column;gap:8px;max-width:250px;"><label style="font-size:14px;">メールアドレス<input type="email" value="invalid-email" style="width:100%;padding:8px;border:1px solid #ef4444;border-radius:4px;margin-top:4px;"></label><p style="color:#ef4444;font-size:14px;">メールアドレスが無効です</p><button style="padding:8px 16px;background:#ff3e00;color:white;border:none;border-radius:4px;">登録</button></form>`}
		/>
	</section>

	<section class="mb-10">
		<h2 id="enhance" class="text-xl font-bold mb-4">プログレッシブエンハンスメント</h2>

		<CodePreview
			title="use:enhance"
			description="JavaScriptでフォームを強化"
			language="svelte"
			code={`<script>
  import { enhance } from '$app/forms';

  let loading = $state(false);
</script>

<form
  method="POST"
  use:enhance={() => {
    loading = true;

    return async ({ result, update }) => {
      loading = false;

      if (result.type === 'success') {
        // 成功時の処理
      }

      await update();  // デフォルトの更新処理
    };
  }}
>
  <button disabled={loading}>
    {loading ? '送信中...' : '送信'}
  </button>
</form>`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div style="color:#6a9955;">// use:enhance で</div><div style="color:#6a9955;">// - ページ遷移なしで送信</div><div style="color:#6a9955;">// - ローディング状態の管理</div><div style="color:#6a9955;">// - 成功/失敗時のカスタム処理</div></div>`}
		/>
	</section>

	<section class="mb-10">
		<h2 id="redirect-after" class="text-xl font-bold mb-4">アクション後のリダイレクト</h2>

		<CodePreview
			title="成功後にリダイレクト"
			description="redirect関数を使用"
			language="typescript"
			code={`// src/routes/login/+page.server.ts
import { redirect, fail } from '@sveltejs/kit';

export const actions = {
  default: async ({ request, cookies }) => {
    const data = await request.formData();
    const email = data.get('email');
    const password = data.get('password');

    const user = await login(email, password);

    if (!user) {
      return fail(401, {
        email,
        error: 'メールアドレスまたはパスワードが違います'
      });
    }

    // セッションを設定
    cookies.set('session', user.sessionId, { path: '/' });

    // ダッシュボードへリダイレクト
    redirect(303, '/dashboard');
  }
};`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div style="color:#6a9955;">// 成功 → redirect()</div><div style="color:#6a9955;">// 失敗 → fail() でエラーを返す</div></div>`}
		/>
	</section>

	<div class="flex justify-between pt-6 border-t border-gray-200 dark:border-gray-700">
		<a href="/sveltekit/loading" class="inline-flex items-center gap-2 px-4 py-2 rounded-lg border border-gray-300 dark:border-gray-600 hover:bg-gray-100 dark:hover:bg-gray-800 transition-colors">
			<svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
				<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 19l-7-7 7-7" />
			</svg>
			前へ：データ読み込み
		</a>
		<a href="/sveltekit/hooks" class="inline-flex items-center gap-2 px-4 py-2 rounded-lg bg-primary-600 text-white hover:bg-primary-700 transition-colors">
			次へ：Hooks
			<svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
				<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 5l7 7-7 7" />
			</svg>
		</a>
	</div>
</article>
