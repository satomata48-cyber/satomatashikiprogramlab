<script>
	import CodePreview from '$lib/components/CodePreview.svelte';
</script>

<svelte:head>
	<title>Windowsからの移行 - Linux | さとまたラボ</title>
</svelte:head>

<article>
	<h1 class="text-3xl font-bold mb-2">Windowsからの移行</h1>
	<p class="text-lg text-gray-600 dark:text-gray-400 mb-8">
		Windows操作をLinuxコマンドに置き換える方法を学ぼう
	</p>

	<!-- 概要 -->
	<section class="mb-10">
		<h2 id="overview" class="text-xl font-bold mb-4">WindowsとLinuxの違い</h2>

		<div class="p-6 rounded-xl bg-gradient-to-r from-blue-50 to-amber-50 dark:from-blue-900/20 dark:to-amber-900/20 border border-blue-200 dark:border-blue-800 mb-6">
			<div class="flex items-center gap-4 mb-4">
				<span class="text-3xl">🪟</span>
				<span class="text-2xl">→</span>
				<span class="text-3xl">🐧</span>
			</div>
			<p class="text-gray-700 dark:text-gray-300">
				Windowsでマウスで行っていた操作を、Linuxではターミナル（コマンドライン）で行います。最初は慣れが必要ですが、慣れると<strong>圧倒的に高速</strong>に作業できます。
			</p>
		</div>

		<div class="grid grid-cols-1 md:grid-cols-2 gap-4 mb-6">
			<div class="p-4 rounded-lg bg-blue-50 dark:bg-blue-900/20 border border-blue-200 dark:border-blue-800">
				<p class="font-semibold text-blue-800 dark:text-blue-200 mb-2">🪟 Windows</p>
				<ul class="text-sm text-blue-700 dark:text-blue-300 list-disc list-inside space-y-1">
					<li>GUI（グラフィカル）操作が中心</li>
					<li>エクスプローラーでファイル操作</li>
					<li>設定アプリで環境設定</li>
					<li>コマンドプロンプト / PowerShell</li>
				</ul>
			</div>
			<div class="p-4 rounded-lg bg-amber-50 dark:bg-amber-900/20 border border-amber-200 dark:border-amber-800">
				<p class="font-semibold text-amber-800 dark:text-amber-200 mb-2">🐧 Linux</p>
				<ul class="text-sm text-amber-700 dark:text-amber-300 list-disc list-inside space-y-1">
					<li>ターミナル（CLI）操作が中心</li>
					<li>コマンドでファイル操作</li>
					<li>設定ファイルを直接編集</li>
					<li>Bash / Zsh シェル</li>
				</ul>
			</div>
		</div>
	</section>

	<!-- パス表記の違い -->
	<section class="mb-10">
		<h2 id="path" class="text-xl font-bold mb-4">
			<span class="inline-flex items-center justify-center w-8 h-8 bg-orange-500 text-white rounded-full text-sm mr-2">1</span>
			パス表記の置き換え
		</h2>

		<div class="overflow-x-auto mb-6">
			<table class="w-full text-sm">
				<thead>
					<tr class="border-b border-gray-200 dark:border-gray-700">
						<th class="text-left py-3 px-4">項目</th>
						<th class="text-left py-3 px-4">Windows</th>
						<th class="text-left py-3 px-4">Linux</th>
					</tr>
				</thead>
				<tbody>
					<tr class="border-b border-gray-200 dark:border-gray-700">
						<td class="py-3 px-4 font-medium">区切り文字</td>
						<td class="py-3 px-4 font-mono text-blue-600">\（バックスラッシュ）</td>
						<td class="py-3 px-4 font-mono text-orange-600">/（スラッシュ）</td>
					</tr>
					<tr class="border-b border-gray-200 dark:border-gray-700">
						<td class="py-3 px-4 font-medium">ルート</td>
						<td class="py-3 px-4 font-mono text-blue-600">C:\</td>
						<td class="py-3 px-4 font-mono text-orange-600">/</td>
					</tr>
					<tr class="border-b border-gray-200 dark:border-gray-700">
						<td class="py-3 px-4 font-medium">ユーザーフォルダ</td>
						<td class="py-3 px-4 font-mono text-blue-600">C:\Users\username</td>
						<td class="py-3 px-4 font-mono text-orange-600">/home/username または ~</td>
					</tr>
					<tr class="border-b border-gray-200 dark:border-gray-700">
						<td class="py-3 px-4 font-medium">デスクトップ</td>
						<td class="py-3 px-4 font-mono text-blue-600">C:\Users\username\Desktop</td>
						<td class="py-3 px-4 font-mono text-orange-600">~/Desktop</td>
					</tr>
					<tr class="border-b border-gray-200 dark:border-gray-700">
						<td class="py-3 px-4 font-medium">ドキュメント</td>
						<td class="py-3 px-4 font-mono text-blue-600">C:\Users\username\Documents</td>
						<td class="py-3 px-4 font-mono text-orange-600">~/Documents</td>
					</tr>
					<tr class="border-b border-gray-200 dark:border-gray-700">
						<td class="py-3 px-4 font-medium">ダウンロード</td>
						<td class="py-3 px-4 font-mono text-blue-600">C:\Users\username\Downloads</td>
						<td class="py-3 px-4 font-mono text-orange-600">~/Downloads</td>
					</tr>
					<tr>
						<td class="py-3 px-4 font-medium">プログラム</td>
						<td class="py-3 px-4 font-mono text-blue-600">C:\Program Files</td>
						<td class="py-3 px-4 font-mono text-orange-600">/usr/bin, /usr/local/bin</td>
					</tr>
				</tbody>
			</table>
		</div>

		<CodePreview
			title="パスの変換例"
			description="WindowsパスをLinuxパスに"
			language="bash"
			code={`# Windows: C:\\Users\\username\\projects\\my-app
# Linux:   /home/username/projects/my-app
#          または ~/projects/my-app

# プロジェクトフォルダに移動
cd ~/projects/my-app

# ファイルを指定
code ~/projects/my-app/src/index.js`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:12px;"><div style="color:#6a9955;"># Windows</div><div style="color:#569cd6;">C:\\Users\\name\\Desktop</div><div style="margin-top:8px;color:#6a9955;"># Linux</div><div style="color:#ce9178;">~/Desktop</div></div>`}
		/>
	</section>

	<!-- ファイル操作コマンド -->
	<section class="mb-10">
		<h2 id="file-commands" class="text-xl font-bold mb-4">
			<span class="inline-flex items-center justify-center w-8 h-8 bg-orange-500 text-white rounded-full text-sm mr-2">2</span>
			ファイル操作コマンドの置き換え
		</h2>

		<div class="overflow-x-auto mb-6">
			<table class="w-full text-sm">
				<thead>
					<tr class="border-b border-gray-200 dark:border-gray-700">
						<th class="text-left py-3 px-4">操作</th>
						<th class="text-left py-3 px-4">Windows (cmd)</th>
						<th class="text-left py-3 px-4">Linux (bash)</th>
					</tr>
				</thead>
				<tbody>
					<tr class="border-b border-gray-200 dark:border-gray-700">
						<td class="py-3 px-4 font-medium">フォルダ移動</td>
						<td class="py-3 px-4 font-mono text-blue-600">cd folder</td>
						<td class="py-3 px-4 font-mono text-orange-600">cd folder</td>
					</tr>
					<tr class="border-b border-gray-200 dark:border-gray-700">
						<td class="py-3 px-4 font-medium">ファイル一覧</td>
						<td class="py-3 px-4 font-mono text-blue-600">dir</td>
						<td class="py-3 px-4 font-mono text-orange-600">ls</td>
					</tr>
					<tr class="border-b border-gray-200 dark:border-gray-700">
						<td class="py-3 px-4 font-medium">詳細一覧</td>
						<td class="py-3 px-4 font-mono text-blue-600">dir /a</td>
						<td class="py-3 px-4 font-mono text-orange-600">ls -la</td>
					</tr>
					<tr class="border-b border-gray-200 dark:border-gray-700">
						<td class="py-3 px-4 font-medium">現在地表示</td>
						<td class="py-3 px-4 font-mono text-blue-600">cd（引数なし）</td>
						<td class="py-3 px-4 font-mono text-orange-600">pwd</td>
					</tr>
					<tr class="border-b border-gray-200 dark:border-gray-700">
						<td class="py-3 px-4 font-medium">フォルダ作成</td>
						<td class="py-3 px-4 font-mono text-blue-600">mkdir folder</td>
						<td class="py-3 px-4 font-mono text-orange-600">mkdir folder</td>
					</tr>
					<tr class="border-b border-gray-200 dark:border-gray-700">
						<td class="py-3 px-4 font-medium">深いフォルダ作成</td>
						<td class="py-3 px-4 font-mono text-blue-600">mkdir a\b\c</td>
						<td class="py-3 px-4 font-mono text-orange-600">mkdir -p a/b/c</td>
					</tr>
					<tr class="border-b border-gray-200 dark:border-gray-700">
						<td class="py-3 px-4 font-medium">ファイルコピー</td>
						<td class="py-3 px-4 font-mono text-blue-600">copy file.txt dest.txt</td>
						<td class="py-3 px-4 font-mono text-orange-600">cp file.txt dest.txt</td>
					</tr>
					<tr class="border-b border-gray-200 dark:border-gray-700">
						<td class="py-3 px-4 font-medium">フォルダコピー</td>
						<td class="py-3 px-4 font-mono text-blue-600">xcopy /E folder dest</td>
						<td class="py-3 px-4 font-mono text-orange-600">cp -r folder dest</td>
					</tr>
					<tr class="border-b border-gray-200 dark:border-gray-700">
						<td class="py-3 px-4 font-medium">移動/リネーム</td>
						<td class="py-3 px-4 font-mono text-blue-600">move file.txt new.txt</td>
						<td class="py-3 px-4 font-mono text-orange-600">mv file.txt new.txt</td>
					</tr>
					<tr class="border-b border-gray-200 dark:border-gray-700">
						<td class="py-3 px-4 font-medium">ファイル削除</td>
						<td class="py-3 px-4 font-mono text-blue-600">del file.txt</td>
						<td class="py-3 px-4 font-mono text-orange-600">rm file.txt</td>
					</tr>
					<tr class="border-b border-gray-200 dark:border-gray-700">
						<td class="py-3 px-4 font-medium">フォルダ削除</td>
						<td class="py-3 px-4 font-mono text-blue-600">rmdir /S folder</td>
						<td class="py-3 px-4 font-mono text-orange-600">rm -r folder</td>
					</tr>
					<tr class="border-b border-gray-200 dark:border-gray-700">
						<td class="py-3 px-4 font-medium">ファイル内容表示</td>
						<td class="py-3 px-4 font-mono text-blue-600">type file.txt</td>
						<td class="py-3 px-4 font-mono text-orange-600">cat file.txt</td>
					</tr>
					<tr class="border-b border-gray-200 dark:border-gray-700">
						<td class="py-3 px-4 font-medium">画面クリア</td>
						<td class="py-3 px-4 font-mono text-blue-600">cls</td>
						<td class="py-3 px-4 font-mono text-orange-600">clear</td>
					</tr>
					<tr>
						<td class="py-3 px-4 font-medium">ファイル検索</td>
						<td class="py-3 px-4 font-mono text-blue-600">dir /S *.js</td>
						<td class="py-3 px-4 font-mono text-orange-600">find . -name "*.js"</td>
					</tr>
				</tbody>
			</table>
		</div>

		<CodePreview
			title="実践例：プロジェクト作成"
			description="Windowsでの操作をLinuxで"
			language="bash"
			code={`# Windows での操作（コマンドプロンプト）
# cd C:\\Users\\username\\Documents
# mkdir my-project
# cd my-project
# npx sv create .

# Linux での同じ操作
cd ~/Documents
mkdir my-project
cd my-project
npx sv create .

# または一行で
mkdir ~/Documents/my-project && cd ~/Documents/my-project && npx sv create .`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:12px;"><div style="color:#6a9955;">$ mkdir ~/projects/my-app</div><div style="color:#6a9955;">$ cd ~/projects/my-app</div><div style="color:#6a9955;">$ npx sv create .</div><div style="margin-top:8px;color:#4ec9b0;">✓ プロジェクト作成完了</div></div>`}
		/>
	</section>

	<!-- 環境変数 -->
	<section class="mb-10">
		<h2 id="env" class="text-xl font-bold mb-4">
			<span class="inline-flex items-center justify-center w-8 h-8 bg-orange-500 text-white rounded-full text-sm mr-2">3</span>
			環境変数の設定
		</h2>

		<div class="grid grid-cols-1 md:grid-cols-2 gap-4 mb-6">
			<div class="p-4 rounded-lg bg-blue-50 dark:bg-blue-900/20 border border-blue-200 dark:border-blue-800">
				<p class="font-semibold text-blue-800 dark:text-blue-200 mb-3">🪟 Windows</p>
				<div class="text-sm text-blue-700 dark:text-blue-300 space-y-2">
					<p>システムのプロパティ → 環境変数</p>
					<p>または</p>
					<code class="bg-blue-200 dark:bg-blue-800 px-2 py-1 rounded block mt-2 text-xs">set VARIABLE=value</code>
					<code class="bg-blue-200 dark:bg-blue-800 px-2 py-1 rounded block mt-1 text-xs">setx VARIABLE value</code>
				</div>
			</div>
			<div class="p-4 rounded-lg bg-amber-50 dark:bg-amber-900/20 border border-amber-200 dark:border-amber-800">
				<p class="font-semibold text-amber-800 dark:text-amber-200 mb-3">🐧 Linux</p>
				<div class="text-sm text-amber-700 dark:text-amber-300 space-y-2">
					<p>~/.bashrc または ~/.zshrc を編集</p>
					<code class="bg-amber-200 dark:bg-amber-800 px-2 py-1 rounded block mt-2 text-xs">export VARIABLE=value</code>
					<code class="bg-amber-200 dark:bg-amber-800 px-2 py-1 rounded block mt-1 text-xs">source ~/.bashrc</code>
				</div>
			</div>
		</div>

		<CodePreview
			title="環境変数の設定例"
			description=".bashrcに追記して永続化"
			language="bash"
			code={`# 一時的に設定（ターミナルを閉じると消える）
export MY_VAR="hello"
echo $MY_VAR  # hello

# 永続的に設定（.bashrcに追記）
echo 'export MY_VAR="hello"' >> ~/.bashrc

# 設定を反映
source ~/.bashrc

# PATHに追加（例：自作スクリプトフォルダを追加）
export PATH="$HOME/.local/bin:$PATH"

# Node.jsのパスを追加する例
export PATH="$HOME/.nvm/versions/node/v20.10.0/bin:$PATH"

# 環境変数の確認
echo $PATH
echo $HOME
env | grep MY_VAR`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:12px;"><div style="color:#6a9955;">$ export MY_VAR="hello"</div><div style="color:#6a9955;">$ echo $MY_VAR</div><div style="color:#ce9178;">hello</div></div>`}
		/>
	</section>

	<!-- ソフトウェアインストール -->
	<section class="mb-10">
		<h2 id="install" class="text-xl font-bold mb-4">
			<span class="inline-flex items-center justify-center w-8 h-8 bg-orange-500 text-white rounded-full text-sm mr-2">4</span>
			ソフトウェアのインストール
		</h2>

		<div class="p-4 rounded-lg bg-amber-50 dark:bg-amber-900/20 border border-amber-200 dark:border-amber-800 mb-6">
			<p class="font-semibold text-amber-800 dark:text-amber-200 mb-2">Windowsとの違い</p>
			<div class="text-sm text-amber-700 dark:text-amber-300">
				<p>Windowsでは公式サイトから.exeをダウンロードしてインストールしますが、Linuxでは<strong>パッケージマネージャ</strong>を使います。</p>
			</div>
		</div>

		<CodePreview
			title="パッケージマネージャでインストール"
			description="ディストリビューションによって異なる"
			language="bash"
			code={`# Ubuntu / Debian 系
sudo apt update                    # パッケージリストを更新
sudo apt install パッケージ名       # インストール
sudo apt remove パッケージ名        # 削除
sudo apt upgrade                   # 全パッケージを更新

# 例：Git, curl, Node.jsのインストール
sudo apt install git curl

# Node.js（nvmを使う方法がおすすめ）
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.0/install.sh | bash
source ~/.bashrc
nvm install 20
nvm use 20

# Fedora / RHEL 系
sudo dnf install パッケージ名

# Arch Linux
sudo pacman -S パッケージ名`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:12px;"><div style="color:#6a9955;">$ sudo apt install git</div><div style="color:#9cdcfe;">[sudo] password:</div><div style="color:#4ec9b0;">Reading package lists... Done</div><div style="color:#4ec9b0;">Setting up git...</div></div>`}
		/>

		<div class="mt-4 p-4 rounded-lg bg-blue-50 dark:bg-blue-900/20 border border-blue-200 dark:border-blue-800">
			<p class="font-semibold text-blue-800 dark:text-blue-200 mb-2">開発ツールのインストール</p>
			<div class="text-sm text-blue-700 dark:text-blue-300 space-y-2">
				<p><strong>VS Code:</strong> 公式サイトから.debをダウンロードして <code class="bg-blue-200 dark:bg-blue-800 px-1 rounded">sudo dpkg -i code_*.deb</code></p>
				<p><strong>Node.js:</strong> nvmを使うのがおすすめ（バージョン管理が楽）</p>
				<p><strong>Docker:</strong> 公式ドキュメントの手順に従う</p>
			</div>
		</div>
	</section>

	<!-- 権限とsudo -->
	<section class="mb-10">
		<h2 id="sudo" class="text-xl font-bold mb-4">
			<span class="inline-flex items-center justify-center w-8 h-8 bg-orange-500 text-white rounded-full text-sm mr-2">5</span>
			権限とsudo
		</h2>

		<div class="p-4 rounded-lg bg-red-50 dark:bg-red-900/20 border border-red-200 dark:border-red-800 mb-6">
			<p class="font-semibold text-red-800 dark:text-red-200 mb-2">Windowsの「管理者として実行」の代わり</p>
			<div class="text-sm text-red-700 dark:text-red-300">
				<p>Linuxでは <code class="bg-red-200 dark:bg-red-800 px-1 rounded">sudo</code>（スーパーユーザーで実行）を使います。パスワードを聞かれます。</p>
			</div>
		</div>

		<CodePreview
			title="sudoの使い方"
			description="管理者権限が必要な操作"
			language="bash"
			code={`# システム設定の編集
sudo nano /etc/hosts

# パッケージのインストール
sudo apt install nginx

# サービスの操作
sudo systemctl start nginx     # サービス開始
sudo systemctl stop nginx      # サービス停止
sudo systemctl status nginx    # 状態確認
sudo systemctl enable nginx    # 自動起動有効化

# ファイルの所有者変更
sudo chown user:user file.txt

# 権限変更
sudo chmod 755 /var/www/html

# root ユーザーになる（非推奨、必要な時だけ）
sudo su -
# 元に戻る
exit`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:12px;"><div style="color:#6a9955;">$ sudo apt install nginx</div><div style="color:#9cdcfe;">[sudo] password for user:</div><div style="color:#4ec9b0;">Setting up nginx...</div></div>`}
		/>

		<div class="mt-4 p-4 rounded-lg bg-amber-50 dark:bg-amber-900/20 border border-amber-200 dark:border-amber-800">
			<p class="font-semibold text-amber-800 dark:text-amber-200 mb-2">sudoを使うべき場面</p>
			<div class="text-sm text-amber-700 dark:text-amber-300 space-y-1">
				<p>✅ システム全体のソフトウェアインストール</p>
				<p>✅ /etc/ 以下の設定ファイル編集</p>
				<p>✅ systemctlでのサービス管理</p>
				<p>❌ 自分のホームディレクトリ内の操作（不要）</p>
				<p>❌ npm install（通常は不要、グローバルインストール時のみ）</p>
			</div>
		</div>
	</section>

	<!-- ターミナル操作 -->
	<section class="mb-10">
		<h2 id="terminal" class="text-xl font-bold mb-4">
			<span class="inline-flex items-center justify-center w-8 h-8 bg-orange-500 text-white rounded-full text-sm mr-2">6</span>
			ターミナル操作のコツ
		</h2>

		<CodePreview
			title="便利なショートカット"
			description="作業効率を上げるテクニック"
			language="bash"
			code={`# タブ補完（超重要！）
cd Doc[Tab]  # → cd Documents/ に補完される

# 履歴
↑↓キー        # コマンド履歴を移動
Ctrl+R       # 履歴を検索
history      # 履歴一覧を表示

# カーソル移動
Ctrl+A       # 行頭へ移動
Ctrl+E       # 行末へ移動
Ctrl+U       # カーソル前を削除
Ctrl+K       # カーソル後を削除
Ctrl+W       # 単語を削除

# プロセス制御
Ctrl+C       # 実行中のコマンドを中断
Ctrl+Z       # 一時停止（bgで再開、fgで前面に）
Ctrl+D       # 入力終了（exitと同じ）

# 画面
Ctrl+L       # 画面クリア（clearと同じ）
Ctrl+S       # 画面出力を停止
Ctrl+Q       # 画面出力を再開`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:12px;"><div style="color:#6a9955;"># タブ補完の例</div><div style="color:#dcdcaa;">cd Doc</div><span style="color:#569cd6;">[Tab]</span><div style="color:#ce9178;">cd Documents/</div></div>`}
		/>

		<div class="mt-4 p-4 rounded-lg bg-green-50 dark:bg-green-900/20 border border-green-200 dark:border-green-800">
			<p class="font-semibold text-green-800 dark:text-green-200 mb-2">エイリアス設定（よく使うコマンドを短縮）</p>
			<div class="text-sm text-green-700 dark:text-green-300">
				<p class="mb-2">~/.bashrc に追加：</p>
				<code class="bg-green-200 dark:bg-green-800 px-2 py-1 rounded block text-xs">
					alias ll='ls -la'<br>
					alias gs='git status'<br>
					alias gp='git push'<br>
					alias dev='npm run dev'
				</code>
			</div>
		</div>
	</section>

	<!-- 開発環境の移行 -->
	<section class="mb-10">
		<h2 id="dev-env" class="text-xl font-bold mb-4">
			<span class="inline-flex items-center justify-center w-8 h-8 bg-orange-500 text-white rounded-full text-sm mr-2">7</span>
			Web開発環境の構築
		</h2>

		<CodePreview
			title="開発環境セットアップ"
			description="Node.js + Git + VS Code"
			language="bash"
			code={`# 1. システムを更新
sudo apt update && sudo apt upgrade -y

# 2. 基本ツールをインストール
sudo apt install -y git curl wget build-essential

# 3. nvm（Node Version Manager）をインストール
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.0/install.sh | bash
source ~/.bashrc

# 4. Node.jsをインストール
nvm install 20
nvm use 20
node -v  # v20.x.x

# 5. Gitの設定
git config --global user.name "Your Name"
git config --global user.email "your@email.com"

# 6. SSH鍵の作成（GitHub用）
ssh-keygen -t ed25519 -C "your@email.com"
cat ~/.ssh/id_ed25519.pub  # この内容をGitHubに登録

# 7. VS Code（公式サイトから.debをダウンロード後）
sudo dpkg -i code_*.deb

# 8. プロジェクト作成
mkdir -p ~/projects
cd ~/projects
npx sv create my-app
cd my-app
npm install
npm run dev`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:12px;"><div style="color:#4ec9b0;">✓ Node.js v20.10.0</div><div style="color:#4ec9b0;">✓ Git configured</div><div style="color:#4ec9b0;">✓ SSH key generated</div><div style="margin-top:8px;color:#6a9955;">Ready for development!</div></div>`}
		/>
	</section>

	<!-- よくある問題 -->
	<section class="mb-10">
		<h2 id="troubleshoot" class="text-xl font-bold mb-4">よくある問題と解決方法</h2>

		<div class="space-y-4">
			<div class="p-4 rounded-lg bg-gray-50 dark:bg-gray-800/50 border border-gray-200 dark:border-gray-700">
				<p class="font-semibold text-gray-800 dark:text-gray-200 mb-2">❓ "Permission denied" エラー</p>
				<div class="text-sm text-gray-700 dark:text-gray-300">
					<p><strong>原因:</strong> ファイルへのアクセス権限がない</p>
					<p><strong>解決:</strong> <code class="bg-gray-200 dark:bg-gray-700 px-1 rounded">sudo</code> を付けるか、<code class="bg-gray-200 dark:bg-gray-700 px-1 rounded">chmod</code> で権限変更</p>
				</div>
			</div>

			<div class="p-4 rounded-lg bg-gray-50 dark:bg-gray-800/50 border border-gray-200 dark:border-gray-700">
				<p class="font-semibold text-gray-800 dark:text-gray-200 mb-2">❓ "command not found" エラー</p>
				<div class="text-sm text-gray-700 dark:text-gray-300">
					<p><strong>原因:</strong> コマンドがインストールされていない、またはPATHに含まれていない</p>
					<p><strong>解決:</strong> <code class="bg-gray-200 dark:bg-gray-700 px-1 rounded">which コマンド名</code> で確認、なければインストール</p>
				</div>
			</div>

			<div class="p-4 rounded-lg bg-gray-50 dark:bg-gray-800/50 border border-gray-200 dark:border-gray-700">
				<p class="font-semibold text-gray-800 dark:text-gray-200 mb-2">❓ 日本語が文字化けする</p>
				<div class="text-sm text-gray-700 dark:text-gray-300">
					<p><strong>原因:</strong> ロケール設定の問題</p>
					<p><strong>解決:</strong> <code class="bg-gray-200 dark:bg-gray-700 px-1 rounded">export LANG=ja_JP.UTF-8</code> を~/.bashrcに追加</p>
				</div>
			</div>

			<div class="p-4 rounded-lg bg-gray-50 dark:bg-gray-800/50 border border-gray-200 dark:border-gray-700">
				<p class="font-semibold text-gray-800 dark:text-gray-200 mb-2">❓ npm install で EACCES エラー</p>
				<div class="text-sm text-gray-700 dark:text-gray-300">
					<p><strong>原因:</strong> グローバルインストール先の権限問題</p>
					<p><strong>解決:</strong> nvmを使ってNode.jsを管理する（システムのNode.jsを使わない）</p>
				</div>
			</div>
		</div>
	</section>

	<!-- まとめ -->
	<section class="mb-10">
		<h2 id="summary" class="text-xl font-bold mb-4">まとめ：Windows → Linux 対応表</h2>

		<div class="p-4 rounded-lg bg-blue-50 dark:bg-blue-900/20 border border-blue-200 dark:border-blue-800">
			<div class="text-sm text-blue-700 dark:text-blue-300 space-y-2">
				<p><code class="bg-blue-200 dark:bg-blue-800 px-1 rounded">\</code> → <code class="bg-blue-200 dark:bg-blue-800 px-1 rounded">/</code>：パス区切り</p>
				<p><code class="bg-blue-200 dark:bg-blue-800 px-1 rounded">C:\Users\name</code> → <code class="bg-blue-200 dark:bg-blue-800 px-1 rounded">~</code>：ホームディレクトリ</p>
				<p><code class="bg-blue-200 dark:bg-blue-800 px-1 rounded">dir</code> → <code class="bg-blue-200 dark:bg-blue-800 px-1 rounded">ls</code>：ファイル一覧</p>
				<p><code class="bg-blue-200 dark:bg-blue-800 px-1 rounded">copy</code> → <code class="bg-blue-200 dark:bg-blue-800 px-1 rounded">cp</code>：コピー</p>
				<p><code class="bg-blue-200 dark:bg-blue-800 px-1 rounded">move</code> → <code class="bg-blue-200 dark:bg-blue-800 px-1 rounded">mv</code>：移動</p>
				<p><code class="bg-blue-200 dark:bg-blue-800 px-1 rounded">del</code> → <code class="bg-blue-200 dark:bg-blue-800 px-1 rounded">rm</code>：削除</p>
				<p><code class="bg-blue-200 dark:bg-blue-800 px-1 rounded">type</code> → <code class="bg-blue-200 dark:bg-blue-800 px-1 rounded">cat</code>：ファイル表示</p>
				<p><code class="bg-blue-200 dark:bg-blue-800 px-1 rounded">cls</code> → <code class="bg-blue-200 dark:bg-blue-800 px-1 rounded">clear</code>：画面クリア</p>
				<p>管理者実行 → <code class="bg-blue-200 dark:bg-blue-800 px-1 rounded">sudo</code>：特権実行</p>
				<p>.exeインストール → <code class="bg-blue-200 dark:bg-blue-800 px-1 rounded">apt install</code>：パッケージ管理</p>
			</div>
		</div>
	</section>

	<!-- ナビゲーション -->
	<div class="flex justify-between pt-6 border-t border-gray-200 dark:border-gray-700">
		<a href="/linux/folder-structure" class="inline-flex items-center gap-2 px-4 py-2 rounded-lg border border-gray-300 dark:border-gray-600 hover:bg-gray-100 dark:hover:bg-gray-800 transition-colors">
			<svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
				<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 19l-7-7 7-7" />
			</svg>
			前へ：フォルダ構成
		</a>
		<span></span>
	</div>
</article>
