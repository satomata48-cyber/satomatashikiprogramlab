<script>
	import CodePreview from '$lib/components/CodePreview.svelte';
</script>

<svelte:head>
	<title>ブラウザのフォルダ構成 - さとまたプログラミングラボ</title>
	<meta name="description" content="Firefox、Chrome、Chromiumベースブラウザのプロファイルフォルダ構成を詳しく解説" />
</svelte:head>

<div class="max-w-4xl mx-auto">
	<h1 class="text-3xl sm:text-4xl font-bold text-gray-900 dark:text-white mb-6">
		ブラウザのフォルダ構成
	</h1>

	<p class="text-lg text-gray-600 dark:text-gray-300 mb-8">
		ウェブブラウザは、ブックマーク、履歴、拡張機能、パスワードなどのユーザーデータを
		プロファイルフォルダに保存しています。バックアップや移行、トラブルシューティングに必須の知識です。
	</p>

	<!-- Firefox プロファイル -->
	<section class="mb-12">
		<h2 class="text-2xl font-bold text-gray-900 dark:text-white mb-4 flex items-center gap-2">
			<span class="text-orange-500">🦊</span> Firefox プロファイル構成
		</h2>

		<div class="bg-orange-50 dark:bg-orange-900/20 rounded-xl p-6 mb-6">
			<h3 class="font-bold text-orange-700 dark:text-orange-400 mb-3">プロファイルの場所</h3>
			<div class="space-y-2 text-sm">
				<div class="flex flex-col sm:flex-row gap-2">
					<span class="font-medium text-gray-700 dark:text-gray-300 w-20">Linux:</span>
					<code class="bg-orange-100 dark:bg-orange-900/40 px-2 py-1 rounded text-orange-800 dark:text-orange-200">~/.mozilla/firefox/xxxxxxxx.default/</code>
				</div>
				<div class="flex flex-col sm:flex-row gap-2">
					<span class="font-medium text-gray-700 dark:text-gray-300 w-20">Windows:</span>
					<code class="bg-orange-100 dark:bg-orange-900/40 px-2 py-1 rounded text-orange-800 dark:text-orange-200">%APPDATA%\Mozilla\Firefox\Profiles\xxxxxxxx.default\</code>
				</div>
				<div class="flex flex-col sm:flex-row gap-2">
					<span class="font-medium text-gray-700 dark:text-gray-300 w-20">macOS:</span>
					<code class="bg-orange-100 dark:bg-orange-900/40 px-2 py-1 rounded text-orange-800 dark:text-orange-200">~/Library/Application Support/Firefox/Profiles/</code>
				</div>
			</div>
			<p class="text-sm text-orange-600 dark:text-orange-400 mt-3">
				💡 <code>about:profiles</code> でプロファイルの場所を確認できます
			</p>
		</div>

		<h3 class="text-xl font-semibold text-gray-800 dark:text-gray-200 mb-4">重要なファイル一覧</h3>

		<div class="overflow-x-auto mb-6">
			<table class="w-full text-sm">
				<thead class="bg-gray-100 dark:bg-gray-700">
					<tr>
						<th class="px-4 py-3 text-left font-semibold">ファイル/フォルダ</th>
						<th class="px-4 py-3 text-left font-semibold">内容</th>
						<th class="px-4 py-3 text-left font-semibold">重要度</th>
					</tr>
				</thead>
				<tbody class="divide-y divide-gray-200 dark:divide-gray-600">
					<tr class="bg-white dark:bg-gray-800">
						<td class="px-4 py-3 font-mono text-orange-600 dark:text-orange-400">places.sqlite</td>
						<td class="px-4 py-3">ブックマーク・閲覧履歴（SQLiteデータベース）</td>
						<td class="px-4 py-3"><span class="bg-red-100 text-red-800 px-2 py-1 rounded text-xs">最重要</span></td>
					</tr>
					<tr class="bg-gray-50 dark:bg-gray-800/50">
						<td class="px-4 py-3 font-mono text-orange-600 dark:text-orange-400">prefs.js</td>
						<td class="px-4 py-3">ユーザー設定（about:config の内容）</td>
						<td class="px-4 py-3"><span class="bg-red-100 text-red-800 px-2 py-1 rounded text-xs">最重要</span></td>
					</tr>
					<tr class="bg-white dark:bg-gray-800">
						<td class="px-4 py-3 font-mono text-orange-600 dark:text-orange-400">user.js</td>
						<td class="px-4 py-3">カスタム設定（prefs.jsを上書き）</td>
						<td class="px-4 py-3"><span class="bg-yellow-100 text-yellow-800 px-2 py-1 rounded text-xs">重要</span></td>
					</tr>
					<tr class="bg-gray-50 dark:bg-gray-800/50">
						<td class="px-4 py-3 font-mono text-orange-600 dark:text-orange-400">logins.json</td>
						<td class="px-4 py-3">保存されたパスワード（暗号化）</td>
						<td class="px-4 py-3"><span class="bg-red-100 text-red-800 px-2 py-1 rounded text-xs">最重要</span></td>
					</tr>
					<tr class="bg-white dark:bg-gray-800">
						<td class="px-4 py-3 font-mono text-orange-600 dark:text-orange-400">key4.db</td>
						<td class="px-4 py-3">パスワード暗号化キー</td>
						<td class="px-4 py-3"><span class="bg-red-100 text-red-800 px-2 py-1 rounded text-xs">最重要</span></td>
					</tr>
					<tr class="bg-gray-50 dark:bg-gray-800/50">
						<td class="px-4 py-3 font-mono text-orange-600 dark:text-orange-400">extensions/</td>
						<td class="px-4 py-3">インストール済み拡張機能（.xpiファイル）</td>
						<td class="px-4 py-3"><span class="bg-yellow-100 text-yellow-800 px-2 py-1 rounded text-xs">重要</span></td>
					</tr>
					<tr class="bg-white dark:bg-gray-800">
						<td class="px-4 py-3 font-mono text-orange-600 dark:text-orange-400">chrome/</td>
						<td class="px-4 py-3">UIカスタマイズ（userChrome.css）</td>
						<td class="px-4 py-3"><span class="bg-blue-100 text-blue-800 px-2 py-1 rounded text-xs">任意</span></td>
					</tr>
					<tr class="bg-gray-50 dark:bg-gray-800/50">
						<td class="px-4 py-3 font-mono text-orange-600 dark:text-orange-400">bookmarkbackups/</td>
						<td class="px-4 py-3">ブックマークの自動バックアップ</td>
						<td class="px-4 py-3"><span class="bg-yellow-100 text-yellow-800 px-2 py-1 rounded text-xs">重要</span></td>
					</tr>
					<tr class="bg-white dark:bg-gray-800">
						<td class="px-4 py-3 font-mono text-orange-600 dark:text-orange-400">favicons.sqlite</td>
						<td class="px-4 py-3">ブックマークのファビコン</td>
						<td class="px-4 py-3"><span class="bg-gray-100 text-gray-800 px-2 py-1 rounded text-xs">低</span></td>
					</tr>
					<tr class="bg-gray-50 dark:bg-gray-800/50">
						<td class="px-4 py-3 font-mono text-orange-600 dark:text-orange-400">search.json.mozlz4</td>
						<td class="px-4 py-3">検索エンジン設定</td>
						<td class="px-4 py-3"><span class="bg-gray-100 text-gray-800 px-2 py-1 rounded text-xs">低</span></td>
					</tr>
					<tr class="bg-white dark:bg-gray-800">
						<td class="px-4 py-3 font-mono text-orange-600 dark:text-orange-400">containers.json</td>
						<td class="px-4 py-3">コンテナタブの設定</td>
						<td class="px-4 py-3"><span class="bg-gray-100 text-gray-800 px-2 py-1 rounded text-xs">低</span></td>
					</tr>
				</tbody>
			</table>
		</div>

		<CodePreview
			title="Firefox プロファイルのツリー構造"
			code={`~/.mozilla/firefox/xxxxxxxx.default/
├── places.sqlite          # ブックマーク・履歴
├── prefs.js               # ユーザー設定
├── user.js                # カスタム設定（手動作成）
├── logins.json            # 保存されたパスワード
├── key4.db                # 暗号化キー
├── cert9.db               # 証明書データベース
├── cookies.sqlite         # Cookie
├── formhistory.sqlite     # フォーム入力履歴
├── permissions.sqlite     # サイト権限設定
├── content-prefs.sqlite   # サイト別設定
├── favicons.sqlite        # ファビコン
├── search.json.mozlz4     # 検索エンジン
├── handlers.json          # プロトコルハンドラ
├── xulstore.json          # UIレイアウト
├── containers.json        # コンテナタブ
├── extensions/            # 拡張機能
│   ├── {拡張機能ID}.xpi
│   └── ...
├── chrome/                # UIカスタマイズ
│   ├── userChrome.css
│   └── userContent.css
├── bookmarkbackups/       # ブックマークバックアップ
│   └── bookmarks-YYYY-MM-DD.jsonlz4
└── storage/               # 拡張機能のローカルストレージ`}
			language="bash"
		/>
	</section>

	<!-- Chrome/Chromium プロファイル -->
	<section class="mb-12">
		<h2 class="text-2xl font-bold text-gray-900 dark:text-white mb-4 flex items-center gap-2">
			<span class="text-blue-500">🌐</span> Chrome / Chromium プロファイル構成
		</h2>

		<div class="bg-blue-50 dark:bg-blue-900/20 rounded-xl p-6 mb-6">
			<h3 class="font-bold text-blue-700 dark:text-blue-400 mb-3">プロファイルの場所</h3>
			<div class="space-y-2 text-sm">
				<div class="flex flex-col sm:flex-row gap-2">
					<span class="font-medium text-gray-700 dark:text-gray-300 w-24">Linux Chrome:</span>
					<code class="bg-blue-100 dark:bg-blue-900/40 px-2 py-1 rounded text-blue-800 dark:text-blue-200">~/.config/google-chrome/Default/</code>
				</div>
				<div class="flex flex-col sm:flex-row gap-2">
					<span class="font-medium text-gray-700 dark:text-gray-300 w-24">Linux Chromium:</span>
					<code class="bg-blue-100 dark:bg-blue-900/40 px-2 py-1 rounded text-blue-800 dark:text-blue-200">~/.config/chromium/Default/</code>
				</div>
				<div class="flex flex-col sm:flex-row gap-2">
					<span class="font-medium text-gray-700 dark:text-gray-300 w-24">Windows:</span>
					<code class="bg-blue-100 dark:bg-blue-900/40 px-2 py-1 rounded text-blue-800 dark:text-blue-200">%LOCALAPPDATA%\Google\Chrome\User Data\Default\</code>
				</div>
				<div class="flex flex-col sm:flex-row gap-2">
					<span class="font-medium text-gray-700 dark:text-gray-300 w-24">macOS:</span>
					<code class="bg-blue-100 dark:bg-blue-900/40 px-2 py-1 rounded text-blue-800 dark:text-blue-200">~/Library/Application Support/Google/Chrome/Default/</code>
				</div>
			</div>
			<p class="text-sm text-blue-600 dark:text-blue-400 mt-3">
				💡 <code>chrome://version</code> でプロファイルパスを確認できます
			</p>
		</div>

		<h3 class="text-xl font-semibold text-gray-800 dark:text-gray-200 mb-4">重要なファイル一覧</h3>

		<div class="overflow-x-auto mb-6">
			<table class="w-full text-sm">
				<thead class="bg-gray-100 dark:bg-gray-700">
					<tr>
						<th class="px-4 py-3 text-left font-semibold">ファイル/フォルダ</th>
						<th class="px-4 py-3 text-left font-semibold">内容</th>
						<th class="px-4 py-3 text-left font-semibold">形式</th>
					</tr>
				</thead>
				<tbody class="divide-y divide-gray-200 dark:divide-gray-600">
					<tr class="bg-white dark:bg-gray-800">
						<td class="px-4 py-3 font-mono text-blue-600 dark:text-blue-400">Bookmarks</td>
						<td class="px-4 py-3">ブックマーク</td>
						<td class="px-4 py-3"><span class="bg-green-100 text-green-800 px-2 py-1 rounded text-xs">JSON</span></td>
					</tr>
					<tr class="bg-gray-50 dark:bg-gray-800/50">
						<td class="px-4 py-3 font-mono text-blue-600 dark:text-blue-400">History</td>
						<td class="px-4 py-3">閲覧履歴</td>
						<td class="px-4 py-3"><span class="bg-purple-100 text-purple-800 px-2 py-1 rounded text-xs">SQLite</span></td>
					</tr>
					<tr class="bg-white dark:bg-gray-800">
						<td class="px-4 py-3 font-mono text-blue-600 dark:text-blue-400">Preferences</td>
						<td class="px-4 py-3">ブラウザ設定</td>
						<td class="px-4 py-3"><span class="bg-green-100 text-green-800 px-2 py-1 rounded text-xs">JSON</span></td>
					</tr>
					<tr class="bg-gray-50 dark:bg-gray-800/50">
						<td class="px-4 py-3 font-mono text-blue-600 dark:text-blue-400">Login Data</td>
						<td class="px-4 py-3">保存されたパスワード</td>
						<td class="px-4 py-3"><span class="bg-purple-100 text-purple-800 px-2 py-1 rounded text-xs">SQLite</span></td>
					</tr>
					<tr class="bg-white dark:bg-gray-800">
						<td class="px-4 py-3 font-mono text-blue-600 dark:text-blue-400">Cookies</td>
						<td class="px-4 py-3">Cookie</td>
						<td class="px-4 py-3"><span class="bg-purple-100 text-purple-800 px-2 py-1 rounded text-xs">SQLite</span></td>
					</tr>
					<tr class="bg-gray-50 dark:bg-gray-800/50">
						<td class="px-4 py-3 font-mono text-blue-600 dark:text-blue-400">Extensions/</td>
						<td class="px-4 py-3">インストール済み拡張機能</td>
						<td class="px-4 py-3"><span class="bg-gray-100 text-gray-800 px-2 py-1 rounded text-xs">フォルダ</span></td>
					</tr>
					<tr class="bg-white dark:bg-gray-800">
						<td class="px-4 py-3 font-mono text-blue-600 dark:text-blue-400">Local Storage/</td>
						<td class="px-4 py-3">サイトのローカルストレージ</td>
						<td class="px-4 py-3"><span class="bg-gray-100 text-gray-800 px-2 py-1 rounded text-xs">フォルダ</span></td>
					</tr>
					<tr class="bg-gray-50 dark:bg-gray-800/50">
						<td class="px-4 py-3 font-mono text-blue-600 dark:text-blue-400">Web Data</td>
						<td class="px-4 py-3">フォーム自動入力データ</td>
						<td class="px-4 py-3"><span class="bg-purple-100 text-purple-800 px-2 py-1 rounded text-xs">SQLite</span></td>
					</tr>
				</tbody>
			</table>
		</div>

		<CodePreview
			title="Chrome/Chromium プロファイルのツリー構造"
			code={`~/.config/google-chrome/
├── Default/               # デフォルトプロファイル
│   ├── Bookmarks          # ブックマーク（JSON）
│   ├── Bookmarks.bak      # ブックマークバックアップ
│   ├── History            # 閲覧履歴（SQLite）
│   ├── Preferences        # 設定（JSON）
│   ├── Secure Preferences # セキュア設定
│   ├── Login Data         # パスワード（SQLite）
│   ├── Cookies            # Cookie（SQLite）
│   ├── Web Data           # フォームデータ（SQLite）
│   ├── Favicons           # ファビコン（SQLite）
│   ├── Top Sites          # よく見るサイト
│   ├── Shortcuts          # ショートカット
│   ├── Extensions/        # 拡張機能
│   │   └── {拡張機能ID}/
│   │       └── {バージョン}/
│   ├── Local Storage/     # ローカルストレージ
│   ├── Session Storage/   # セッションストレージ
│   ├── IndexedDB/         # IndexedDB
│   └── Cache/             # キャッシュ
├── Profile 1/             # 追加プロファイル
├── Profile 2/
├── Local State            # ブラウザ全体の状態
└── First Run              # 初回起動フラグ`}
			language="bash"
		/>
	</section>

	<!-- Chromiumベースブラウザ -->
	<section class="mb-12">
		<h2 class="text-2xl font-bold text-gray-900 dark:text-white mb-4 flex items-center gap-2">
			<span class="text-purple-500">📂</span> 他のChromiumベースブラウザ
		</h2>

		<p class="text-gray-600 dark:text-gray-300 mb-6">
			Brave、Vivaldi、Edge などのChromiumベースブラウザも同様のフォルダ構成です。
		</p>

		<div class="grid md:grid-cols-2 gap-4 mb-6">
			<div class="bg-orange-50 dark:bg-orange-900/20 rounded-xl p-4">
				<h4 class="font-bold text-orange-700 dark:text-orange-400 mb-2">🦁 Brave (Linux)</h4>
				<code class="text-sm bg-orange-100 dark:bg-orange-900/40 px-2 py-1 rounded block">
					~/.config/BraveSoftware/Brave-Browser/Default/
				</code>
			</div>
			<div class="bg-red-50 dark:bg-red-900/20 rounded-xl p-4">
				<h4 class="font-bold text-red-700 dark:text-red-400 mb-2">🎨 Vivaldi (Linux)</h4>
				<code class="text-sm bg-red-100 dark:bg-red-900/40 px-2 py-1 rounded block">
					~/.config/vivaldi/Default/
				</code>
			</div>
			<div class="bg-blue-50 dark:bg-blue-900/20 rounded-xl p-4">
				<h4 class="font-bold text-blue-700 dark:text-blue-400 mb-2">🌊 Edge (Linux)</h4>
				<code class="text-sm bg-blue-100 dark:bg-blue-900/40 px-2 py-1 rounded block">
					~/.config/microsoft-edge/Default/
				</code>
			</div>
			<div class="bg-cyan-50 dark:bg-cyan-900/20 rounded-xl p-4">
				<h4 class="font-bold text-cyan-700 dark:text-cyan-400 mb-2">⚡ Thorium (Linux)</h4>
				<code class="text-sm bg-cyan-100 dark:bg-cyan-900/40 px-2 py-1 rounded block">
					~/.config/thorium/Default/
				</code>
			</div>
		</div>
	</section>

	<!-- バックアップと移行 -->
	<section class="mb-12">
		<h2 class="text-2xl font-bold text-gray-900 dark:text-white mb-4 flex items-center gap-2">
			<span class="text-green-500">💾</span> バックアップと移行
		</h2>

		<div class="grid md:grid-cols-2 gap-6">
			<div class="bg-green-50 dark:bg-green-900/20 rounded-xl p-6">
				<h3 class="font-bold text-green-700 dark:text-green-400 mb-4">Firefox 最低限バックアップ</h3>
				<ul class="space-y-2 text-sm text-gray-700 dark:text-gray-300">
					<li class="flex items-start gap-2">
						<span class="text-green-500">✓</span>
						<span><code class="bg-green-100 dark:bg-green-900/40 px-1 rounded">places.sqlite</code> - ブックマーク・履歴</span>
					</li>
					<li class="flex items-start gap-2">
						<span class="text-green-500">✓</span>
						<span><code class="bg-green-100 dark:bg-green-900/40 px-1 rounded">prefs.js</code> - 設定</span>
					</li>
					<li class="flex items-start gap-2">
						<span class="text-green-500">✓</span>
						<span><code class="bg-green-100 dark:bg-green-900/40 px-1 rounded">logins.json</code> + <code class="bg-green-100 dark:bg-green-900/40 px-1 rounded">key4.db</code> - パスワード</span>
					</li>
					<li class="flex items-start gap-2">
						<span class="text-green-500">✓</span>
						<span><code class="bg-green-100 dark:bg-green-900/40 px-1 rounded">extensions/</code> - 拡張機能</span>
					</li>
				</ul>
			</div>

			<div class="bg-blue-50 dark:bg-blue-900/20 rounded-xl p-6">
				<h3 class="font-bold text-blue-700 dark:text-blue-400 mb-4">Chrome 最低限バックアップ</h3>
				<ul class="space-y-2 text-sm text-gray-700 dark:text-gray-300">
					<li class="flex items-start gap-2">
						<span class="text-blue-500">✓</span>
						<span><code class="bg-blue-100 dark:bg-blue-900/40 px-1 rounded">Bookmarks</code> - ブックマーク</span>
					</li>
					<li class="flex items-start gap-2">
						<span class="text-blue-500">✓</span>
						<span><code class="bg-blue-100 dark:bg-blue-900/40 px-1 rounded">Preferences</code> - 設定</span>
					</li>
					<li class="flex items-start gap-2">
						<span class="text-blue-500">✓</span>
						<span><code class="bg-blue-100 dark:bg-blue-900/40 px-1 rounded">Login Data</code> - パスワード</span>
					</li>
					<li class="flex items-start gap-2">
						<span class="text-blue-500">✓</span>
						<span><code class="bg-blue-100 dark:bg-blue-900/40 px-1 rounded">Extensions/</code> - 拡張機能</span>
					</li>
				</ul>
			</div>
		</div>

		<div class="mt-6 bg-yellow-50 dark:bg-yellow-900/20 border border-yellow-200 dark:border-yellow-800 rounded-xl p-4">
			<h4 class="font-bold text-yellow-700 dark:text-yellow-400 mb-2">⚠️ 注意事項</h4>
			<ul class="text-sm text-yellow-800 dark:text-yellow-200 space-y-1">
				<li>• ブラウザを閉じた状態でバックアップを取ること</li>
				<li>• パスワードファイルは暗号化されており、同じOSアカウントでないと復元できない場合がある</li>
				<li>• Cookieには有効期限があり、復元しても再ログインが必要な場合が多い</li>
			</ul>
		</div>
	</section>

	<!-- コマンドラインでの操作 -->
	<section class="mb-12">
		<h2 class="text-2xl font-bold text-gray-900 dark:text-white mb-4 flex items-center gap-2">
			<span class="text-gray-500">💻</span> コマンドラインでの操作
		</h2>

		<CodePreview
			title="Firefox プロファイルのバックアップ"
			code={`# プロファイル一覧を確認
ls ~/.mozilla/firefox/

# プロファイルをバックアップ
cp -r ~/.mozilla/firefox/xxxxxxxx.default ~/firefox-backup

# 特定のファイルだけバックアップ
mkdir ~/firefox-essential-backup
cp ~/.mozilla/firefox/xxxxxxxx.default/places.sqlite ~/firefox-essential-backup/
cp ~/.mozilla/firefox/xxxxxxxx.default/prefs.js ~/firefox-essential-backup/
cp ~/.mozilla/firefox/xxxxxxxx.default/logins.json ~/firefox-essential-backup/
cp ~/.mozilla/firefox/xxxxxxxx.default/key4.db ~/firefox-essential-backup/`}
			language="bash"
		/>

		<CodePreview
			title="Chrome プロファイルのバックアップ"
			code={`# プロファイルの場所を確認
ls ~/.config/google-chrome/

# Defaultプロファイルをバックアップ
cp -r ~/.config/google-chrome/Default ~/chrome-backup

# ブックマークだけエクスポート（JSONなので可読）
cp ~/.config/google-chrome/Default/Bookmarks ~/chrome-bookmarks.json

# 読みやすく整形
cat ~/chrome-bookmarks.json | python3 -m json.tool > ~/bookmarks-formatted.json`}
			language="bash"
		/>

		<CodePreview
			title="カスタムプロファイルでブラウザを起動"
			code={`# Firefox: 特定のプロファイルで起動
firefox -P "プロファイル名"

# Firefox: プロファイルマネージャーを開く
firefox -ProfileManager

# Chrome: 別のユーザーデータディレクトリで起動
google-chrome --user-data-dir=/path/to/custom/profile

# Chrome: シークレットモードで起動
google-chrome --incognito`}
			language="bash"
		/>
	</section>

	<!-- まとめ -->
	<section class="mb-12">
		<h2 class="text-2xl font-bold text-gray-900 dark:text-white mb-4">まとめ</h2>

		<div class="bg-gradient-to-r from-purple-50 to-blue-50 dark:from-purple-900/20 dark:to-blue-900/20 rounded-xl p-6">
			<div class="grid md:grid-cols-2 gap-6">
				<div>
					<h3 class="font-bold text-purple-700 dark:text-purple-400 mb-3">Firefox の特徴</h3>
					<ul class="space-y-2 text-sm text-gray-700 dark:text-gray-300">
						<li>• SQLite形式のデータベースファイルが多い</li>
						<li>• <code>about:profiles</code> で管理が簡単</li>
						<li>• <code>user.js</code> でカスタム設定を永続化</li>
						<li>• <code>userChrome.css</code> でUIをカスタマイズ可能</li>
					</ul>
				</div>
				<div>
					<h3 class="font-bold text-blue-700 dark:text-blue-400 mb-3">Chrome の特徴</h3>
					<ul class="space-y-2 text-sm text-gray-700 dark:text-gray-300">
						<li>• BookmarksはJSON形式で可読性が高い</li>
						<li>• <code>chrome://version</code> でパスを確認</li>
						<li>• 複数プロファイルは Profile 1, 2... で管理</li>
						<li>• Googleアカウントで同期が簡単</li>
					</ul>
				</div>
			</div>
		</div>
	</section>
</div>
