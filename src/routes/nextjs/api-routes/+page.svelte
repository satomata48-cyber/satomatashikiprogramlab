<script>
	import CodePreview from '$lib/components/CodePreview.svelte';
</script>

<svelte:head>
	<title>Next.js API Routes | さとまたラボ</title>
</svelte:head>

<article>
	<h1 class="text-3xl font-bold mb-2">API Routes</h1>
	<p class="text-lg text-gray-600 dark:text-gray-400 mb-8">
		Next.jsでバックエンドAPIを作成する
	</p>

	<section class="mb-10">
		<h2 id="basic" class="text-xl font-bold mb-4">基本的なAPI Route</h2>

		<CodePreview
			title="route.ts の作成"
			description="app/api/以下にファイルを作成"
			language="typescript"
			code={`// app/api/hello/route.ts
import { NextResponse } from 'next/server';

export async function GET() {
  return NextResponse.json({
    message: 'Hello, World!'
  });
}

// アクセス: GET /api/hello
// レスポンス: { "message": "Hello, World!" }`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div style="color:#4ec9b0;">GET</div><div>/api/hello</div><div style="margin-top:8px;color:#ce9178;">&#123; "message": "Hello, World!" &#125;</div></div>`}
		/>
	</section>

	<section class="mb-10">
		<h2 id="methods" class="text-xl font-bold mb-4">HTTPメソッド</h2>

		<CodePreview
			title="複数メソッドの定義"
			description="GET, POST, PUT, DELETE など"
			language="typescript"
			code={`// app/api/users/route.ts
import { NextResponse } from 'next/server';

// GET: ユーザー一覧を取得
export async function GET() {
  const users = await db.user.findMany();
  return NextResponse.json(users);
}

// POST: 新規ユーザー作成
export async function POST(request: Request) {
  const body = await request.json();
  const user = await db.user.create({
    data: body
  });
  return NextResponse.json(user, { status: 201 });
}`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div><span style="color:#4ec9b0;">GET</span> /api/users → 一覧取得</div><div><span style="color:#4ec9b0;">POST</span> /api/users → 新規作成</div><div><span style="color:#4ec9b0;">PUT</span> /api/users/1 → 更新</div><div><span style="color:#4ec9b0;">DELETE</span> /api/users/1 → 削除</div></div>`}
		/>
	</section>

	<section class="mb-10">
		<h2 id="dynamic" class="text-xl font-bold mb-4">動的API Route</h2>

		<CodePreview
			title="パラメータを受け取る"
			description="[id]でURLパラメータを取得"
			language="typescript"
			code={`// app/api/users/[id]/route.ts
import { NextResponse } from 'next/server';

interface Context {
  params: { id: string }
}

// GET: 特定ユーザーを取得
export async function GET(
  request: Request,
  { params }: Context
) {
  const user = await db.user.findUnique({
    where: { id: params.id }
  });

  if (!user) {
    return NextResponse.json(
      { error: 'User not found' },
      { status: 404 }
    );
  }

  return NextResponse.json(user);
}

// DELETE: ユーザーを削除
export async function DELETE(
  request: Request,
  { params }: Context
) {
  await db.user.delete({
    where: { id: params.id }
  });

  return new NextResponse(null, { status: 204 });
}`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div>/api/users/<span style="color:#4ec9b0;">[id]</span>/route.ts</div><div style="margin-top:8px;color:#6a9955;">// /api/users/123</div><div style="color:#6a9955;">// → params.id = "123"</div></div>`}
		/>
	</section>

	<section class="mb-10">
		<h2 id="request" class="text-xl font-bold mb-4">リクエストの処理</h2>

		<CodePreview
			title="リクエストボディとクエリパラメータ"
			description="様々なデータの取得方法"
			language="typescript"
			code={`// app/api/search/route.ts
import { NextResponse } from 'next/server';

export async function GET(request: Request) {
  // クエリパラメータを取得
  const { searchParams } = new URL(request.url);
  const query = searchParams.get('q');
  const limit = searchParams.get('limit') || '10';

  // /api/search?q=hello&limit=5
  // → query = "hello", limit = "5"

  const results = await search(query, parseInt(limit));
  return NextResponse.json(results);
}

export async function POST(request: Request) {
  // JSONボディを取得
  const body = await request.json();

  // フォームデータを取得
  // const formData = await request.formData();
  // const name = formData.get('name');

  // ヘッダーを取得
  const authHeader = request.headers.get('Authorization');

  return NextResponse.json({ received: body });
}`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div style="color:#6a9955;">// クエリパラメータ</div><div>searchParams.get('q')</div><div style="margin-top:8px;color:#6a9955;">// JSONボディ</div><div>await request.json()</div><div style="margin-top:8px;color:#6a9955;">// ヘッダー</div><div>request.headers.get('Authorization')</div></div>`}
		/>
	</section>

	<section class="mb-10">
		<h2 id="response" class="text-xl font-bold mb-4">レスポンスの設定</h2>

		<CodePreview
			title="カスタムレスポンス"
			description="ステータスコードやヘッダーを設定"
			language="typescript"
			code={`import { NextResponse } from 'next/server';

export async function GET() {
  // 基本的なJSONレスポンス
  return NextResponse.json({ data: 'value' });

  // ステータスコード付き
  return NextResponse.json(
    { error: 'Not found' },
    { status: 404 }
  );

  // カスタムヘッダー
  return NextResponse.json(
    { data: 'value' },
    {
      status: 200,
      headers: {
        'Cache-Control': 'max-age=3600',
        'X-Custom-Header': 'value'
      }
    }
  );

  // リダイレクト
  return NextResponse.redirect(new URL('/login', request.url));
}`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div><span style="color:#b5cea8;">200</span> OK</div><div><span style="color:#b5cea8;">201</span> Created</div><div><span style="color:#b5cea8;">204</span> No Content</div><div><span style="color:#b5cea8;">400</span> Bad Request</div><div><span style="color:#b5cea8;">404</span> Not Found</div><div><span style="color:#b5cea8;">500</span> Server Error</div></div>`}
		/>
	</section>

	<section class="mb-10">
		<h2 id="middleware" class="text-xl font-bold mb-4">ミドルウェア</h2>

		<CodePreview
			title="middleware.ts"
			description="リクエストをインターセプト"
			language="typescript"
			code={`// middleware.ts (プロジェクトルート)
import { NextResponse } from 'next/server';
import type { NextRequest } from 'next/server';

export function middleware(request: NextRequest) {
  // 認証チェック
  const token = request.cookies.get('token');

  if (!token && request.nextUrl.pathname.startsWith('/api/protected')) {
    return NextResponse.json(
      { error: 'Unauthorized' },
      { status: 401 }
    );
  }

  return NextResponse.next();
}

// 適用するパスを指定
export const config = {
  matcher: '/api/:path*'
};`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div style="color:#6a9955;">// 全てのAPIリクエストの前に実行</div><div style="color:#6a9955;">// 認証、ログ、レート制限などに使う</div></div>`}
		/>
	</section>

	<div class="flex justify-between pt-6 border-t border-gray-200 dark:border-gray-700">
		<a href="/nextjs/data-fetching" class="inline-flex items-center gap-2 px-4 py-2 rounded-lg border border-gray-300 dark:border-gray-600 hover:bg-gray-100 dark:hover:bg-gray-800 transition-colors">
			<svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
				<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 19l-7-7 7-7" />
			</svg>
			前へ：データ取得
		</a>
		<a href="/sveltekit/intro" class="inline-flex items-center gap-2 px-4 py-2 rounded-lg bg-primary-600 text-white hover:bg-primary-700 transition-colors">
			次へ：SvelteKit
			<svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
				<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 5l7 7-7 7" />
			</svg>
		</a>
	</div>
</article>
