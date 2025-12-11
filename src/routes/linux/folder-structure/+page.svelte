<script>
	import CodePreview from '$lib/components/CodePreview.svelte';
</script>

<svelte:head>
	<title>フォルダ構成 - Linux | さとまたラボ</title>
</svelte:head>

<article>
	<h1 class="text-3xl font-bold mb-2">Linuxのフォルダ構成</h1>
	<p class="text-lg text-gray-600 dark:text-gray-400 mb-8">
		Linuxのディレクトリ構造を理解して、ファイル操作をマスターしよう
	</p>

	<!-- 概要 -->
	<section class="mb-10">
		<h2 id="overview" class="text-xl font-bold mb-4">Linuxのディレクトリ構造</h2>

		<div class="p-6 rounded-xl bg-gradient-to-r from-amber-50 to-green-50 dark:from-amber-900/20 dark:to-green-900/20 border border-amber-200 dark:border-amber-800 mb-6">
			<div class="flex items-center gap-4 mb-4">
				<span class="text-3xl">🐧</span>
				<span class="text-2xl">+</span>
				<span class="text-3xl">📁</span>
			</div>
			<p class="text-gray-700 dark:text-gray-300">
				Linuxでは全てが<strong>「/」（ルート）</strong>から始まる階層構造になっています。Windowsのように「C:」「D:」というドライブ文字は使いません。
			</p>
		</div>

		<div class="p-4 rounded-lg bg-blue-50 dark:bg-blue-900/20 border border-blue-200 dark:border-blue-800 mb-6">
			<p class="font-semibold text-blue-800 dark:text-blue-200 mb-2">WindowsとLinuxの違い</p>
			<div class="text-sm text-blue-700 dark:text-blue-300 space-y-2">
				<div class="grid grid-cols-2 gap-4">
					<div>
						<p class="font-medium">Windows</p>
						<code class="bg-blue-200 dark:bg-blue-800 px-2 py-1 rounded text-xs">C:\Users\username\Desktop</code>
					</div>
					<div>
						<p class="font-medium">Linux</p>
						<code class="bg-blue-200 dark:bg-blue-800 px-2 py-1 rounded text-xs">/home/username/Desktop</code>
					</div>
				</div>
				<p class="mt-2">パス区切りが <code class="bg-blue-200 dark:bg-blue-800 px-1 rounded">\</code>（バックスラッシュ）ではなく <code class="bg-blue-200 dark:bg-blue-800 px-1 rounded">/</code>（スラッシュ）です。</p>
			</div>
		</div>
	</section>

	<!-- ルートディレクトリ構造 -->
	<section class="mb-10">
		<h2 id="root" class="text-xl font-bold mb-4">ルートディレクトリ（/）の構成</h2>

		<CodePreview
			title="Linuxのディレクトリ構造"
			description="主要なディレクトリとその役割"
			language="text"
			code={`/                       ← ルートディレクトリ（全ての起点）
├── bin/                ← 基本コマンド（ls, cp, mvなど）
├── boot/               ← 起動に必要なファイル
├── dev/                ← デバイスファイル（ハードウェア）
├── etc/                ← システム設定ファイル（重要！）
├── home/               ← ユーザーのホームディレクトリ（重要！）
│   └── username/       ← あなたのファイルはここ
│       ├── Desktop/
│       ├── Documents/
│       ├── Downloads/
│       └── .config/    ← アプリの設定（隠しフォルダ）
├── lib/                ← 共有ライブラリ
├── media/              ← USBやCDなどの自動マウント先
├── mnt/                ← 手動マウント用
├── opt/                ← 追加ソフトウェア
├── proc/               ← プロセス情報（仮想ファイルシステム）
├── root/               ← rootユーザーのホーム
├── sbin/               ← システム管理コマンド
├── srv/                ← サーバー用データ
├── sys/                ← システム情報（仮想ファイルシステム）
├── tmp/                ← 一時ファイル（再起動で消える）
├── usr/                ← ユーザー用プログラム
│   ├── bin/            ← ユーザーコマンド
│   ├── lib/            ← ライブラリ
│   ├── local/          ← 手動インストールしたソフト
│   └── share/          ← 共有データ
└── var/                ← 変動データ（ログなど）
    └── log/            ← システムログ`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:12px;"><div style="color:#6a9955;"># よく使うディレクトリ</div><div style="color:#569cd6;">/home/username/</div><div style="margin-left:8px;color:#9cdcfe;">あなたのファイル</div><div style="color:#569cd6;">/etc/</div><div style="margin-left:8px;color:#9cdcfe;">設定ファイル</div><div style="color:#569cd6;">/var/log/</div><div style="margin-left:8px;color:#9cdcfe;">ログファイル</div></div>`}
		/>
	</section>

	<!-- 重要なディレクトリ詳細 -->
	<section class="mb-10">
		<h2 id="important" class="text-xl font-bold mb-4">開発者が知っておくべきディレクトリ</h2>

		<div class="space-y-4">
			<!-- /home -->
			<div class="p-4 rounded-lg bg-green-50 dark:bg-green-900/20 border border-green-200 dark:border-green-800">
				<p class="font-semibold text-green-800 dark:text-green-200 mb-2">📁 /home/username/ - ホームディレクトリ</p>
				<div class="text-sm text-green-700 dark:text-green-300 space-y-2">
					<p>あなたの全てのファイルが置かれる場所。Windowsの <code class="bg-green-200 dark:bg-green-800 px-1 rounded">C:\Users\username</code> に相当。</p>
					<ul class="list-disc list-inside ml-2 space-y-1">
						<li><code class="bg-green-200 dark:bg-green-800 px-1 rounded">~</code> や <code class="bg-green-200 dark:bg-green-800 px-1 rounded">$HOME</code> で参照可能</li>
						<li>プロジェクトは通常ここに作成</li>
						<li><code class="bg-green-200 dark:bg-green-800 px-1 rounded">.</code>で始まるファイルは隠しファイル</li>
					</ul>
				</div>
			</div>

			<!-- /etc -->
			<div class="p-4 rounded-lg bg-amber-50 dark:bg-amber-900/20 border border-amber-200 dark:border-amber-800">
				<p class="font-semibold text-amber-800 dark:text-amber-200 mb-2">⚙️ /etc/ - システム設定</p>
				<div class="text-sm text-amber-700 dark:text-amber-300 space-y-2">
					<p>システム全体の設定ファイルが置かれる場所。</p>
					<ul class="list-disc list-inside ml-2 space-y-1">
						<li><code class="bg-amber-200 dark:bg-amber-800 px-1 rounded">/etc/hosts</code> - ホスト名解決</li>
						<li><code class="bg-amber-200 dark:bg-amber-800 px-1 rounded">/etc/nginx/</code> - Nginx設定</li>
						<li><code class="bg-amber-200 dark:bg-amber-800 px-1 rounded">/etc/ssh/</code> - SSH設定</li>
						<li>編集には通常 <code class="bg-amber-200 dark:bg-amber-800 px-1 rounded">sudo</code> が必要</li>
					</ul>
				</div>
			</div>

			<!-- /usr/local -->
			<div class="p-4 rounded-lg bg-purple-50 dark:bg-purple-900/20 border border-purple-200 dark:border-purple-800">
				<p class="font-semibold text-purple-800 dark:text-purple-200 mb-2">📦 /usr/local/ - 手動インストール先</p>
				<div class="text-sm text-purple-700 dark:text-purple-300 space-y-2">
					<p>パッケージマネージャを使わずに手動でインストールしたソフトウェアの場所。</p>
					<ul class="list-disc list-inside ml-2 space-y-1">
						<li><code class="bg-purple-200 dark:bg-purple-800 px-1 rounded">/usr/local/bin/</code> - 実行ファイル</li>
						<li><code class="bg-purple-200 dark:bg-purple-800 px-1 rounded">/usr/local/lib/</code> - ライブラリ</li>
						<li>Node.jsのグローバルパッケージもここに入ることがある</li>
					</ul>
				</div>
			</div>

			<!-- /var -->
			<div class="p-4 rounded-lg bg-blue-50 dark:bg-blue-900/20 border border-blue-200 dark:border-blue-800">
				<p class="font-semibold text-blue-800 dark:text-blue-200 mb-2">📝 /var/ - 変動データ</p>
				<div class="text-sm text-blue-700 dark:text-blue-300 space-y-2">
					<p>ログファイルやキャッシュなど、変動するデータの場所。</p>
					<ul class="list-disc list-inside ml-2 space-y-1">
						<li><code class="bg-blue-200 dark:bg-blue-800 px-1 rounded">/var/log/</code> - システムログ</li>
						<li><code class="bg-blue-200 dark:bg-blue-800 px-1 rounded">/var/www/</code> - Webサーバーのドキュメントルート</li>
						<li><code class="bg-blue-200 dark:bg-blue-800 px-1 rounded">/var/cache/</code> - キャッシュファイル</li>
					</ul>
				</div>
			</div>

			<!-- /tmp -->
			<div class="p-4 rounded-lg bg-red-50 dark:bg-red-900/20 border border-red-200 dark:border-red-800">
				<p class="font-semibold text-red-800 dark:text-red-200 mb-2">🗑️ /tmp/ - 一時ファイル</p>
				<div class="text-sm text-red-700 dark:text-red-300 space-y-2">
					<p>一時的なファイルを置く場所。再起動すると消えるので重要なファイルは置かない！</p>
					<ul class="list-disc list-inside ml-2 space-y-1">
						<li>全ユーザーが書き込み可能</li>
						<li>スクリプトの一時データに便利</li>
						<li>自動削除されるので片付け不要</li>
					</ul>
				</div>
			</div>
		</div>
	</section>

	<!-- 隠しファイル -->
	<section class="mb-10">
		<h2 id="hidden" class="text-xl font-bold mb-4">隠しファイルとドットファイル</h2>

		<CodePreview
			title="ホームディレクトリの隠しファイル"
			description=".(ドット)で始まるファイルは隠しファイル"
			language="bash"
			code={`# 隠しファイルを含めて表示
ls -la ~

# よくある隠しファイル/フォルダ
/home/username/
├── .bashrc           ← Bashの設定（重要！）
├── .zshrc            ← Zshの設定
├── .profile          ← ログイン時の設定
├── .gitconfig        ← Gitの設定
├── .ssh/             ← SSH鍵（重要！）
│   ├── id_rsa        ← 秘密鍵（絶対に公開しない！）
│   ├── id_rsa.pub    ← 公開鍵
│   └── known_hosts   ← 接続したことのあるホスト
├── .config/          ← アプリの設定
│   ├── Code/         ← VS Codeの設定
│   └── nvim/         ← Neovimの設定
├── .local/           ← ユーザーローカルデータ
│   └── bin/          ← ユーザーの実行ファイル
├── .npm/             ← npmのキャッシュ
├── .nvm/             ← Node Version Manager
└── .cache/           ← キャッシュデータ`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:12px;"><div style="color:#6a9955;"># 隠しファイルを見る</div><div style="color:#dcdcaa;">ls -la</div><div style="margin-top:8px;color:#9cdcfe;">drwxr-xr-x  .config</div><div style="color:#9cdcfe;">drwx------  .ssh</div><div style="color:#9cdcfe;">-rw-r--r--  .bashrc</div></div>`}
		/>

		<div class="mt-4 p-4 rounded-lg bg-amber-50 dark:bg-amber-900/20 border border-amber-200 dark:border-amber-800">
			<p class="font-semibold text-amber-800 dark:text-amber-200 mb-2">重要なドットファイル</p>
			<div class="text-sm text-amber-700 dark:text-amber-300 space-y-2">
				<p><code class="bg-amber-200 dark:bg-amber-800 px-1 rounded">.bashrc</code>：ターミナル起動時に読み込まれる設定。環境変数やエイリアスを定義。</p>
				<p><code class="bg-amber-200 dark:bg-amber-800 px-1 rounded">.ssh/</code>：SSH鍵の保管場所。権限を正しく設定しないと動かない。</p>
				<p><code class="bg-amber-200 dark:bg-amber-800 px-1 rounded">.gitconfig</code>：Gitのユーザー名やメールアドレスを設定。</p>
			</div>
		</div>
	</section>

	<!-- パス操作 -->
	<section class="mb-10">
		<h2 id="path" class="text-xl font-bold mb-4">パスの操作</h2>

		<CodePreview
			title="パスの表記方法"
			description="絶対パスと相対パス"
			language="bash"
			code={`# 絶対パス（/から始まる完全なパス）
cd /home/username/projects/my-app

# 相対パス（現在地からの相対位置）
cd projects/my-app      # 現在地から「projects/my-app」へ
cd ..                   # 一つ上のディレクトリへ
cd ../..                # 二つ上のディレクトリへ
cd ./src                # 現在地の「src」フォルダへ（./は省略可能）

# 特殊なパス表記
cd ~                    # ホームディレクトリへ（/home/username）
cd ~/projects           # ホームのprojectsフォルダへ
cd -                    # 直前にいたディレクトリへ戻る

# 現在地を確認
pwd                     # /home/username/projects/my-app`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:12px;"><div style="color:#6a9955;">$ pwd</div><div style="color:#ce9178;">/home/username/projects</div><div style="margin-top:8px;color:#6a9955;">$ cd my-app</div><div style="color:#6a9955;">$ pwd</div><div style="color:#ce9178;">/home/username/projects/my-app</div></div>`}
		/>

		<div class="mt-4 grid grid-cols-1 md:grid-cols-2 gap-4">
			<div class="p-4 rounded-lg bg-gray-50 dark:bg-gray-800/50 border border-gray-200 dark:border-gray-700">
				<p class="font-semibold text-gray-800 dark:text-gray-200 mb-2">パス記号の意味</p>
				<div class="text-sm text-gray-700 dark:text-gray-300 space-y-1">
					<p><code class="bg-gray-200 dark:bg-gray-700 px-1 rounded">/</code>：ルートまたはパス区切り</p>
					<p><code class="bg-gray-200 dark:bg-gray-700 px-1 rounded">~</code>：ホームディレクトリ</p>
					<p><code class="bg-gray-200 dark:bg-gray-700 px-1 rounded">.</code>：現在のディレクトリ</p>
					<p><code class="bg-gray-200 dark:bg-gray-700 px-1 rounded">..</code>：親ディレクトリ</p>
				</div>
			</div>
			<div class="p-4 rounded-lg bg-gray-50 dark:bg-gray-800/50 border border-gray-200 dark:border-gray-700">
				<p class="font-semibold text-gray-800 dark:text-gray-200 mb-2">環境変数</p>
				<div class="text-sm text-gray-700 dark:text-gray-300 space-y-1">
					<p><code class="bg-gray-200 dark:bg-gray-700 px-1 rounded">$HOME</code>：ホームディレクトリ</p>
					<p><code class="bg-gray-200 dark:bg-gray-700 px-1 rounded">$PWD</code>：現在のディレクトリ</p>
					<p><code class="bg-gray-200 dark:bg-gray-700 px-1 rounded">$PATH</code>：コマンド検索パス</p>
					<p><code class="bg-gray-200 dark:bg-gray-700 px-1 rounded">$USER</code>：ユーザー名</p>
				</div>
			</div>
		</div>
	</section>

	<!-- ファイル操作コマンド -->
	<section class="mb-10">
		<h2 id="commands" class="text-xl font-bold mb-4">基本的なファイル操作コマンド</h2>

		<CodePreview
			title="ファイル・ディレクトリ操作"
			description="よく使うコマンド"
			language="bash"
			code={`# ディレクトリ操作
mkdir my-folder              # フォルダ作成
mkdir -p a/b/c               # 深い階層を一度に作成
rmdir my-folder              # 空のフォルダを削除

# ファイル操作
touch file.txt               # 空ファイル作成
cp file.txt copy.txt         # コピー
cp -r folder/ backup/        # フォルダをコピー（-r: 再帰的）
mv file.txt newname.txt      # 移動・リネーム
rm file.txt                  # ファイル削除
rm -r folder/                # フォルダ削除（-r: 再帰的）
rm -rf folder/               # 強制削除（確認なし、危険！）

# ファイル内容表示
cat file.txt                 # 全内容を表示
head -n 10 file.txt          # 先頭10行を表示
tail -n 10 file.txt          # 末尾10行を表示
tail -f log.txt              # リアルタイムで末尾を監視
less file.txt                # ページャーで表示（qで終了）

# 検索
find . -name "*.js"          # 現在地以下の.jsファイルを検索
grep "keyword" file.txt      # ファイル内のキーワード検索
grep -r "keyword" ./         # フォルダ内を再帰検索`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:12px;"><div style="color:#6a9955;">$ mkdir -p projects/my-app</div><div style="color:#6a9955;">$ cd projects/my-app</div><div style="color:#6a9955;">$ touch index.js</div><div style="color:#6a9955;">$ ls</div><div style="color:#ce9178;">index.js</div></div>`}
		/>

		<div class="mt-4 p-4 rounded-lg bg-red-50 dark:bg-red-900/20 border border-red-200 dark:border-red-800">
			<p class="font-semibold text-red-800 dark:text-red-200 mb-2">危険なコマンドに注意！</p>
			<div class="text-sm text-red-700 dark:text-red-300 space-y-2">
				<p><code class="bg-red-200 dark:bg-red-800 px-1 rounded">rm -rf /</code>：システム全体を削除（絶対に実行しない！）</p>
				<p><code class="bg-red-200 dark:bg-red-800 px-1 rounded">rm -rf</code>は確認なしで削除されるので、パスを必ず確認してから実行してください。</p>
			</div>
		</div>
	</section>

	<!-- 権限 -->
	<section class="mb-10">
		<h2 id="permissions" class="text-xl font-bold mb-4">ファイル権限（パーミッション）</h2>

		<CodePreview
			title="権限の確認と変更"
			description="ls -lで権限を確認"
			language="bash"
			code={`# 権限を確認
ls -l
# -rw-r--r-- 1 user group 1234 Jan 1 12:00 file.txt
# drwxr-xr-x 2 user group 4096 Jan 1 12:00 folder/

# 権限の読み方（10文字）
# d rwx r-x r-x
# │ └─┬─┘└─┬─┘└─┬─┘
# │   │    │    └── その他ユーザーの権限
# │   │    └─────── グループの権限
# │   └──────────── 所有者の権限
# └──────────────── d=ディレクトリ, -=ファイル, l=シンボリックリンク

# r=read(読み取り), w=write(書き込み), x=execute(実行)

# 権限を変更
chmod 755 script.sh          # rwxr-xr-x（実行可能にする）
chmod 644 file.txt           # rw-r--r--（一般的なファイル）
chmod +x script.sh           # 実行権限を追加
chmod -w file.txt            # 書き込み権限を削除

# 所有者を変更
chown user:group file.txt    # 所有者とグループを変更
sudo chown root file.txt     # rootに変更（sudo必要）`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:12px;"><div style="color:#6a9955;">$ ls -l</div><div style="color:#569cd6;">-rw-r--r--</div><span style="color:#9cdcfe;"> user user file.txt</span><div style="color:#569cd6;">drwxr-xr-x</div><span style="color:#9cdcfe;"> user user folder/</span></div>`}
		/>

		<div class="mt-4 p-4 rounded-lg bg-gray-50 dark:bg-gray-800/50 border border-gray-200 dark:border-gray-700">
			<p class="font-semibold text-gray-800 dark:text-gray-200 mb-3">よく使う権限の数字</p>
			<div class="text-sm text-gray-700 dark:text-gray-300">
				<div class="grid grid-cols-2 md:grid-cols-4 gap-2">
					<div><code class="text-orange-600">755</code>：実行ファイル</div>
					<div><code class="text-orange-600">644</code>：通常ファイル</div>
					<div><code class="text-orange-600">700</code>：プライベート</div>
					<div><code class="text-orange-600">600</code>：SSH鍵など</div>
				</div>
				<p class="mt-3 text-xs text-gray-500 dark:text-gray-400">
					計算方法：r=4, w=2, x=1 の合計。例：rwx=7, rw-=6, r-x=5, r--=4
				</p>
			</div>
		</div>
	</section>

	<!-- 開発者向けフォルダ構成 -->
	<section class="mb-10">
		<h2 id="dev-structure" class="text-xl font-bold mb-4">開発プロジェクトの配置</h2>

		<CodePreview
			title="おすすめのプロジェクト配置"
			description="ホームディレクトリでの整理方法"
			language="text"
			code={`/home/username/
├── projects/                    ← 開発プロジェクトをまとめる
│   ├── work/                    ← 仕事関連
│   │   ├── client-a/
│   │   └── client-b/
│   ├── personal/                ← 個人プロジェクト
│   │   ├── my-blog/
│   │   └── portfolio/
│   └── learning/                ← 学習用
│       ├── typescript-practice/
│       └── sveltekit-tutorial/
│
├── .local/
│   └── bin/                     ← 自作スクリプトを置く
│
└── .config/                     ← エディタやツールの設定`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:12px;"><div style="color:#6a9955;"># プロジェクト作成の例</div><div style="color:#dcdcaa;">mkdir -p ~/projects/personal</div><div style="color:#dcdcaa;">cd ~/projects/personal</div><div style="color:#dcdcaa;">npx sv create my-app</div></div>`}
		/>
	</section>

	<!-- まとめ -->
	<section class="mb-10">
		<h2 id="summary" class="text-xl font-bold mb-4">まとめ</h2>

		<div class="p-4 rounded-lg bg-blue-50 dark:bg-blue-900/20 border border-blue-200 dark:border-blue-800">
			<ul class="text-sm text-blue-700 dark:text-blue-300 list-disc list-inside space-y-2">
				<li>Linuxは全て<code class="bg-blue-200 dark:bg-blue-800 px-1 rounded">/</code>（ルート）から始まる階層構造</li>
				<li>ホームディレクトリは<code class="bg-blue-200 dark:bg-blue-800 px-1 rounded">/home/username/</code>または<code class="bg-blue-200 dark:bg-blue-800 px-1 rounded">~</code></li>
				<li>パス区切りは<code class="bg-blue-200 dark:bg-blue-800 px-1 rounded">/</code>（スラッシュ）</li>
				<li><code class="bg-blue-200 dark:bg-blue-800 px-1 rounded">.</code>で始まるファイルは隠しファイル</li>
				<li>権限（パーミッション）を理解して適切に設定する</li>
				<li>プロジェクトは<code class="bg-blue-200 dark:bg-blue-800 px-1 rounded">~/projects/</code>にまとめると管理しやすい</li>
			</ul>
		</div>
	</section>

	<!-- ナビゲーション -->
	<div class="flex justify-between pt-6 border-t border-gray-200 dark:border-gray-700">
		<span></span>
		<a href="/linux/switch-from-windows" class="inline-flex items-center gap-2 px-4 py-2 rounded-lg bg-primary-600 text-white hover:bg-primary-700 transition-colors">
			次へ：Windowsからの移行
			<svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
				<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 5l7 7-7 7" />
			</svg>
		</a>
	</div>
</article>
