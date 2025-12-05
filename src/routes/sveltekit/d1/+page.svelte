<script>
	import CodePreview from '$lib/components/CodePreview.svelte';
</script>

<svelte:head>
	<title>SvelteKit × D1連携 | さとまたラボ</title>
</svelte:head>

<article>
	<h1 class="text-3xl font-bold mb-2">D1連携</h1>
	<p class="text-lg text-gray-600 dark:text-gray-400 mb-8">
		SvelteKitでCloudflare D1を使ってデータを保存しよう
	</p>

	<!-- まず何を作るか -->
	<section class="mb-12">
		<h2 id="goal" class="text-xl font-bold mb-4">この章のゴール</h2>

		<div class="p-6 rounded-xl bg-gradient-to-r from-orange-50 to-amber-50 dark:from-orange-900/20 dark:to-amber-900/20 border border-orange-200 dark:border-orange-800 mb-6">
			<p class="text-lg text-orange-800 dark:text-orange-200 mb-4">
				「Todoリスト」を作りながら、<strong>データベースの基本</strong>を学びます
			</p>
			<div class="bg-white/70 dark:bg-black/30 rounded-lg p-4">
				<p class="text-sm text-gray-700 dark:text-gray-300 mb-2">完成イメージ：</p>
				<div class="font-mono text-sm bg-gray-100 dark:bg-gray-800 p-3 rounded">
					<div class="flex items-center gap-2 mb-1">⬜ 牛乳を買う</div>
					<div class="flex items-center gap-2 mb-1">✅ <span class="line-through text-gray-400">メールを返信する</span></div>
					<div class="flex items-center gap-2">⬜ 部屋を掃除する</div>
				</div>
				<p class="text-xs text-gray-500 mt-2">追加・完了・削除ができて、ページを閉じてもデータが残る</p>
			</div>
		</div>
	</section>

	<!-- そもそもデータベースとは -->
	<section class="mb-12">
		<h2 id="what-is-database" class="text-xl font-bold mb-4">そもそもデータベースって何？</h2>

		<p class="text-gray-700 dark:text-gray-300 mb-4">
			今まで作ったアプリを思い出してください。ページをリロードすると、入力したデータは消えてしまいましたよね？
		</p>

		<div class="grid md:grid-cols-2 gap-4 mb-6">
			<div class="p-4 rounded-lg bg-red-50 dark:bg-red-900/20 border border-red-200 dark:border-red-800">
				<p class="font-semibold text-red-800 dark:text-red-200 mb-2">今までのアプリ</p>
				<p class="text-sm text-red-700 dark:text-red-300">
					データは「ブラウザのメモリ」にある<br>
					→ リロードすると消える<br>
					→ 別のパソコンからは見れない
				</p>
			</div>
			<div class="p-4 rounded-lg bg-green-50 dark:bg-green-900/20 border border-green-200 dark:border-green-800">
				<p class="font-semibold text-green-800 dark:text-green-200 mb-2">データベースを使うと</p>
				<p class="text-sm text-green-700 dark:text-green-300">
					データは「サーバーに保存」される<br>
					→ リロードしても消えない<br>
					→ どこからでもアクセスできる
				</p>
			</div>
		</div>

		<div class="p-4 rounded-lg bg-blue-50 dark:bg-blue-900/20 border border-blue-200 dark:border-blue-800 mb-6">
			<p class="font-semibold text-blue-800 dark:text-blue-200 mb-2">データベースを身近な例で例えると...</p>
			<p class="text-sm text-blue-700 dark:text-blue-300">
				<strong>Excelのスプレッドシート</strong>を想像してください。
				行と列があって、データを整理して保存できますよね。
				データベースも同じで、「テーブル（表）」にデータを保存します。
			</p>
			<div class="mt-3 bg-white dark:bg-gray-800 rounded p-3 font-mono text-xs overflow-x-auto">
				<table class="w-full">
					<thead>
						<tr class="border-b">
							<th class="text-left p-1">id</th>
							<th class="text-left p-1">title</th>
							<th class="text-left p-1">completed</th>
						</tr>
					</thead>
					<tbody>
						<tr class="border-b border-gray-200 dark:border-gray-700">
							<td class="p-1">1</td>
							<td class="p-1">牛乳を買う</td>
							<td class="p-1">0（未完了）</td>
						</tr>
						<tr class="border-b border-gray-200 dark:border-gray-700">
							<td class="p-1">2</td>
							<td class="p-1">メールを返信する</td>
							<td class="p-1">1（完了）</td>
						</tr>
						<tr>
							<td class="p-1">3</td>
							<td class="p-1">部屋を掃除する</td>
							<td class="p-1">0（未完了）</td>
						</tr>
					</tbody>
				</table>
			</div>
		</div>
	</section>

	<!-- D1とは -->
	<section class="mb-12">
		<h2 id="what-is-d1" class="text-xl font-bold mb-4">D1って何？なぜ使うの？</h2>

		<p class="text-gray-700 dark:text-gray-300 mb-4">
			データベースには色々な種類がありますが、今回は <strong>Cloudflare D1</strong> を使います。
		</p>

		<div class="p-5 rounded-xl bg-orange-50 dark:bg-orange-900/20 border border-orange-200 dark:border-orange-800 mb-6">
			<p class="font-bold text-orange-800 dark:text-orange-200 mb-3">D1を選ぶ理由</p>
			<div class="space-y-3 text-sm text-orange-700 dark:text-orange-300">
				<div class="flex gap-3">
					<span class="text-xl">1</span>
					<div>
						<strong>無料で始められる</strong><br>
						<span class="text-xs">個人開発なら十分な無料枠があります</span>
					</div>
				</div>
				<div class="flex gap-3">
					<span class="text-xl">2</span>
					<div>
						<strong>設定が簡単</strong><br>
						<span class="text-xs">自分でサーバーを用意する必要がありません</span>
					</div>
				</div>
				<div class="flex gap-3">
					<span class="text-xl">3</span>
					<div>
						<strong>Cloudflare Pagesと相性が良い</strong><br>
						<span class="text-xs">SvelteKitアプリと一緒にデプロイできます</span>
					</div>
				</div>
			</div>
		</div>

		<div class="p-4 rounded-lg bg-amber-50 dark:bg-amber-900/20 border border-amber-200 dark:border-amber-800">
			<p class="font-semibold text-amber-800 dark:text-amber-200 mb-2">Supabaseとどっちを使えばいい？</p>
			<p class="text-sm text-amber-700 dark:text-amber-300">
				<strong>ログイン機能が必要なら → Supabase</strong>（認証機能が組み込まれている）<br>
				<strong>データ保存だけなら → D1</strong>（シンプルで軽量）<br><br>
				今回はシンプルなTodoアプリなので、D1で十分です。
			</p>
		</div>
	</section>

	<!-- 準備 -->
	<section class="mb-12">
		<h2 id="preparation" class="text-xl font-bold mb-4">Step 1：準備</h2>

		<p class="text-gray-700 dark:text-gray-300 mb-4">
			D1を使うには、いくつかの準備が必要です。一つずつ進めていきましょう。
		</p>

		<!-- Cloudflareアカウント -->
		<div class="mb-8">
			<h3 class="text-lg font-semibold mb-3 flex items-center gap-2">
				<span class="w-7 h-7 bg-orange-500 text-white rounded-full flex items-center justify-center text-sm">1</span>
				Cloudflareアカウントを作る
			</h3>

			<div class="ml-9">
				<p class="text-gray-600 dark:text-gray-400 mb-3">
					まだCloudflareのアカウントがない場合は、先に作成してください。
				</p>
				<a
					href="https://dash.cloudflare.com/sign-up"
					target="_blank"
					rel="noopener"
					class="inline-flex items-center gap-2 text-blue-600 dark:text-blue-400 hover:underline"
				>
					Cloudflare サインアップページ →
				</a>
			</div>
		</div>

		<!-- Wranglerインストール -->
		<div class="mb-8">
			<h3 class="text-lg font-semibold mb-3 flex items-center gap-2">
				<span class="w-7 h-7 bg-orange-500 text-white rounded-full flex items-center justify-center text-sm">2</span>
				Wrangler（ラングラー）をインストール
			</h3>

			<div class="ml-9">
				<div class="p-4 rounded-lg bg-gray-50 dark:bg-gray-800 mb-4">
					<p class="font-semibold text-gray-800 dark:text-gray-200 mb-2">Wranglerって何？</p>
					<p class="text-sm text-gray-600 dark:text-gray-400">
						Cloudflareを操作するためのコマンドラインツールです。
						データベースを作ったり、アプリをデプロイしたりするのに使います。
					</p>
				</div>

				<CodePreview
					title="ターミナルで実行"
					description=""
					language="bash"
					code={`npm install -g wrangler`}
					previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div style="color:#6a9955;"># -g は「グローバル」の意味</div><div style="color:#6a9955;"># どのプロジェクトからでも使えるようになる</div></div>`}
				/>
			</div>
		</div>

		<!-- ログイン -->
		<div class="mb-8">
			<h3 class="text-lg font-semibold mb-3 flex items-center gap-2">
				<span class="w-7 h-7 bg-orange-500 text-white rounded-full flex items-center justify-center text-sm">3</span>
				Cloudflareにログイン
			</h3>

			<div class="ml-9">
				<CodePreview
					title="ターミナルで実行"
					description=""
					language="bash"
					code={`wrangler login`}
					previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div style="color:#6a9955;"># ブラウザが自動で開く</div><div style="color:#6a9955;"># 「Allow」をクリックして認証</div></div>`}
				/>

				<p class="text-sm text-gray-600 dark:text-gray-400 mt-3">
					このコマンドを実行すると、ブラウザが開いてCloudflareの認証画面が表示されます。
					「Allow」をクリックすると、ターミナルとCloudflareが連携されます。
				</p>
			</div>
		</div>

		<!-- D1作成 -->
		<div class="mb-8">
			<h3 class="text-lg font-semibold mb-3 flex items-center gap-2">
				<span class="w-7 h-7 bg-orange-500 text-white rounded-full flex items-center justify-center text-sm">4</span>
				データベースを作成
			</h3>

			<div class="ml-9">
				<CodePreview
					title="ターミナルで実行"
					description=""
					language="bash"
					code={`wrangler d1 create my-todo-db`}
					previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div style="color:#6a9955;"># my-todo-db = データベースの名前</div><div style="color:#6a9955;"># 好きな名前を付けてOK</div></div>`}
				/>

				<div class="mt-4 p-4 rounded-lg bg-green-50 dark:bg-green-900/20 border border-green-200 dark:border-green-800">
					<p class="font-semibold text-green-800 dark:text-green-200 mb-2">成功するとこんな表示が出ます</p>
					<pre class="text-xs bg-gray-800 text-green-400 p-3 rounded overflow-x-auto">
{`✅ Successfully created DB 'my-todo-db'

[[d1_databases]]
binding = "DB"
database_name = "my-todo-db"
database_id = "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"`}</pre>
					<p class="text-sm text-green-700 dark:text-green-300 mt-2">
						<strong>この表示は後で使うので、コピーしておいてください！</strong>
					</p>
				</div>
			</div>
		</div>
	</section>

	<!-- プロジェクト設定 -->
	<section class="mb-12">
		<h2 id="config" class="text-xl font-bold mb-4">Step 2：プロジェクトの設定</h2>

		<p class="text-gray-700 dark:text-gray-300 mb-6">
			作成したD1データベースをSvelteKitプロジェクトで使えるように設定します。
		</p>

		<!-- wrangler.toml -->
		<div class="mb-8">
			<h3 class="text-lg font-semibold mb-3 flex items-center gap-2">
				<span class="w-7 h-7 bg-blue-500 text-white rounded-full flex items-center justify-center text-sm">1</span>
				wrangler.toml を作成
			</h3>

			<div class="ml-9">
				<div class="p-4 rounded-lg bg-gray-50 dark:bg-gray-800 mb-4">
					<p class="font-semibold text-gray-800 dark:text-gray-200 mb-2">このファイルは何をするの？</p>
					<p class="text-sm text-gray-600 dark:text-gray-400">
						「このプロジェクトはD1データベースを使いますよ」という設定ファイルです。
						プロジェクトのルート（package.jsonと同じ場所）に作成してください。
					</p>
				</div>

				<CodePreview
					title="wrangler.toml（新規作成）"
					description="プロジェクトルートに配置"
					language="toml"
					code={`name = "my-todo-app"
compatibility_date = "2024-01-01"
pages_build_output_dir = ".svelte-kit/cloudflare"

[[d1_databases]]
binding = "DB"
database_name = "my-todo-db"
database_id = "ここにさっきコピーしたIDを貼り付ける"`}
					previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div style="color:#6a9955;"># binding = "DB" がポイント</div><div style="color:#6a9955;"># これでコード内から platform.env.DB でアクセスできる</div></div>`}
				/>

				<div class="mt-4 p-4 rounded-lg bg-amber-50 dark:bg-amber-900/20 border border-amber-200 dark:border-amber-800">
					<p class="font-semibold text-amber-800 dark:text-amber-200 mb-2">binding = "DB" って何？</p>
					<p class="text-sm text-amber-700 dark:text-amber-300">
						これは「データベースに付ける名前」です。
						コードの中で <code class="bg-amber-200 dark:bg-amber-700 px-1 rounded">platform.env.DB</code> と書くと、このデータベースにアクセスできます。
						「DB」以外の名前（例：「TODO_DB」）にしてもOKです。
					</p>
				</div>
			</div>
		</div>

		<!-- アダプター -->
		<div class="mb-8">
			<h3 class="text-lg font-semibold mb-3 flex items-center gap-2">
				<span class="w-7 h-7 bg-blue-500 text-white rounded-full flex items-center justify-center text-sm">2</span>
				Cloudflare用アダプターをインストール
			</h3>

			<div class="ml-9">
				<div class="p-4 rounded-lg bg-gray-50 dark:bg-gray-800 mb-4">
					<p class="font-semibold text-gray-800 dark:text-gray-200 mb-2">アダプターって何？</p>
					<p class="text-sm text-gray-600 dark:text-gray-400">
						SvelteKitは色々な場所（Vercel、Netlify、Cloudflareなど）にデプロイできます。
						「どこにデプロイするか」を決めるのがアダプターです。
						D1を使うには、Cloudflare用のアダプターが必要です。
					</p>
				</div>

				<CodePreview
					title="ターミナルで実行"
					description=""
					language="bash"
					code={`npm install -D @sveltejs/adapter-cloudflare`}
					previewHtml={``}
				/>
			</div>
		</div>

		<!-- svelte.config.js -->
		<div class="mb-8">
			<h3 class="text-lg font-semibold mb-3 flex items-center gap-2">
				<span class="w-7 h-7 bg-blue-500 text-white rounded-full flex items-center justify-center text-sm">3</span>
				svelte.config.js を変更
			</h3>

			<div class="ml-9">
				<CodePreview
					title="svelte.config.js"
					description="既存ファイルを編集"
					language="javascript"
					code={`// 変更前: import adapter from '@sveltejs/adapter-auto';
// 変更後:
import adapter from '@sveltejs/adapter-cloudflare';
import { vitePreprocess } from '@sveltejs/vite-plugin-svelte';

const config = {
  preprocess: vitePreprocess(),
  kit: {
    adapter: adapter()
  }
};

export default config;`}
					previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div style="color:#6a9955;">// adapter-auto → adapter-cloudflare に変更するだけ！</div></div>`}
				/>
			</div>
		</div>

		<!-- app.d.ts -->
		<div class="mb-8">
			<h3 class="text-lg font-semibold mb-3 flex items-center gap-2">
				<span class="w-7 h-7 bg-blue-500 text-white rounded-full flex items-center justify-center text-sm">4</span>
				型定義を追加（TypeScript用）
			</h3>

			<div class="ml-9">
				<div class="p-4 rounded-lg bg-gray-50 dark:bg-gray-800 mb-4">
					<p class="font-semibold text-gray-800 dark:text-gray-200 mb-2">なぜこれが必要？</p>
					<p class="text-sm text-gray-600 dark:text-gray-400">
						TypeScriptに「platform.env.DB というものがありますよ」と教えるためです。
						これがないと、コードを書くときに赤い波線（エラー）が出てしまいます。
					</p>
				</div>

				<CodePreview
					title="src/app.d.ts"
					description="既存ファイルに追加"
					language="typescript"
					code={`declare global {
  namespace App {
    interface Platform {
      env: {
        DB: D1Database;
      };
    }
  }
}

export {};`}
					previewHtml={``}
				/>
			</div>
		</div>
	</section>

	<!-- テーブル作成 -->
	<section class="mb-12">
		<h2 id="create-table" class="text-xl font-bold mb-4">Step 3：テーブルを作成</h2>

		<p class="text-gray-700 dark:text-gray-300 mb-4">
			データベースは作りましたが、まだ中身は空っぽです。
			Todoを保存するための「テーブル（表）」を作りましょう。
		</p>

		<div class="p-4 rounded-lg bg-blue-50 dark:bg-blue-900/20 border border-blue-200 dark:border-blue-800 mb-6">
			<p class="font-semibold text-blue-800 dark:text-blue-200 mb-2">テーブルの設計</p>
			<p class="text-sm text-blue-700 dark:text-blue-300 mb-3">
				Todoには何が必要でしょうか？考えてみましょう。
			</p>
			<div class="bg-white dark:bg-gray-800 rounded p-3 font-mono text-sm">
				<table class="w-full text-left">
					<thead>
						<tr class="border-b border-gray-200 dark:border-gray-600">
							<th class="p-2">カラム名</th>
							<th class="p-2">内容</th>
							<th class="p-2">例</th>
						</tr>
					</thead>
					<tbody class="text-xs">
						<tr class="border-b border-gray-100 dark:border-gray-700">
							<td class="p-2">id</td>
							<td class="p-2">識別用の番号</td>
							<td class="p-2">1, 2, 3...</td>
						</tr>
						<tr class="border-b border-gray-100 dark:border-gray-700">
							<td class="p-2">title</td>
							<td class="p-2">Todoの内容</td>
							<td class="p-2">"牛乳を買う"</td>
						</tr>
						<tr class="border-b border-gray-100 dark:border-gray-700">
							<td class="p-2">completed</td>
							<td class="p-2">完了したかどうか</td>
							<td class="p-2">0（未完了）/ 1（完了）</td>
						</tr>
						<tr>
							<td class="p-2">created_at</td>
							<td class="p-2">作成日時</td>
							<td class="p-2">"2024-01-01 12:00:00"</td>
						</tr>
					</tbody>
				</table>
			</div>
		</div>

		<div class="mb-8">
			<h3 class="text-lg font-semibold mb-3 flex items-center gap-2">
				<span class="w-7 h-7 bg-purple-500 text-white rounded-full flex items-center justify-center text-sm">1</span>
				SQLファイルを作成
			</h3>

			<div class="ml-9">
				<CodePreview
					title="schema.sql（新規作成）"
					description="プロジェクトルートに配置"
					language="sql"
					code={`CREATE TABLE IF NOT EXISTS todos (
  id INTEGER PRIMARY KEY AUTOINCREMENT,
  title TEXT NOT NULL,
  completed INTEGER DEFAULT 0,
  created_at TEXT DEFAULT CURRENT_TIMESTAMP
);`}
					previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div style="color:#6a9955;">-- CREATE TABLE = テーブルを作る</div><div style="color:#6a9955;">-- IF NOT EXISTS = 既にあれば何もしない</div><div style="color:#6a9955;">-- PRIMARY KEY = 主キー（ユニークなID）</div><div style="color:#6a9955;">-- AUTOINCREMENT = 自動で1, 2, 3...と増える</div></div>`}
				/>
			</div>
		</div>

		<div class="mb-8">
			<h3 class="text-lg font-semibold mb-3 flex items-center gap-2">
				<span class="w-7 h-7 bg-purple-500 text-white rounded-full flex items-center justify-center text-sm">2</span>
				テーブルを作成（実行）
			</h3>

			<div class="ml-9">
				<CodePreview
					title="ターミナルで実行"
					description=""
					language="bash"
					code={`wrangler d1 execute my-todo-db --local --file=./schema.sql`}
					previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div style="color:#6a9955;"># --local = ローカル（開発用）のDBに対して実行</div><div style="color:#6a9955;"># --file = このSQLファイルを実行する</div></div>`}
				/>

				<div class="mt-4 p-4 rounded-lg bg-gray-100 dark:bg-gray-800">
					<p class="text-sm text-gray-600 dark:text-gray-400">
						<strong>--local</strong> と <strong>--remote</strong> の違い：<br>
						<code>--local</code> = あなたのパソコン内のテスト用データベース<br>
						<code>--remote</code> = Cloudflare上の本番データベース<br><br>
						開発中は <code>--local</code> を使い、本番公開前に <code>--remote</code> にも実行します。
					</p>
				</div>
			</div>
		</div>
	</section>

	<!-- コードを書く -->
	<section class="mb-12">
		<h2 id="write-code" class="text-xl font-bold mb-4">Step 4：コードを書く</h2>

		<p class="text-gray-700 dark:text-gray-300 mb-6">
			いよいよコードを書いていきます。大きく分けて2つのファイルを作ります。
		</p>

		<div class="grid md:grid-cols-2 gap-4 mb-8">
			<div class="p-4 rounded-lg bg-blue-50 dark:bg-blue-900/20 border border-blue-200 dark:border-blue-800">
				<p class="font-semibold text-blue-800 dark:text-blue-200">+page.server.ts</p>
				<p class="text-sm text-blue-700 dark:text-blue-300">
					サーバー側の処理<br>
					データベースとのやり取りを書く
				</p>
			</div>
			<div class="p-4 rounded-lg bg-green-50 dark:bg-green-900/20 border border-green-200 dark:border-green-800">
				<p class="font-semibold text-green-800 dark:text-green-200">+page.svelte</p>
				<p class="text-sm text-green-700 dark:text-green-300">
					画面（UI）の処理<br>
					ユーザーに見える部分を書く
				</p>
			</div>
		</div>

		<!-- サーバー側 -->
		<div class="mb-10">
			<h3 class="text-lg font-semibold mb-4">+page.server.ts（サーバー側）</h3>

			<div class="p-4 rounded-lg bg-amber-50 dark:bg-amber-900/20 border border-amber-200 dark:border-amber-800 mb-4">
				<p class="font-semibold text-amber-800 dark:text-amber-200 mb-2">このファイルで何をする？</p>
				<p class="text-sm text-amber-700 dark:text-amber-300">
					<strong>1. load関数</strong> = ページを開いたときにTodo一覧を取得<br>
					<strong>2. actions</strong> = ボタンを押したときの処理（追加・完了・削除）
				</p>
			</div>

			<CodePreview
				title="src/routes/+page.server.ts"
				description=""
				language="typescript"
				code={`import { fail } from '@sveltejs/kit';
import type { PageServerLoad, Actions } from './$types';

// ========================================
// ページを開いたとき：Todo一覧を取得する
// ========================================
export const load: PageServerLoad = async ({ platform }) => {
  // D1データベースに接続
  // platform?.env?.DB の「?.」は「存在しなければundefined」という意味
  const db = platform?.env?.DB;

  // D1が使えない場合（npm run devで実行時など）
  if (!db) {
    return { todos: [] };
  }

  // SQLを実行してTodoを取得
  const { results } = await db
    .prepare('SELECT * FROM todos ORDER BY created_at DESC')
    .all();

  // 取得したデータを画面に渡す
  return { todos: results };
};

// ========================================
// ボタンを押したとき：追加・完了・削除
// ========================================
export const actions: Actions = {

  // 「追加」ボタンを押したとき
  create: async ({ request, platform }) => {
    const db = platform?.env?.DB;
    if (!db) return fail(500);

    // フォームから送信されたデータを取得
    const formData = await request.formData();
    const title = formData.get('title') as string;

    // 入力チェック
    if (!title || title.trim() === '') {
      return fail(400, { message: 'タイトルを入力してください' });
    }

    // データベースに追加
    await db
      .prepare('INSERT INTO todos (title) VALUES (?)')
      .bind(title)
      .run();

    return { success: true };
  },

  // 「完了/未完了」ボタンを押したとき
  toggle: async ({ request, platform }) => {
    const db = platform?.env?.DB;
    if (!db) return fail(500);

    const formData = await request.formData();
    const id = formData.get('id');
    const currentStatus = formData.get('completed');

    // 0→1、1→0 に切り替える
    const newStatus = currentStatus === '1' ? 0 : 1;

    await db
      .prepare('UPDATE todos SET completed = ? WHERE id = ?')
      .bind(newStatus, id)
      .run();

    return { success: true };
  },

  // 「削除」ボタンを押したとき
  delete: async ({ request, platform }) => {
    const db = platform?.env?.DB;
    if (!db) return fail(500);

    const formData = await request.formData();
    const id = formData.get('id');

    await db
      .prepare('DELETE FROM todos WHERE id = ?')
      .bind(id)
      .run();

    return { success: true };
  }
};`}
				previewHtml={``}
			/>

			<div class="mt-6 space-y-4">
				<div class="p-4 rounded-lg bg-gray-50 dark:bg-gray-800">
					<p class="font-semibold text-gray-800 dark:text-gray-200 mb-2">prepare()、bind()、run() って何？</p>
					<div class="text-sm text-gray-600 dark:text-gray-400 space-y-2">
						<p><strong>.prepare(SQL文)</strong> = 「このSQLを実行するよ」と準備する</p>
						<p><strong>.bind(値)</strong> = SQLの「?」の部分に値を入れる（安全に）</p>
						<p><strong>.run()</strong> = 実行する（INSERT、UPDATE、DELETE用）</p>
						<p><strong>.all()</strong> = 実行して結果を取得する（SELECT用）</p>
					</div>
				</div>

				<div class="p-4 rounded-lg bg-red-50 dark:bg-red-900/20 border border-red-200 dark:border-red-800">
					<p class="font-semibold text-red-800 dark:text-red-200 mb-2">なぜ bind() を使うの？直接SQLに書いちゃダメ？</p>
					<p class="text-sm text-red-700 dark:text-red-300">
						<strong>セキュリティのためです。</strong><br>
						悪意のあるユーザーが入力欄に特殊な文字を入れて、データベースを壊したり盗んだりすることがあります（SQLインジェクション攻撃）。<br>
						<code>.bind()</code> を使うと、入力された値を安全に処理してくれます。
					</p>
				</div>
			</div>
		</div>

		<!-- 画面側 -->
		<div class="mb-10">
			<h3 class="text-lg font-semibold mb-4">+page.svelte（画面側）</h3>

			<CodePreview
				title="src/routes/+page.svelte"
				description=""
				language="svelte"
				code={`<script lang="ts">
  import { enhance } from '$app/forms';

  // サーバーから受け取ったデータ
  let { data } = $props();
</script>

<div class="max-w-md mx-auto p-4">
  <h1 class="text-2xl font-bold mb-6">Todoリスト</h1>

  <!-- 新しいTodoを追加するフォーム -->
  <form method="POST" action="?/create" use:enhance class="flex gap-2 mb-6">
    <input
      type="text"
      name="title"
      placeholder="新しいタスクを入力..."
      class="flex-1 border rounded px-3 py-2"
    />
    <button class="bg-blue-500 text-white px-4 py-2 rounded">
      追加
    </button>
  </form>

  <!-- Todoの一覧 -->
  <ul class="space-y-2">
    {#each data.todos as todo}
      <li class="flex items-center gap-2 p-3 border rounded">

        <!-- 完了/未完了を切り替えるボタン -->
        <form method="POST" action="?/toggle" use:enhance>
          <input type="hidden" name="id" value={todo.id} />
          <input type="hidden" name="completed" value={todo.completed} />
          <button class="text-xl">
            {todo.completed ? '✅' : '⬜'}
          </button>
        </form>

        <!-- タイトル -->
        <span class="flex-1" class:line-through={todo.completed}>
          {todo.title}
        </span>

        <!-- 削除ボタン -->
        <form method="POST" action="?/delete" use:enhance>
          <input type="hidden" name="id" value={todo.id} />
          <button class="text-red-500">削除</button>
        </form>
      </li>
    {/each}
  </ul>
</div>`}
				previewHtml={``}
			/>

			<div class="mt-6 space-y-4">
				<div class="p-4 rounded-lg bg-gray-50 dark:bg-gray-800">
					<p class="font-semibold text-gray-800 dark:text-gray-200 mb-2">action="?/create" って何？</p>
					<p class="text-sm text-gray-600 dark:text-gray-400">
						フォームを送信したとき、サーバー側の <code>actions</code> のどの関数を呼ぶかを指定しています。<br>
						<code>?/create</code> → <code>actions.create</code> が実行される<br>
						<code>?/toggle</code> → <code>actions.toggle</code> が実行される<br>
						<code>?/delete</code> → <code>actions.delete</code> が実行される
					</p>
				</div>

				<div class="p-4 rounded-lg bg-gray-50 dark:bg-gray-800">
					<p class="font-semibold text-gray-800 dark:text-gray-200 mb-2">use:enhance って何？</p>
					<p class="text-sm text-gray-600 dark:text-gray-400">
						通常、フォームを送信するとページ全体がリロードされます。
						<code>use:enhance</code> を付けると、ページをリロードせずに送信できます。
						より快適な操作感になります。
					</p>
				</div>

				<div class="p-4 rounded-lg bg-gray-50 dark:bg-gray-800">
					<p class="font-semibold text-gray-800 dark:text-gray-200 mb-2">input type="hidden" って何？</p>
					<p class="text-sm text-gray-600 dark:text-gray-400">
						画面には表示されないけど、フォームと一緒に送信されるデータです。
						「どのTodoを削除するか」を伝えるためにIDを送っています。
					</p>
				</div>
			</div>
		</div>
	</section>

	<!-- 動かしてみる -->
	<section class="mb-12">
		<h2 id="run" class="text-xl font-bold mb-4">Step 5：動かしてみる</h2>

		<div class="p-4 rounded-lg bg-red-50 dark:bg-red-900/20 border border-red-200 dark:border-red-800 mb-6">
			<p class="font-semibold text-red-800 dark:text-red-200 mb-2">注意：npm run dev ではD1は動きません！</p>
			<p class="text-sm text-red-700 dark:text-red-300">
				普段使っている <code>npm run dev</code> はViteの開発サーバーです。
				D1を使うには、Cloudflareの環境をシミュレートする必要があります。
			</p>
		</div>

		<div class="mb-6">
			<h3 class="text-lg font-semibold mb-3">package.json にスクリプトを追加</h3>

			<CodePreview
				title="package.json"
				description=""
				language="json"
				code={`{
  "scripts": {
    "dev": "vite dev",
    "dev:d1": "npm run build && wrangler pages dev .svelte-kit/cloudflare",
    "build": "vite build"
  }
}`}
				previewHtml={``}
			/>
		</div>

		<div class="mb-6">
			<h3 class="text-lg font-semibold mb-3">D1を使って開発サーバーを起動</h3>

			<CodePreview
				title="ターミナルで実行"
				description=""
				language="bash"
				code={`npm run dev:d1`}
				previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div style="color:#4ec9b0;">http://localhost:8788 にアクセス！</div></div>`}
			/>
		</div>

		<div class="p-4 rounded-lg bg-green-50 dark:bg-green-900/20 border border-green-200 dark:border-green-800">
			<p class="font-semibold text-green-800 dark:text-green-200 mb-2">使い分け</p>
			<p class="text-sm text-green-700 dark:text-green-300">
				<strong>npm run dev</strong> = 普段の開発（高速、D1使えない）<br>
				<strong>npm run dev:d1</strong> = D1を使う開発（少し遅い、D1使える）<br><br>
				画面のデザインを作るときは <code>npm run dev</code>、データベースの動作確認は <code>npm run dev:d1</code> と使い分けると効率的です。
			</p>
		</div>
	</section>

	<!-- まとめ -->
	<section class="mb-10">
		<h2 id="summary" class="text-xl font-bold mb-4">まとめ</h2>

		<div class="space-y-4">
			<div class="p-4 rounded-lg bg-orange-50 dark:bg-orange-900/20 border border-orange-200 dark:border-orange-800">
				<p class="font-semibold text-orange-800 dark:text-orange-200">D1 = Cloudflareのデータベース</p>
				<p class="text-sm text-orange-700 dark:text-orange-300">
					データを永続的に保存できる。リロードしても消えない。
				</p>
			</div>
			<div class="p-4 rounded-lg bg-blue-50 dark:bg-blue-900/20 border border-blue-200 dark:border-blue-800">
				<p class="font-semibold text-blue-800 dark:text-blue-200">platform.env.DB でアクセス</p>
				<p class="text-sm text-blue-700 dark:text-blue-300">
					+page.server.ts など、サーバー側のコードからのみアクセス可能。
				</p>
			</div>
			<div class="p-4 rounded-lg bg-green-50 dark:bg-green-900/20 border border-green-200 dark:border-green-800">
				<p class="font-semibold text-green-800 dark:text-green-200">.prepare().bind().run() でSQL実行</p>
				<p class="text-sm text-green-700 dark:text-green-300">
					.bind() を使うことでSQLインジェクション攻撃を防げる。
				</p>
			</div>
			<div class="p-4 rounded-lg bg-purple-50 dark:bg-purple-900/20 border border-purple-200 dark:border-purple-800">
				<p class="font-semibold text-purple-800 dark:text-purple-200">開発には wrangler pages dev が必要</p>
				<p class="text-sm text-purple-700 dark:text-purple-300">
					npm run dev ではD1にアクセスできないので注意。
				</p>
			</div>
		</div>
	</section>

	<!-- ナビゲーション -->
	<div class="flex justify-between pt-6 border-t border-gray-200 dark:border-gray-700">
		<a href="/sveltekit/supabase" class="inline-flex items-center gap-2 px-4 py-2 rounded-lg border border-gray-300 dark:border-gray-600 hover:bg-gray-100 dark:hover:bg-gray-800 transition-colors">
			<svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
				<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 19l-7-7 7-7" />
			</svg>
			前へ：Supabase連携
		</a>
		<a href="/sveltekit/libraries" class="inline-flex items-center gap-2 px-4 py-2 rounded-lg bg-primary-600 text-white hover:bg-primary-700 transition-colors">
			次へ：ライブラリ
			<svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
				<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 5l7 7-7 7" />
			</svg>
		</a>
	</div>
</article>
