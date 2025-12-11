<script>
	import CodePreview from '$lib/components/CodePreview.svelte';
</script>

<svelte:head>
	<title>リブランディング手順 - Linux | さとまたラボ</title>
</svelte:head>

<article>
	<h1 class="text-3xl font-bold mb-2">Linux OSのリブランディング</h1>
	<p class="text-lg text-gray-600 dark:text-gray-400 mb-8">
		自分だけのオリジナルLinuxディストロを作ろう
	</p>

	<!-- 概要 -->
	<section class="mb-10">
		<h2 id="overview" class="text-xl font-bold mb-4">リブランディングとは</h2>

		<div class="p-6 rounded-xl bg-gradient-to-r from-purple-50 to-pink-50 dark:from-purple-900/20 dark:to-pink-900/20 border border-purple-200 dark:border-purple-800 mb-6">
			<div class="flex items-center gap-4 mb-4">
				<span class="text-3xl">🐧</span>
				<span class="text-2xl">→</span>
				<span class="text-3xl">🎨</span>
				<span class="text-2xl">→</span>
				<span class="text-3xl">💿</span>
			</div>
			<p class="text-gray-700 dark:text-gray-300">
				既存のLinuxディストリビューションをベースに、<strong>ソフトウェアの追加・削除</strong>、<strong>設定のカスタマイズ</strong>、<strong>デザインの変更</strong>などを行い、独自のISOイメージを作成することです。
			</p>
		</div>

		<div class="p-4 rounded-lg bg-blue-50 dark:bg-blue-900/20 border border-blue-200 dark:border-blue-800 mb-6">
			<p class="font-semibold text-blue-800 dark:text-blue-200 mb-2">リブランディングの用途</p>
			<ul class="text-sm text-blue-700 dark:text-blue-300 list-disc list-inside space-y-1">
				<li><strong>個人用バックアップ</strong>：現在の環境を丸ごとISO化して保存</li>
				<li><strong>チーム・企業配布</strong>：必要なソフトを入れた標準環境を配布</li>
				<li><strong>教育用</strong>：学習に必要なツールだけを入れた環境</li>
				<li><strong>オリジナルディストロ公開</strong>：独自ブランドのOSを公開</li>
			</ul>
		</div>
	</section>

	<!-- ツール比較 -->
	<section class="mb-10">
		<h2 id="tools" class="text-xl font-bold mb-4">リブランディングツール比較</h2>

		<div class="overflow-x-auto mb-6">
			<table class="w-full text-sm">
				<thead>
					<tr class="border-b border-gray-200 dark:border-gray-700 bg-gray-50 dark:bg-gray-800">
						<th class="text-left py-3 px-4">ツール</th>
						<th class="text-left py-3 px-4">対応OS</th>
						<th class="text-left py-3 px-4">難易度</th>
						<th class="text-left py-3 px-4">方式</th>
						<th class="text-left py-3 px-4">特徴</th>
					</tr>
				</thead>
				<tbody>
					<tr class="border-b border-gray-200 dark:border-gray-700 bg-green-50 dark:bg-green-900/10">
						<td class="py-3 px-4 font-bold text-green-600">Cubic</td>
						<td class="py-3 px-4">Ubuntu/Debian系</td>
						<td class="py-3 px-4"><span class="text-green-600">★☆☆ 簡単</span></td>
						<td class="py-3 px-4">GUI</td>
						<td class="py-3 px-4">ベースISOからカスタム</td>
					</tr>
					<tr class="border-b border-gray-200 dark:border-gray-700 bg-green-50 dark:bg-green-900/10">
						<td class="py-3 px-4 font-bold text-green-600">MX Snapshot</td>
						<td class="py-3 px-4">MX Linux</td>
						<td class="py-3 px-4"><span class="text-green-600">★☆☆ 簡単</span></td>
						<td class="py-3 px-4">GUI</td>
						<td class="py-3 px-4">現在の環境をISO化</td>
					</tr>
					<tr class="border-b border-gray-200 dark:border-gray-700">
						<td class="py-3 px-4 font-bold text-amber-600">Penguins Eggs</td>
						<td class="py-3 px-4">多数対応</td>
						<td class="py-3 px-4"><span class="text-amber-600">★★☆ 普通</span></td>
						<td class="py-3 px-4">CLI</td>
						<td class="py-3 px-4">現在の環境をISO化</td>
					</tr>
					<tr class="border-b border-gray-200 dark:border-gray-700">
						<td class="py-3 px-4 font-bold text-amber-600">Linux Live Kit</td>
						<td class="py-3 px-4">汎用</td>
						<td class="py-3 px-4"><span class="text-amber-600">★★☆ 普通</span></td>
						<td class="py-3 px-4">スクリプト</td>
						<td class="py-3 px-4">システム全体をISO化</td>
					</tr>
					<tr>
						<td class="py-3 px-4 font-bold text-red-600">Archiso</td>
						<td class="py-3 px-4">Arch系</td>
						<td class="py-3 px-4"><span class="text-red-600">★★★ 難しい</span></td>
						<td class="py-3 px-4">CLI</td>
						<td class="py-3 px-4">高度なカスタマイズ</td>
					</tr>
				</tbody>
			</table>
		</div>

		<div class="p-4 rounded-lg bg-green-50 dark:bg-green-900/20 border border-green-200 dark:border-green-800">
			<p class="font-semibold text-green-800 dark:text-green-200 mb-2">初心者へのおすすめ</p>
			<p class="text-sm text-green-700 dark:text-green-300">
				<strong>Cubic</strong>（Ubuntu系）または<strong>MX Snapshot</strong>（MX Linux）がGUI操作で最も簡単です。
			</p>
		</div>
	</section>

	<!-- Cubic -->
	<section class="mb-10">
		<h2 id="cubic" class="text-xl font-bold mb-4">
			<span class="inline-flex items-center justify-center w-8 h-8 bg-green-500 text-white rounded-full text-sm mr-2">1</span>
			Cubic（Ubuntu/Debian系）
		</h2>

		<div class="p-4 rounded-lg bg-green-50 dark:bg-green-900/20 border border-green-200 dark:border-green-800 mb-6">
			<p class="font-semibold text-green-800 dark:text-green-200 mb-2">Cubicとは</p>
			<p class="text-sm text-green-700 dark:text-green-300">
				<strong>C</strong>ustom <strong>Ub</strong>untu <strong>I</strong>SO <strong>C</strong>reatorの略。GUIウィザードでUbuntu/DebianベースのカスタムISOを簡単に作成できます。chroot環境でパッケージのインストールや設定変更が可能。
			</p>
		</div>

		<CodePreview
			title="Cubicのインストール"
			description="Ubuntu/Debian系でPPAから導入"
			language="bash"
			code={`# PPAを追加
sudo apt-add-repository universe
sudo apt-add-repository ppa:cubic-wizard/release

# パッケージリストを更新
sudo apt update

# Cubicをインストール
sudo apt install --no-install-recommends cubic

# 起動
cubic`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:12px;"><div style="color:#4ec9b0;">✓ cubic installed</div><div style="margin-top:8px;color:#6a9955;">GUIが起動します</div></div>`}
		/>

		<div class="mt-6 space-y-4">
			<h3 class="font-bold text-lg">Cubicの使い方</h3>

			<div class="p-4 rounded-lg bg-gray-50 dark:bg-gray-800/50 border border-gray-200 dark:border-gray-700">
				<p class="font-semibold text-gray-800 dark:text-gray-200 mb-3">Step 1: プロジェクト作成</p>
				<ol class="text-sm text-gray-700 dark:text-gray-300 list-decimal list-inside space-y-2">
					<li>Cubicを起動</li>
					<li>プロジェクトフォルダを指定（例：<code class="bg-gray-200 dark:bg-gray-700 px-1 rounded">~/cubic-projects/my-distro</code>）</li>
					<li>「Next」をクリック</li>
				</ol>
			</div>

			<div class="p-4 rounded-lg bg-gray-50 dark:bg-gray-800/50 border border-gray-200 dark:border-gray-700">
				<p class="font-semibold text-gray-800 dark:text-gray-200 mb-3">Step 2: ベースISOを選択</p>
				<ol class="text-sm text-gray-700 dark:text-gray-300 list-decimal list-inside space-y-2">
					<li>「Select」ボタンでベースとなるISOファイルを選択<br>
						<span class="text-xs text-gray-500">（事前にUbuntu/Linux Mint等のISOをダウンロードしておく）</span>
					</li>
					<li>「Custom ISO」セクションでディストロ名等を変更可能</li>
					<li>「Next」をクリック</li>
				</ol>
			</div>

			<div class="p-4 rounded-lg bg-gray-50 dark:bg-gray-800/50 border border-gray-200 dark:border-gray-700">
				<p class="font-semibold text-gray-800 dark:text-gray-200 mb-3">Step 3: chroot環境でカスタマイズ</p>
				<p class="text-sm text-gray-700 dark:text-gray-300 mb-3">
					ターミナルが表示されます。ここで自由にカスタマイズできます：
				</p>
				<CodePreview
					title="chroot内での操作例"
					description="パッケージの追加・削除"
					language="bash"
					code={`# パッケージリストを更新
apt update

# ソフトウェアを追加
apt install -y vim git curl nodejs npm

# 不要なソフトを削除
apt remove --purge thunderbird libreoffice-*
apt autoremove -y

# 壁紙を変更（/usr/share/backgrounds/に配置）
cp /path/to/my-wallpaper.jpg /usr/share/backgrounds/

# デフォルト設定を変更
# /etc/skel/ 以下のファイルが新規ユーザーにコピーされる

# 終わったらexitでchroot終了
exit`}
					previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:12px;"><div style="color:#ce9178;">(chroot) root@cubic:/#</div><div style="color:#6a9955;">apt install vim git</div><div style="color:#4ec9b0;">Setting up vim...</div></div>`}
				/>
			</div>

			<div class="p-4 rounded-lg bg-gray-50 dark:bg-gray-800/50 border border-gray-200 dark:border-gray-700">
				<p class="font-semibold text-gray-800 dark:text-gray-200 mb-3">Step 4: ISO生成</p>
				<ol class="text-sm text-gray-700 dark:text-gray-300 list-decimal list-inside space-y-2">
					<li>カスタマイズ完了後「Next」をクリック</li>
					<li>カーネルやブートオプションを確認</li>
					<li>「Generate」でISOを生成</li>
					<li>完成したISOはプロジェクトフォルダ内に保存される</li>
				</ol>
			</div>
		</div>

		<div class="mt-4 p-4 rounded-lg bg-amber-50 dark:bg-amber-900/20 border border-amber-200 dark:border-amber-800">
			<p class="font-semibold text-amber-800 dark:text-amber-200 mb-2">注意点</p>
			<ul class="text-sm text-amber-700 dark:text-amber-300 list-disc list-inside space-y-1">
				<li>CubicはベースISOからカスタムISOを作成（現在の環境ではない）</li>
				<li>十分なディスク容量が必要（最低20GB推奨）</li>
				<li>対応：Ubuntu 18.04〜24.04、Debian Bookworm以降</li>
			</ul>
		</div>

		<div class="mt-4">
			<a href="https://github.com/PJ-Singh-001/Cubic" target="_blank" rel="noopener" class="text-sm text-blue-600 dark:text-blue-400 hover:underline">GitHub: Cubic →</a>
		</div>
	</section>

	<!-- MX Snapshot -->
	<section class="mb-10">
		<h2 id="mx-snapshot" class="text-xl font-bold mb-4">
			<span class="inline-flex items-center justify-center w-8 h-8 bg-cyan-500 text-white rounded-full text-sm mr-2">2</span>
			MX Snapshot（MX Linux）
		</h2>

		<div class="p-4 rounded-lg bg-cyan-50 dark:bg-cyan-900/20 border border-cyan-200 dark:border-cyan-800 mb-6">
			<p class="font-semibold text-cyan-800 dark:text-cyan-200 mb-2">MX Snapshotとは</p>
			<p class="text-sm text-cyan-700 dark:text-cyan-300">
				MX Linuxに標準搭載されたGUIツール。<strong>現在使用中のシステム</strong>をそのままISOイメージに変換できます。バックアップ用途にも、配布用途にも使えます。
			</p>
		</div>

		<div class="p-4 rounded-lg bg-green-50 dark:bg-green-900/20 border border-green-200 dark:border-green-800 mb-6">
			<p class="font-semibold text-green-800 dark:text-green-200 mb-2">MX Snapshotの強み</p>
			<ul class="text-sm text-green-700 dark:text-green-300 list-disc list-inside space-y-1">
				<li>GUIで数クリックで完了</li>
				<li>現在の環境をそのままISO化</li>
				<li>プリインストールソフト（MX Linux）</li>
				<li>ユーザーデータ含む/除外を選択可能</li>
			</ul>
		</div>

		<div class="space-y-4">
			<h3 class="font-bold text-lg">MX Snapshotの使い方</h3>

			<div class="p-4 rounded-lg bg-gray-50 dark:bg-gray-800/50 border border-gray-200 dark:border-gray-700">
				<p class="font-semibold text-gray-800 dark:text-gray-200 mb-3">Step 1: 起動</p>
				<ol class="text-sm text-gray-700 dark:text-gray-300 list-decimal list-inside space-y-2">
					<li>MX Linuxのメニューから「MX Snapshot」を起動</li>
					<li>または <code class="bg-gray-200 dark:bg-gray-700 px-1 rounded">mx-snapshot</code> をターミナルで実行</li>
					<li>root権限が必要（パスワード入力）</li>
				</ol>
			</div>

			<div class="p-4 rounded-lg bg-gray-50 dark:bg-gray-800/50 border border-gray-200 dark:border-gray-700">
				<p class="font-semibold text-gray-800 dark:text-gray-200 mb-3">Step 2: モードを選択</p>
				<div class="text-sm text-gray-700 dark:text-gray-300 space-y-3">
					<div class="p-3 bg-white dark:bg-gray-800 rounded">
						<p class="font-medium text-blue-600 dark:text-blue-400">Preserving accounts（アカウント保持）</p>
						<p>ユーザーアカウント、/home のデータ、設定を全て含む。<br>
						<span class="text-xs text-gray-500">→ 個人バックアップ、同じ環境の複製に最適</span></p>
					</div>
					<div class="p-3 bg-white dark:bg-gray-800 rounded">
						<p class="font-medium text-green-600 dark:text-green-400">Reset accounts（アカウントリセット）</p>
						<p>ユーザーデータを含まない。インストール時に新規ユーザーを作成。<br>
						<span class="text-xs text-gray-500">→ 他人への配布、公開用ディストロに最適</span></p>
					</div>
				</div>
			</div>

			<div class="p-4 rounded-lg bg-gray-50 dark:bg-gray-800/50 border border-gray-200 dark:border-gray-700">
				<p class="font-semibold text-gray-800 dark:text-gray-200 mb-3">Step 3: 設定</p>
				<ul class="text-sm text-gray-700 dark:text-gray-300 list-disc list-inside space-y-2">
					<li><strong>Snapshot name</strong>：ISOファイル名</li>
					<li><strong>Work directory</strong>：作業フォルダ（十分な空き容量が必要）</li>
					<li><strong>Compression</strong>：圧縮形式（zstdが高速、xzが高圧縮）</li>
					<li><strong>Exclusions</strong>：除外するフォルダ（キャッシュ等）</li>
				</ul>
			</div>

			<div class="p-4 rounded-lg bg-gray-50 dark:bg-gray-800/50 border border-gray-200 dark:border-gray-700">
				<p class="font-semibold text-gray-800 dark:text-gray-200 mb-3">Step 4: 生成</p>
				<ol class="text-sm text-gray-700 dark:text-gray-300 list-decimal list-inside space-y-2">
					<li>「Next」または「OK」をクリック</li>
					<li>ISO生成が開始（システムサイズにより10〜30分程度）</li>
					<li>完成したISOは指定したWork directoryに保存</li>
				</ol>
			</div>
		</div>

		<CodePreview
			title="CLIでの実行"
			description="コマンドラインオプション"
			language="bash"
			code={`# 基本的な使い方（GUI起動）
sudo mx-snapshot

# CLIモードで実行
sudo mx-snapshot --cli

# オプション例
sudo mx-snapshot -c \\
  --reset \\                    # アカウントリセット
  -z zstd \\                    # zstd圧縮
  -x \\                         # 標準フォルダを除外
  -w /home/user/snapshot        # 作業ディレクトリ

# 特定のカーネルを使用
sudo mx-snapshot -k /boot/vmlinuz-6.1.0-mx`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:12px;"><div style="color:#6a9955;">Creating snapshot...</div><div style="color:#4ec9b0;">Compressing filesystem...</div><div style="color:#4ec9b0;">ISO created: my-mx-snapshot.iso</div></div>`}
		/>

		<div class="mt-4 p-4 rounded-lg bg-amber-50 dark:bg-amber-900/20 border border-amber-200 dark:border-amber-800">
			<p class="font-semibold text-amber-800 dark:text-amber-200 mb-2">容量の目安</p>
			<p class="text-sm text-amber-700 dark:text-amber-300">
				作業フォルダには、ルートパーティション使用量と同程度の空き容量が必要です。<br>
				例：システムが15GB使用中 → 最低15GBの空きが必要
			</p>
		</div>

		<div class="mt-4">
			<a href="https://mxlinux.org/wiki/help-files/help-mx-save-system-to-iso-snapshot/" target="_blank" rel="noopener" class="text-sm text-blue-600 dark:text-blue-400 hover:underline">MX Snapshot 公式ドキュメント →</a>
		</div>
	</section>

	<!-- Penguins Eggs -->
	<section class="mb-10">
		<h2 id="penguins-eggs" class="text-xl font-bold mb-4">
			<span class="inline-flex items-center justify-center w-8 h-8 bg-amber-500 text-white rounded-full text-sm mr-2">3</span>
			Penguins Eggs（多ディストロ対応）
		</h2>

		<div class="p-4 rounded-lg bg-amber-50 dark:bg-amber-900/20 border border-amber-200 dark:border-amber-800 mb-6">
			<p class="font-semibold text-amber-800 dark:text-amber-200 mb-2">Penguins Eggsとは</p>
			<p class="text-sm text-amber-700 dark:text-amber-300">
				多くのディストロに対応したリマスタリングツール。現在の環境をライブISOに変換。Debian、Ubuntu、Arch、Fedora、openSUSEなど幅広く対応。
			</p>
		</div>

		<div class="grid grid-cols-1 md:grid-cols-2 gap-4 mb-6">
			<div class="p-4 rounded-lg bg-green-50 dark:bg-green-900/20 border border-green-200 dark:border-green-800">
				<p class="font-semibold text-green-800 dark:text-green-200 mb-2">対応ディストロ</p>
				<ul class="text-sm text-green-700 dark:text-green-300 list-disc list-inside space-y-1">
					<li>Debian (Buster〜Trixie)</li>
					<li>Ubuntu / Linux Mint</li>
					<li>Arch Linux / Manjaro</li>
					<li>Fedora / AlmaLinux / Rocky</li>
					<li>openSUSE</li>
				</ul>
			</div>
			<div class="p-4 rounded-lg bg-blue-50 dark:bg-blue-900/20 border border-blue-200 dark:border-blue-800">
				<p class="font-semibold text-blue-800 dark:text-blue-200 mb-2">特徴</p>
				<ul class="text-sm text-blue-700 dark:text-blue-300 list-disc list-inside space-y-1">
					<li>Calamaresインストーラー対応</li>
					<li>PXEブート対応</li>
					<li>amd64 / i386 / arm64 対応</li>
					<li>活発な開発（2024年も更新中）</li>
				</ul>
			</div>
		</div>

		<CodePreview
			title="Penguins Eggsのインストール"
			description="複数の方法がある"
			language="bash"
			code={`# 方法1: AppImage（全ディストロ共通）
wget https://github.com/pieroproietti/penguins-eggs/releases/download/v10.0.50/penguins-eggs-10.0.50.AppImage
chmod +x penguins-eggs-*.AppImage
sudo ./penguins-eggs-*.AppImage

# 方法2: fresh-eggsスクリプト（推奨）
git clone https://github.com/pieroproietti/get-eggs
cd get-eggs
sudo ./get-eggs.sh

# 方法3: Debian/Ubuntu系はdebパッケージ
# GitHubリリースページから.debをダウンロード
sudo dpkg -i penguins-eggs_*.deb
sudo apt install -f  # 依存関係を解決`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:12px;"><div style="color:#4ec9b0;">✓ penguins-eggs installed</div><div style="margin-top:8px;color:#6a9955;">eggs version: 10.0.50</div></div>`}
		/>

		<CodePreview
			title="ISO作成の手順"
			description="基本的なコマンド"
			language="bash"
			code={`# 1. 初期設定（初回のみ）
sudo eggs dad -d  # 自動設定

# 2. Calamaresインストーラーを導入（オプション）
sudo eggs calamares -i

# 3. ISO生成
sudo eggs produce

# オプション付きの例
sudo eggs produce \\
  --prefix "MyDistro" \\     # ファイル名のプレフィックス
  --basename "mylinux" \\    # ISOのベース名
  --theme "eggs" \\          # テーマ
  --release                   # リリース版（高圧縮）

# ユーザーデータを含める場合
sudo eggs produce --clone

# 生成されたISOの場所
ls /home/eggs/`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:12px;"><div style="color:#6a9955;">$ sudo eggs produce</div><div style="color:#9cdcfe;">Creating live system...</div><div style="color:#9cdcfe;">Compressing squashfs...</div><div style="color:#4ec9b0;">ISO created: /home/eggs/MyDistro-mylinux.iso</div></div>`}
		/>

		<div class="mt-4 p-4 rounded-lg bg-purple-50 dark:bg-purple-900/20 border border-purple-200 dark:border-purple-800">
			<p class="font-semibold text-purple-800 dark:text-purple-200 mb-2">主なコマンド</p>
			<div class="text-sm text-purple-700 dark:text-purple-300 space-y-1">
				<p><code class="bg-purple-200 dark:bg-purple-800 px-1 rounded">eggs produce</code>：ISO生成</p>
				<p><code class="bg-purple-200 dark:bg-purple-800 px-1 rounded">eggs calamares -i</code>：インストーラー導入</p>
				<p><code class="bg-purple-200 dark:bg-purple-800 px-1 rounded">eggs kill</code>：作業ファイル削除</p>
				<p><code class="bg-purple-200 dark:bg-purple-800 px-1 rounded">eggs info</code>：システム情報表示</p>
			</div>
		</div>

		<div class="mt-4">
			<a href="https://penguins-eggs.net/" target="_blank" rel="noopener" class="text-sm text-blue-600 dark:text-blue-400 hover:underline">Penguins Eggs 公式サイト →</a>
		</div>
	</section>

	<!-- Linux Live Kit -->
	<section class="mb-10">
		<h2 id="linux-live-kit" class="text-xl font-bold mb-4">
			<span class="inline-flex items-center justify-center w-8 h-8 bg-purple-500 text-white rounded-full text-sm mr-2">4</span>
			Linux Live Kit（汎用）
		</h2>

		<div class="p-4 rounded-lg bg-purple-50 dark:bg-purple-900/20 border border-purple-200 dark:border-purple-800 mb-6">
			<p class="font-semibold text-purple-800 dark:text-purple-200 mb-2">Linux Live Kitとは</p>
			<p class="text-sm text-purple-700 dark:text-purple-300">
				シェルスクリプト集でシステムをライブLinuxに変換。特定のディストロに依存せず、squashfsとaufs/overlayfsをサポートするカーネルなら使用可能。
			</p>
		</div>

		<CodePreview
			title="Linux Live Kitの使い方"
			description="基本的な手順"
			language="bash"
			code={`# 1. ダウンロード
cd /opt
git clone https://github.com/Tomas-M/linux-live.git
cd linux-live

# 2. 必要なパッケージをインストール
sudo apt install squashfs-tools genisoimage

# 3. 設定ファイルを編集
nano ./config

# config の主な設定項目：
# LIVEKITNAME="MyLinux"        # ディストロ名
# VMLINUZ="/boot/vmlinuz-$(uname -r)"  # カーネルパス
# AUESSION="changes"           # 変更保存フォルダ名

# 4. vmlinuzのシンボリックリンクを作成
sudo ln -sf /boot/vmlinuz-$(uname -r) /vmlinuz

# 5. ビルド実行（root権限で）
sudo ./build

# 6. 出力確認
ls /tmp/
# → MyLinux.iso（ISOファイル）
# → MyLinux.tar（USBブート用）`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:12px;"><div style="color:#6a9955;">$ sudo ./build</div><div style="color:#9cdcfe;">Creating squashfs modules...</div><div style="color:#9cdcfe;">Building ISO image...</div><div style="color:#4ec9b0;">Done: /tmp/MyLinux.iso</div></div>`}
		/>

		<div class="mt-4 p-4 rounded-lg bg-gray-50 dark:bg-gray-800/50 border border-gray-200 dark:border-gray-700">
			<p class="font-semibold text-gray-800 dark:text-gray-200 mb-3">USBブータブルにする</p>
			<CodePreview
				title="USBへの書き込み"
				description="tarファイルを展開してbootinst.shを実行"
				language="bash"
				code={`# USBドライブをマウント（例：/dev/sdb1）
sudo mount /dev/sdb1 /mnt/usb

# tarファイルを展開
sudo tar -xvf /tmp/MyLinux.tar -C /mnt/usb

# ブータブルにする
cd /mnt/usb/boot
sudo ./bootinst.sh

# アンマウント
sudo umount /mnt/usb`}
				previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:12px;"><div style="color:#4ec9b0;">USB is now bootable!</div></div>`}
			/>
		</div>

		<div class="mt-4 p-4 rounded-lg bg-amber-50 dark:bg-amber-900/20 border border-amber-200 dark:border-amber-800">
			<p class="font-semibold text-amber-800 dark:text-amber-200 mb-2">注意点</p>
			<ul class="text-sm text-amber-700 dark:text-amber-300 list-disc list-inside space-y-1">
				<li>現時点ではBIOSブートのみ対応（UEFI非対応）</li>
				<li>カーネルがsquashfsとaufs/overlayfsをサポートしている必要がある</li>
				<li>Debianベースで最も安定動作</li>
			</ul>
		</div>

		<div class="mt-4">
			<a href="https://www.linux-live.org/" target="_blank" rel="noopener" class="text-sm text-blue-600 dark:text-blue-400 hover:underline">Linux Live Kit 公式サイト →</a>
		</div>
	</section>

	<!-- ブランディングのカスタマイズ -->
	<section class="mb-10">
		<h2 id="branding" class="text-xl font-bold mb-4">ブランディング要素のカスタマイズ</h2>

		<p class="text-gray-700 dark:text-gray-300 mb-4">
			オリジナルディストロとして配布する場合、以下の要素をカスタマイズします：
		</p>

		<div class="grid grid-cols-1 md:grid-cols-2 gap-4">
			<div class="p-4 rounded-lg bg-gray-50 dark:bg-gray-800/50 border border-gray-200 dark:border-gray-700">
				<p class="font-semibold text-gray-800 dark:text-gray-200 mb-2">🎨 ビジュアル</p>
				<ul class="text-sm text-gray-700 dark:text-gray-300 list-disc list-inside space-y-1">
					<li>壁紙：<code class="bg-gray-200 dark:bg-gray-700 px-1 rounded text-xs">/usr/share/backgrounds/</code></li>
					<li>ロゴ・アイコン：<code class="bg-gray-200 dark:bg-gray-700 px-1 rounded text-xs">/usr/share/pixmaps/</code></li>
					<li>GRUBテーマ：<code class="bg-gray-200 dark:bg-gray-700 px-1 rounded text-xs">/boot/grub/themes/</code></li>
					<li>Plymouth（起動画面）</li>
				</ul>
			</div>

			<div class="p-4 rounded-lg bg-gray-50 dark:bg-gray-800/50 border border-gray-200 dark:border-gray-700">
				<p class="font-semibold text-gray-800 dark:text-gray-200 mb-2">📝 システム情報</p>
				<ul class="text-sm text-gray-700 dark:text-gray-300 list-disc list-inside space-y-1">
					<li>OS名：<code class="bg-gray-200 dark:bg-gray-700 px-1 rounded text-xs">/etc/os-release</code></li>
					<li>LSB情報：<code class="bg-gray-200 dark:bg-gray-700 px-1 rounded text-xs">/etc/lsb-release</code></li>
					<li>Issue：<code class="bg-gray-200 dark:bg-gray-700 px-1 rounded text-xs">/etc/issue</code></li>
					<li>MOTD：<code class="bg-gray-200 dark:bg-gray-700 px-1 rounded text-xs">/etc/motd</code></li>
				</ul>
			</div>

			<div class="p-4 rounded-lg bg-gray-50 dark:bg-gray-800/50 border border-gray-200 dark:border-gray-700">
				<p class="font-semibold text-gray-800 dark:text-gray-200 mb-2">⚙️ デフォルト設定</p>
				<ul class="text-sm text-gray-700 dark:text-gray-300 list-disc list-inside space-y-1">
					<li>skelフォルダ：<code class="bg-gray-200 dark:bg-gray-700 px-1 rounded text-xs">/etc/skel/</code></li>
					<li>デスクトップ設定</li>
					<li>ブラウザのホームページ</li>
					<li>ターミナルのテーマ</li>
				</ul>
			</div>

			<div class="p-4 rounded-lg bg-gray-50 dark:bg-gray-800/50 border border-gray-200 dark:border-gray-700">
				<p class="font-semibold text-gray-800 dark:text-gray-200 mb-2">📦 ソフトウェア</p>
				<ul class="text-sm text-gray-700 dark:text-gray-300 list-disc list-inside space-y-1">
					<li>プリインストールアプリ</li>
					<li>APTリポジトリ設定</li>
					<li>自動起動アプリ</li>
					<li>カスタムスクリプト</li>
				</ul>
			</div>
		</div>

		<CodePreview
			title="/etc/os-release の編集例"
			description="OS名をカスタマイズ"
			language="bash"
			code={`# /etc/os-release を編集
PRETTY_NAME="MyLinux 1.0"
NAME="MyLinux"
VERSION_ID="1.0"
VERSION="1.0 (Codename)"
VERSION_CODENAME=codename
ID=mylinux
ID_LIKE=debian ubuntu
HOME_URL="https://mylinux.example.com/"
SUPPORT_URL="https://mylinux.example.com/support"
BUG_REPORT_URL="https://mylinux.example.com/bugs"`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:12px;"><div style="color:#6a9955;">$ cat /etc/os-release</div><div style="color:#ce9178;">PRETTY_NAME="MyLinux 1.0"</div></div>`}
		/>
	</section>

	<!-- まとめ -->
	<section class="mb-10">
		<h2 id="summary" class="text-xl font-bold mb-4">まとめ</h2>

		<div class="p-4 rounded-lg bg-blue-50 dark:bg-blue-900/20 border border-blue-200 dark:border-blue-800 mb-4">
			<p class="font-semibold text-blue-800 dark:text-blue-200 mb-3">ツール選びのポイント</p>
			<ul class="text-sm text-blue-700 dark:text-blue-300 list-disc list-inside space-y-2">
				<li><strong>Ubuntu/Debian系でGUI派</strong> → Cubic</li>
				<li><strong>MX Linuxユーザー</strong> → MX Snapshot（最も簡単）</li>
				<li><strong>現在の環境をそのままISO化</strong> → Penguins Eggs または MX Snapshot</li>
				<li><strong>多様なディストロに対応したい</strong> → Penguins Eggs</li>
				<li><strong>低レベルな制御が必要</strong> → Linux Live Kit</li>
			</ul>
		</div>

		<div class="p-4 rounded-lg bg-green-50 dark:bg-green-900/20 border border-green-200 dark:border-green-800">
			<p class="font-semibold text-green-800 dark:text-green-200 mb-2">初心者向けおすすめ手順</p>
			<ol class="text-sm text-green-700 dark:text-green-300 list-decimal list-inside space-y-1">
				<li><strong>MX Linux</strong>をインストール</li>
				<li>好みのソフトをインストール・設定</li>
				<li><strong>MX Snapshot</strong>で「Reset accounts」モードでISO化</li>
				<li>完成！配布可能なオリジナルディストロの出来上がり</li>
			</ol>
		</div>
	</section>

	<!-- ナビゲーション -->
	<div class="flex justify-between pt-6 border-t border-gray-200 dark:border-gray-700">
		<a href="/linux/popular-2025" class="inline-flex items-center gap-2 px-4 py-2 rounded-lg border border-gray-300 dark:border-gray-600 hover:bg-gray-100 dark:hover:bg-gray-800 transition-colors">
			<svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
				<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 19l-7-7 7-7" />
			</svg>
			前へ：2025年人気のOS
		</a>
		<span></span>
	</div>
</article>
