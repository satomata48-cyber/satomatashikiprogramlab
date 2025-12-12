<script>
	import CodePreview from '$lib/components/CodePreview.svelte';
</script>

<svelte:head>
	<title>Claude Codeでカスタム Linux 構築 - Linux | さとまたラボ</title>
</svelte:head>

<article>
	<h1 class="text-3xl font-bold mb-2">Claude Codeでカスタム Linux OS 構築</h1>
	<p class="text-lg text-gray-600 dark:text-gray-400 mb-8">
		Buildrootを使って完全自己管理型のLinuxディストリビューションを作る
	</p>

	<!-- 概要 -->
	<section class="mb-10">
		<h2 id="overview" class="text-xl font-bold mb-4">プロジェクト概要</h2>

		<div class="p-6 rounded-xl bg-gradient-to-r from-indigo-50 to-purple-50 dark:from-indigo-900/20 dark:to-purple-900/20 border border-indigo-200 dark:border-indigo-800 mb-6">
			<div class="flex items-center gap-4 mb-4">
				<span class="text-3xl">🐧</span>
				<span class="text-2xl">+</span>
				<span class="text-3xl">🤖</span>
				<span class="text-2xl">=</span>
				<span class="text-3xl">💿</span>
			</div>
			<p class="text-gray-700 dark:text-gray-300">
				<strong>Claude Code</strong>を活用して、<strong>Buildroot + Linuxカーネル</strong>でゼロからカスタムLinuxディストリビューションを構築します。
				既存ディストロの改変（リブランディング）とは異なり、<strong>アップデートを含めて全て自分で管理できる</strong>構成を目指します。
			</p>
		</div>

		<div class="grid grid-cols-1 md:grid-cols-2 gap-4 mb-6">
			<div class="p-4 rounded-lg bg-blue-50 dark:bg-blue-900/20 border border-blue-200 dark:border-blue-800">
				<p class="font-semibold text-blue-800 dark:text-blue-200 mb-2">このアプローチの目的</p>
				<ul class="text-sm text-blue-700 dark:text-blue-300 list-disc list-inside space-y-1">
					<li>完全自己管理型のLinuxを作成</li>
					<li>アップデートも自分でコントロール</li>
					<li>システムの中身を完全に理解</li>
					<li>Claude Codeで開発を効率化</li>
				</ul>
			</div>
			<div class="p-4 rounded-lg bg-purple-50 dark:bg-purple-900/20 border border-purple-200 dark:border-purple-800">
				<p class="font-semibold text-purple-800 dark:text-purple-200 mb-2">リブランディングとの違い</p>
				<ul class="text-sm text-purple-700 dark:text-purple-300 list-disc list-inside space-y-1">
					<li>既存ディストロに依存しない</li>
					<li>パッケージ構成を自分で決定</li>
					<li>ビルドプロセスを完全に把握</li>
					<li>再現性の高い設定ファイル管理</li>
				</ul>
			</div>
		</div>
	</section>

	<!-- なぜBuildrootか -->
	<section class="mb-10">
		<h2 id="why-buildroot" class="text-xl font-bold mb-4">なぜBuildrootを選択するか</h2>

		<div class="overflow-x-auto mb-6">
			<table class="w-full text-sm">
				<thead>
					<tr class="border-b border-gray-200 dark:border-gray-700 bg-gray-50 dark:bg-gray-800">
						<th class="text-left py-3 px-4">項目</th>
						<th class="text-left py-3 px-4">Buildroot</th>
						<th class="text-left py-3 px-4">LFS</th>
						<th class="text-left py-3 px-4">Yocto</th>
						<th class="text-left py-3 px-4">既存ディストロ改変</th>
					</tr>
				</thead>
				<tbody>
					<tr class="border-b border-gray-200 dark:border-gray-700">
						<td class="py-3 px-4 font-medium">構築の自動化</td>
						<td class="py-3 px-4 text-green-600 dark:text-green-400 font-bold">◎</td>
						<td class="py-3 px-4 text-yellow-600 dark:text-yellow-400">△</td>
						<td class="py-3 px-4 text-green-600 dark:text-green-400">○</td>
						<td class="py-3 px-4 text-green-600 dark:text-green-400 font-bold">◎</td>
					</tr>
					<tr class="border-b border-gray-200 dark:border-gray-700">
						<td class="py-3 px-4 font-medium">学習コスト</td>
						<td class="py-3 px-4 text-green-600 dark:text-green-400">低〜中</td>
						<td class="py-3 px-4 text-red-600 dark:text-red-400">高</td>
						<td class="py-3 px-4 text-red-600 dark:text-red-400">高</td>
						<td class="py-3 px-4 text-green-600 dark:text-green-400">低</td>
					</tr>
					<tr class="border-b border-gray-200 dark:border-gray-700">
						<td class="py-3 px-4 font-medium">カスタマイズ性</td>
						<td class="py-3 px-4 text-green-600 dark:text-green-400 font-bold">◎</td>
						<td class="py-3 px-4 text-green-600 dark:text-green-400 font-bold">◎</td>
						<td class="py-3 px-4 text-green-600 dark:text-green-400 font-bold">◎</td>
						<td class="py-3 px-4 text-yellow-600 dark:text-yellow-400">△</td>
					</tr>
					<tr class="border-b border-gray-200 dark:border-gray-700">
						<td class="py-3 px-4 font-medium">ビルド時間</td>
						<td class="py-3 px-4 text-green-600 dark:text-green-400">短い（15分〜）</td>
						<td class="py-3 px-4 text-red-600 dark:text-red-400">長い</td>
						<td class="py-3 px-4 text-red-600 dark:text-red-400">長い（50分〜）</td>
						<td class="py-3 px-4">-</td>
					</tr>
					<tr class="border-b border-gray-200 dark:border-gray-700">
						<td class="py-3 px-4 font-medium">再現性</td>
						<td class="py-3 px-4 text-green-600 dark:text-green-400 font-bold">◎</td>
						<td class="py-3 px-4 text-yellow-600 dark:text-yellow-400">△</td>
						<td class="py-3 px-4 text-green-600 dark:text-green-400 font-bold">◎</td>
						<td class="py-3 px-4 text-yellow-600 dark:text-yellow-400">△</td>
					</tr>
					<tr>
						<td class="py-3 px-4 font-medium">「全て自分で管理」</td>
						<td class="py-3 px-4 text-green-600 dark:text-green-400 font-bold">◎</td>
						<td class="py-3 px-4 text-green-600 dark:text-green-400 font-bold">◎</td>
						<td class="py-3 px-4 text-green-600 dark:text-green-400">○</td>
						<td class="py-3 px-4 text-red-600 dark:text-red-400">×</td>
					</tr>
				</tbody>
			</table>
		</div>

		<div class="p-4 rounded-lg bg-green-50 dark:bg-green-900/20 border border-green-200 dark:border-green-800">
			<p class="font-semibold text-green-800 dark:text-green-200 mb-2">Buildrootの強み</p>
			<ul class="text-sm text-green-700 dark:text-green-300 list-disc list-inside space-y-1">
				<li><strong>設定ファイル（defconfig）ベース</strong>で再現性が高い</li>
				<li>パッケージ追加・削除が容易</li>
				<li>アップデートも自分で管理できる</li>
				<li>自動化されつつも<strong>中身が見える</strong></li>
				<li>最終的にISO/ブータブルイメージを生成可能</li>
				<li>2025年も活発に開発中（2025.02リリース済み）</li>
			</ul>
		</div>
	</section>

	<!-- Linuxシステムの構成要素 -->
	<section class="mb-10">
		<h2 id="linux-structure" class="text-xl font-bold mb-4">Linuxシステムの構成要素</h2>

		<div class="p-4 rounded-lg bg-gray-900 text-gray-100 font-mono text-sm mb-6 overflow-x-auto">
			<pre class="whitespace-pre">{`┌─────────────────────────────────────────────────┐
│           ユーザーアプリケーション                  │
│         (bash, vim, firefox, etc.)              │
├─────────────────────────────────────────────────┤
│              システムライブラリ                    │
│          (glibc, musl, libstdc++)               │
├─────────────────────────────────────────────────┤
│           基本ユーティリティ                       │
│      (coreutils, busybox, systemd/init)         │
├─────────────────────────────────────────────────┤
│              Linuxカーネル                        │
│    (プロセス管理、メモリ管理、デバイスドライバ)        │
├─────────────────────────────────────────────────┤
│           ブートローダー (GRUB等)                  │
├─────────────────────────────────────────────────┤
│              ハードウェア                         │
└─────────────────────────────────────────────────┘`}</pre>
		</div>

		<h3 class="font-bold text-lg mb-3">Linuxカーネルの役割</h3>

		<p class="text-gray-700 dark:text-gray-300 mb-4">
			カーネルは「OSの心臓部」であり、以下の機能を担います：
		</p>

		<div class="overflow-x-auto mb-6">
			<table class="w-full text-sm">
				<thead>
					<tr class="border-b border-gray-200 dark:border-gray-700 bg-gray-50 dark:bg-gray-800">
						<th class="text-left py-2 px-4">機能</th>
						<th class="text-left py-2 px-4">説明</th>
					</tr>
				</thead>
				<tbody class="text-gray-700 dark:text-gray-300">
					<tr class="border-b border-gray-200 dark:border-gray-700">
						<td class="py-2 px-4 font-medium">プロセス管理</td>
						<td class="py-2 px-4">プログラムの実行・スケジューリング</td>
					</tr>
					<tr class="border-b border-gray-200 dark:border-gray-700">
						<td class="py-2 px-4 font-medium">メモリ管理</td>
						<td class="py-2 px-4">RAMの割り当て・仮想メモリ</td>
					</tr>
					<tr class="border-b border-gray-200 dark:border-gray-700">
						<td class="py-2 px-4 font-medium">ファイルシステム</td>
						<td class="py-2 px-4">ext4, btrfs などでディスクアクセス</td>
					</tr>
					<tr class="border-b border-gray-200 dark:border-gray-700">
						<td class="py-2 px-4 font-medium">デバイスドライバ</td>
						<td class="py-2 px-4">ハードウェアとの通信</td>
					</tr>
					<tr class="border-b border-gray-200 dark:border-gray-700">
						<td class="py-2 px-4 font-medium">ネットワーク</td>
						<td class="py-2 px-4">TCP/IPスタック</td>
					</tr>
					<tr>
						<td class="py-2 px-4 font-medium">セキュリティ</td>
						<td class="py-2 px-4">権限管理、SELinux等</td>
					</tr>
				</tbody>
			</table>
		</div>

		<div class="p-4 rounded-lg bg-amber-50 dark:bg-amber-900/20 border border-amber-200 dark:border-amber-800">
			<p class="font-semibold text-amber-800 dark:text-amber-200 mb-2">重要なポイント</p>
			<p class="text-sm text-amber-700 dark:text-amber-300">
				カーネル単体では何もできません。<strong>ユーザー空間のツール</strong>（シェル、コマンド群など）が必要です。
				Buildrootはカーネルとユーザー空間の両方を一括で構築してくれます。
			</p>
		</div>
	</section>

	<!-- Buildrootの仕組み -->
	<section class="mb-10">
		<h2 id="buildroot-how" class="text-xl font-bold mb-4">Buildrootの仕組み</h2>

		<div class="p-4 rounded-lg bg-gray-900 text-gray-100 font-mono text-xs mb-6 overflow-x-auto">
			<pre class="whitespace-pre">{`┌──────────────────────────────────────────────────────────┐
│                      Buildroot                           │
│  ┌─────────────────────────────────────────────────────┐ │
│  │                   設定システム                       │ │
│  │              (make menuconfig)                      │ │
│  └─────────────────────────────────────────────────────┘ │
│                         ↓                                │
│  ┌─────────────────────────────────────────────────────┐ │
│  │               自動ダウンロード                        │ │
│  │    - Linuxカーネルソース                             │ │
│  │    - ツールチェーン (gcc, binutils)                  │ │
│  │    - ライブラリ (glibc/musl)                         │ │
│  │    - ユーティリティ (busybox等)                      │ │
│  │    - 選択したパッケージ全て                          │ │
│  └─────────────────────────────────────────────────────┘ │
│                         ↓                                │
│  ┌─────────────────────────────────────────────────────┐ │
│  │             クロスコンパイル・ビルド                   │ │
│  └─────────────────────────────────────────────────────┘ │
│                         ↓                                │
│  ┌─────────────────────────────────────────────────────┐ │
│  │                出力イメージ生成                       │ │
│  │    - rootfs.tar (ルートファイルシステム)              │ │
│  │    - bzImage (カーネルイメージ)                      │ │
│  │    - sdcard.img (ブータブルイメージ)                 │ │
│  └─────────────────────────────────────────────────────┘ │
└──────────────────────────────────────────────────────────┘`}</pre>
		</div>

		<h3 class="font-bold text-lg mb-3">Buildrootが自動化してくれること</h3>

		<div class="overflow-x-auto mb-6">
			<table class="w-full text-sm">
				<thead>
					<tr class="border-b border-gray-200 dark:border-gray-700 bg-gray-50 dark:bg-gray-800">
						<th class="text-left py-2 px-4">作業</th>
						<th class="text-left py-2 px-4">手動の場合</th>
						<th class="text-left py-2 px-4">Buildroot</th>
					</tr>
				</thead>
				<tbody class="text-gray-700 dark:text-gray-300">
					<tr class="border-b border-gray-200 dark:border-gray-700">
						<td class="py-2 px-4">ソース取得</td>
						<td class="py-2 px-4">各プロジェクトから個別DL</td>
						<td class="py-2 px-4 text-green-600 dark:text-green-400 font-medium">自動</td>
					</tr>
					<tr class="border-b border-gray-200 dark:border-gray-700">
						<td class="py-2 px-4">依存関係解決</td>
						<td class="py-2 px-4">自分で調査・管理</td>
						<td class="py-2 px-4 text-green-600 dark:text-green-400 font-medium">自動</td>
					</tr>
					<tr class="border-b border-gray-200 dark:border-gray-700">
						<td class="py-2 px-4">クロスコンパイラ構築</td>
						<td class="py-2 px-4">非常に複雑</td>
						<td class="py-2 px-4 text-green-600 dark:text-green-400 font-medium">自動</td>
					</tr>
					<tr class="border-b border-gray-200 dark:border-gray-700">
						<td class="py-2 px-4">パッチ適用</td>
						<td class="py-2 px-4">手動</td>
						<td class="py-2 px-4 text-green-600 dark:text-green-400 font-medium">自動</td>
					</tr>
					<tr class="border-b border-gray-200 dark:border-gray-700">
						<td class="py-2 px-4">ビルド順序</td>
						<td class="py-2 px-4">依存関係を考慮して手動</td>
						<td class="py-2 px-4 text-green-600 dark:text-green-400 font-medium">自動</td>
					</tr>
					<tr class="border-b border-gray-200 dark:border-gray-700">
						<td class="py-2 px-4">ルートFS構築</td>
						<td class="py-2 px-4">手動でディレクトリ構成</td>
						<td class="py-2 px-4 text-green-600 dark:text-green-400 font-medium">自動</td>
					</tr>
					<tr>
						<td class="py-2 px-4">イメージ生成</td>
						<td class="py-2 px-4">複雑なコマンド</td>
						<td class="py-2 px-4 text-green-600 dark:text-green-400 font-medium">自動</td>
					</tr>
				</tbody>
			</table>
		</div>
	</section>

	<!-- 基本的なビルドの流れ -->
	<section class="mb-10">
		<h2 id="build-flow" class="text-xl font-bold mb-4">基本的なビルドの流れ</h2>

		<CodePreview
			title="Buildrootビルド手順"
			description="取得から完成まで"
			language="bash"
			code={`# 1. Buildrootを取得
git clone https://github.com/buildroot/buildroot.git
cd buildroot

# 2. ターゲットの設定（メニュー形式）
make menuconfig
#   ここで以下を選択:
#   - ターゲットアーキテクチャ (x86_64)
#   - Linuxカーネルバージョン
#   - C ライブラリ (glibc or musl)
#   - 含めるパッケージ (bash, vim, etc.)
#   - 出力フォーマット (ISO, SDカード等)

# 3. ビルド実行（全自動）
make
#   → 15分〜数時間でシステム完成

# 4. 出力確認
ls output/images/
#   → bzImage, rootfs.ext4, sdcard.img など`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:12px;"><div style="color:#6a9955;">$ make menuconfig</div><div style="color:#4ec9b0;">[ncurses GUI が起動]</div><div style="margin-top:8px;color:#6a9955;">$ make</div><div style="color:#9cdcfe;">Building...</div><div style="color:#4ec9b0;">Output: output/images/</div></div>`}
		/>

		<div class="mt-6 p-4 rounded-lg bg-blue-50 dark:bg-blue-900/20 border border-blue-200 dark:border-blue-800">
			<p class="font-semibold text-blue-800 dark:text-blue-200 mb-2">make menuconfigでの主な設定項目</p>
			<ul class="text-sm text-blue-700 dark:text-blue-300 list-disc list-inside space-y-1">
				<li><strong>Target options</strong>：ターゲットアーキテクチャ（x86_64, ARM64等）</li>
				<li><strong>Toolchain</strong>：Cライブラリの選択（glibc/musl）</li>
				<li><strong>System configuration</strong>：ホスト名、バナー等</li>
				<li><strong>Kernel</strong>：Linuxカーネルバージョンと設定</li>
				<li><strong>Target packages</strong>：含めるソフトウェアパッケージ</li>
				<li><strong>Filesystem images</strong>：出力イメージ形式</li>
				<li><strong>Bootloaders</strong>：GRUB、syslinux等</li>
			</ul>
		</div>
	</section>

	<!-- アップデートの管理方法 -->
	<section class="mb-10">
		<h2 id="update-management" class="text-xl font-bold mb-4">アップデートの管理方法</h2>

		<div class="grid grid-cols-1 md:grid-cols-3 gap-4 mb-6">
			<div class="p-4 rounded-lg bg-gray-50 dark:bg-gray-800/50 border border-gray-200 dark:border-gray-700">
				<p class="font-semibold text-gray-800 dark:text-gray-200 mb-2">カーネルアップデート</p>
				<ol class="text-sm text-gray-700 dark:text-gray-300 list-decimal list-inside space-y-1">
					<li>make menuconfig でカーネルバージョン変更</li>
					<li>make linux-rebuild</li>
					<li>新しい bzImage が生成される</li>
				</ol>
			</div>
			<div class="p-4 rounded-lg bg-gray-50 dark:bg-gray-800/50 border border-gray-200 dark:border-gray-700">
				<p class="font-semibold text-gray-800 dark:text-gray-200 mb-2">パッケージアップデート</p>
				<ol class="text-sm text-gray-700 dark:text-gray-300 list-decimal list-inside space-y-1">
					<li>Buildroot自体を git pull で更新</li>
					<li>必要に応じて設定変更</li>
					<li>make clean && make で再ビルド</li>
				</ol>
			</div>
			<div class="p-4 rounded-lg bg-gray-50 dark:bg-gray-800/50 border border-gray-200 dark:border-gray-700">
				<p class="font-semibold text-gray-800 dark:text-gray-200 mb-2">セキュリティパッチ</p>
				<ol class="text-sm text-gray-700 dark:text-gray-300 list-decimal list-inside space-y-1">
					<li>自分でパッチを用意</li>
					<li>board/your-board/patches/ に配置</li>
					<li>ビルド時に自動的に適用される</li>
				</ol>
			</div>
		</div>
	</section>

	<!-- GUI/UIの実現可能性 -->
	<section class="mb-10">
		<h2 id="gui-options" class="text-xl font-bold mb-4">GUI/UIの実現可能性</h2>

		<div class="p-4 rounded-lg bg-gray-900 text-gray-100 font-mono text-xs mb-6 overflow-x-auto">
			<pre class="whitespace-pre">{`【ディスプレイサーバー】
  ├── X11 (Xorg)      ← 伝統的、互換性高い
  └── Wayland         ← モダン、軽量

【グラフィックライブラリ】
  ├── Qt5/Qt6         ← 高機能、やや重い
  ├── GTK3/GTK4       ← GNOME系
  ├── SDL2            ← ゲーム・シンプルUI向け
  └── DirectFB        ← 超軽量（Xなし）

【ウィンドウマネージャ/デスクトップ】
  ├── Matchbox        ← 超軽量（組み込み向け）
  ├── Fluxbox         ← 軽量
  ├── Openbox         ← 軽量
  ├── i3              ← タイル型WM
  └── Enlightenment   ← 見た目良い、軽量

【アプリケーション】
  ├── ターミナル (xterm, st, etc.)
  ├── ファイルマネージャ (pcmanfm, thunar)
  ├── ブラウザ (midori, netsurf, firefox)
  └── 各種ツール`}</pre>
		</div>

		<h3 class="font-bold text-lg mb-3">現実的なUI構成例</h3>

		<div class="overflow-x-auto mb-6">
			<table class="w-full text-sm">
				<thead>
					<tr class="border-b border-gray-200 dark:border-gray-700 bg-gray-50 dark:bg-gray-800">
						<th class="text-left py-2 px-4">レベル</th>
						<th class="text-left py-2 px-4">構成</th>
						<th class="text-left py-2 px-4">サイズ</th>
						<th class="text-left py-2 px-4">用途</th>
					</tr>
				</thead>
				<tbody class="text-gray-700 dark:text-gray-300">
					<tr class="border-b border-gray-200 dark:border-gray-700 bg-green-50 dark:bg-green-900/10">
						<td class="py-2 px-4 font-medium">最小GUI</td>
						<td class="py-2 px-4">Linux + BusyBox + DirectFB</td>
						<td class="py-2 px-4">~50MB</td>
						<td class="py-2 px-4">キオスク端末、単一アプリ専用機</td>
					</tr>
					<tr class="border-b border-gray-200 dark:border-gray-700 bg-blue-50 dark:bg-blue-900/10">
						<td class="py-2 px-4 font-medium">軽量デスクトップ</td>
						<td class="py-2 px-4">Linux + musl + X11 + Openbox</td>
						<td class="py-2 px-4">~200-500MB</td>
						<td class="py-2 px-4">軽量PC、Raspberry Pi的な用途</td>
					</tr>
					<tr class="bg-purple-50 dark:bg-purple-900/10">
						<td class="py-2 px-4 font-medium">フル機能</td>
						<td class="py-2 px-4">Linux + glibc + X11/Wayland + Enlightenment</td>
						<td class="py-2 px-4">~1-2GB</td>
						<td class="py-2 px-4">日常使用可能なデスクトップ</td>
					</tr>
				</tbody>
			</table>
		</div>
	</section>

	<!-- 開発の段階的アプローチ -->
	<section class="mb-10">
		<h2 id="phases" class="text-xl font-bold mb-4">開発の段階的アプローチ</h2>

		<div class="space-y-4">
			<div class="flex items-start gap-4">
				<div class="flex-shrink-0 w-10 h-10 rounded-full bg-green-500 text-white flex items-center justify-center font-bold">1</div>
				<div class="flex-1 p-4 rounded-lg bg-green-50 dark:bg-green-900/20 border border-green-200 dark:border-green-800">
					<p class="font-semibold text-green-800 dark:text-green-200">Phase 1: CLI版（基本システム）</p>
					<ul class="text-sm text-green-700 dark:text-green-300 list-disc list-inside mt-2 space-y-1">
						<li>ブート → ログイン → シェル操作</li>
						<li>ネットワーク機能</li>
						<li>基本ユーティリティ</li>
					</ul>
				</div>
			</div>

			<div class="flex justify-center">
				<svg class="w-6 h-6 text-gray-400" fill="none" stroke="currentColor" viewBox="0 0 24 24">
					<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M19 14l-7 7m0 0l-7-7m7 7V3" />
				</svg>
			</div>

			<div class="flex items-start gap-4">
				<div class="flex-shrink-0 w-10 h-10 rounded-full bg-blue-500 text-white flex items-center justify-center font-bold">2</div>
				<div class="flex-1 p-4 rounded-lg bg-blue-50 dark:bg-blue-900/20 border border-blue-200 dark:border-blue-800">
					<p class="font-semibold text-blue-800 dark:text-blue-200">Phase 2: 最小GUI版</p>
					<ul class="text-sm text-blue-700 dark:text-blue-300 list-disc list-inside mt-2 space-y-1">
						<li>フレームバッファ + 簡単なUIアプリ</li>
						<li>または X11 + 最小ウィンドウマネージャ</li>
					</ul>
				</div>
			</div>

			<div class="flex justify-center">
				<svg class="w-6 h-6 text-gray-400" fill="none" stroke="currentColor" viewBox="0 0 24 24">
					<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M19 14l-7 7m0 0l-7-7m7 7V3" />
				</svg>
			</div>

			<div class="flex items-start gap-4">
				<div class="flex-shrink-0 w-10 h-10 rounded-full bg-purple-500 text-white flex items-center justify-center font-bold">3</div>
				<div class="flex-1 p-4 rounded-lg bg-purple-50 dark:bg-purple-900/20 border border-purple-200 dark:border-purple-800">
					<p class="font-semibold text-purple-800 dark:text-purple-200">Phase 3: デスクトップ版</p>
					<ul class="text-sm text-purple-700 dark:text-purple-300 list-disc list-inside mt-2 space-y-1">
						<li>X11/Wayland + ウィンドウマネージャ</li>
						<li>ファイルマネージャ、ターミナル</li>
						<li>ブラウザ等のアプリケーション</li>
					</ul>
				</div>
			</div>

			<div class="flex justify-center">
				<svg class="w-6 h-6 text-gray-400" fill="none" stroke="currentColor" viewBox="0 0 24 24">
					<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M19 14l-7 7m0 0l-7-7m7 7V3" />
				</svg>
			</div>

			<div class="flex items-start gap-4">
				<div class="flex-shrink-0 w-10 h-10 rounded-full bg-amber-500 text-white flex items-center justify-center font-bold">4</div>
				<div class="flex-1 p-4 rounded-lg bg-amber-50 dark:bg-amber-900/20 border border-amber-200 dark:border-amber-800">
					<p class="font-semibold text-amber-800 dark:text-amber-200">Phase 4: 独自機能追加</p>
					<ul class="text-sm text-amber-700 dark:text-amber-300 list-disc list-inside mt-2 space-y-1">
						<li>カスタムアプリケーション</li>
						<li>独自テーマ/ブランディング</li>
						<li>パッケージ管理システム</li>
					</ul>
				</div>
			</div>
		</div>
	</section>

	<!-- Claude Code活用 -->
	<section class="mb-10">
		<h2 id="claude-code" class="text-xl font-bold mb-4">Claude Code活用での作業分担</h2>

		<div class="grid grid-cols-1 md:grid-cols-2 gap-6 mb-6">
			<div class="p-5 rounded-lg bg-indigo-50 dark:bg-indigo-900/20 border border-indigo-200 dark:border-indigo-800">
				<div class="flex items-center gap-2 mb-3">
					<span class="text-2xl">🤖</span>
					<p class="font-semibold text-indigo-800 dark:text-indigo-200">Claude Codeでできること</p>
				</div>
				<ul class="text-sm text-indigo-700 dark:text-indigo-300 space-y-2">
					<li class="flex items-start gap-2">
						<span class="text-indigo-500 mt-0.5">✓</span>
						<span><strong>設定ファイル作成</strong>：Buildrootの.configファイル生成</span>
					</li>
					<li class="flex items-start gap-2">
						<span class="text-indigo-500 mt-0.5">✓</span>
						<span><strong>ビルドスクリプト作成</strong>：自動化スクリプト</span>
					</li>
					<li class="flex items-start gap-2">
						<span class="text-indigo-500 mt-0.5">✓</span>
						<span><strong>カスタムパッケージ定義</strong>：独自アプリの追加方法</span>
					</li>
					<li class="flex items-start gap-2">
						<span class="text-indigo-500 mt-0.5">✓</span>
						<span><strong>部分的なビルドテスト</strong>：小規模なコンポーネント</span>
					</li>
					<li class="flex items-start gap-2">
						<span class="text-indigo-500 mt-0.5">✓</span>
						<span><strong>ドキュメント作成</strong>：手順書、設計書</span>
					</li>
					<li class="flex items-start gap-2">
						<span class="text-indigo-500 mt-0.5">✓</span>
						<span><strong>QEMUでの起動テスト</strong>：CLIベースのテスト</span>
					</li>
				</ul>
			</div>

			<div class="p-5 rounded-lg bg-orange-50 dark:bg-orange-900/20 border border-orange-200 dark:border-orange-800">
				<div class="flex items-center gap-2 mb-3">
					<span class="text-2xl">👤</span>
					<p class="font-semibold text-orange-800 dark:text-orange-200">ユーザー側で必要な作業</p>
				</div>
				<ul class="text-sm text-orange-700 dark:text-orange-300 space-y-2">
					<li class="flex items-start gap-2">
						<span class="text-orange-500 mt-0.5">•</span>
						<span><strong>フルビルドの実行</strong>：時間がかかる（GUI付きは1-3時間）</span>
					</li>
					<li class="flex items-start gap-2">
						<span class="text-orange-500 mt-0.5">•</span>
						<span><strong>GUIの実際の表示確認</strong>：グラフィカル出力の確認</span>
					</li>
					<li class="flex items-start gap-2">
						<span class="text-orange-500 mt-0.5">•</span>
						<span><strong>実機でのテスト</strong>：ハードウェア依存の確認</span>
					</li>
				</ul>
			</div>
		</div>

		<div class="p-5 rounded-lg bg-gradient-to-r from-green-50 to-emerald-50 dark:from-green-900/20 dark:to-emerald-900/20 border border-green-200 dark:border-green-800">
			<p class="font-semibold text-green-800 dark:text-green-200 mb-3">作業フロー</p>
			<div class="flex flex-col md:flex-row items-center gap-4">
				<div class="flex-1 p-3 bg-white dark:bg-gray-800 rounded-lg text-center">
					<p class="text-sm font-medium text-gray-800 dark:text-gray-200 mb-2">Claude Codeがやること</p>
					<ul class="text-xs text-gray-600 dark:text-gray-400 space-y-1">
						<li>完全な設定ファイル一式を作成</li>
						<li>ビルド手順を完全自動化したスクリプト</li>
						<li>実行するだけで完成する状態に</li>
					</ul>
				</div>
				<svg class="w-8 h-8 text-green-500 rotate-90 md:rotate-0" fill="none" stroke="currentColor" viewBox="0 0 24 24">
					<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M14 5l7 7m0 0l-7 7m7-7H3" />
				</svg>
				<div class="flex-1 p-3 bg-white dark:bg-gray-800 rounded-lg text-center">
					<p class="text-sm font-medium text-gray-800 dark:text-gray-200 mb-2">ユーザーがやること</p>
					<ul class="text-xs text-gray-600 dark:text-gray-400 space-y-1">
						<li>生成されたファイルをダウンロード</li>
						<li>自分のPC/VMで make 実行</li>
						<li>実際のGUIを確認・カスタマイズ</li>
					</ul>
				</div>
			</div>
		</div>
	</section>

	<!-- 決定が必要な項目 -->
	<section class="mb-10">
		<h2 id="decisions" class="text-xl font-bold mb-4">始める前に決定する項目</h2>

		<p class="text-gray-700 dark:text-gray-300 mb-4">
			以下を決定することで、具体的な実装に進めます：
		</p>

		<div class="grid grid-cols-1 md:grid-cols-2 gap-4">
			<div class="p-4 rounded-lg bg-gray-50 dark:bg-gray-800/50 border border-gray-200 dark:border-gray-700">
				<p class="font-semibold text-gray-800 dark:text-gray-200 mb-2">1. ターゲット環境</p>
				<ul class="text-sm text-gray-700 dark:text-gray-300 space-y-1">
					<li class="flex items-center gap-2">
						<input type="checkbox" class="rounded" disabled />
						<span>QEMU（仮想マシン）</span>
					</li>
					<li class="flex items-center gap-2">
						<input type="checkbox" class="rounded" disabled />
						<span>実機（USB起動など）</span>
					</li>
					<li class="flex items-center gap-2">
						<input type="checkbox" class="rounded" disabled />
						<span>両対応</span>
					</li>
				</ul>
			</div>

			<div class="p-4 rounded-lg bg-gray-50 dark:bg-gray-800/50 border border-gray-200 dark:border-gray-700">
				<p class="font-semibold text-gray-800 dark:text-gray-200 mb-2">2. Cライブラリの選択</p>
				<ul class="text-sm text-gray-700 dark:text-gray-300 space-y-1">
					<li class="flex items-center gap-2">
						<input type="checkbox" class="rounded" disabled />
						<span><strong>glibc</strong>：互換性重視（多くのソフトが動く）</span>
					</li>
					<li class="flex items-center gap-2">
						<input type="checkbox" class="rounded" disabled />
						<span><strong>musl</strong>：軽量・シンプル（サイズ小さい）</span>
					</li>
				</ul>
			</div>

			<div class="p-4 rounded-lg bg-gray-50 dark:bg-gray-800/50 border border-gray-200 dark:border-gray-700">
				<p class="font-semibold text-gray-800 dark:text-gray-200 mb-2">3. initシステム</p>
				<ul class="text-sm text-gray-700 dark:text-gray-300 space-y-1">
					<li class="flex items-center gap-2">
						<input type="checkbox" class="rounded" disabled />
						<span><strong>BusyBox init</strong>：最小構成</span>
					</li>
					<li class="flex items-center gap-2">
						<input type="checkbox" class="rounded" disabled />
						<span><strong>systemd</strong>：現代的だが大きい</span>
					</li>
					<li class="flex items-center gap-2">
						<input type="checkbox" class="rounded" disabled />
						<span><strong>OpenRC</strong>：中間的</span>
					</li>
				</ul>
			</div>

			<div class="p-4 rounded-lg bg-gray-50 dark:bg-gray-800/50 border border-gray-200 dark:border-gray-700">
				<p class="font-semibold text-gray-800 dark:text-gray-200 mb-2">4. UIレベル</p>
				<ul class="text-sm text-gray-700 dark:text-gray-300 space-y-1">
					<li class="flex items-center gap-2">
						<input type="checkbox" class="rounded" disabled />
						<span>CLI のみ（Phase 1）</span>
					</li>
					<li class="flex items-center gap-2">
						<input type="checkbox" class="rounded" disabled />
						<span>最小GUI（Phase 2）</span>
					</li>
					<li class="flex items-center gap-2">
						<input type="checkbox" class="rounded" disabled />
						<span>デスクトップ環境（Phase 3）</span>
					</li>
				</ul>
			</div>
		</div>
	</section>

	<!-- 参考リンク -->
	<section class="mb-10">
		<h2 id="references" class="text-xl font-bold mb-4">参考リンク</h2>

		<div class="grid grid-cols-1 md:grid-cols-2 gap-4">
			<a href="https://buildroot.org/" target="_blank" rel="noopener" class="p-4 rounded-lg bg-gray-50 dark:bg-gray-800/50 border border-gray-200 dark:border-gray-700 hover:border-blue-500 dark:hover:border-blue-400 transition-colors">
				<p class="font-semibold text-gray-800 dark:text-gray-200 mb-1">Buildroot公式</p>
				<p class="text-sm text-blue-600 dark:text-blue-400">buildroot.org</p>
			</a>
			<a href="https://buildroot.org/downloads/manual/manual.html" target="_blank" rel="noopener" class="p-4 rounded-lg bg-gray-50 dark:bg-gray-800/50 border border-gray-200 dark:border-gray-700 hover:border-blue-500 dark:hover:border-blue-400 transition-colors">
				<p class="font-semibold text-gray-800 dark:text-gray-200 mb-1">Buildrootマニュアル</p>
				<p class="text-sm text-blue-600 dark:text-blue-400">公式ドキュメント</p>
			</a>
			<a href="https://kernel.org/" target="_blank" rel="noopener" class="p-4 rounded-lg bg-gray-50 dark:bg-gray-800/50 border border-gray-200 dark:border-gray-700 hover:border-blue-500 dark:hover:border-blue-400 transition-colors">
				<p class="font-semibold text-gray-800 dark:text-gray-200 mb-1">Linux Kernel</p>
				<p class="text-sm text-blue-600 dark:text-blue-400">kernel.org</p>
			</a>
			<a href="https://www.linuxfromscratch.org/" target="_blank" rel="noopener" class="p-4 rounded-lg bg-gray-50 dark:bg-gray-800/50 border border-gray-200 dark:border-gray-700 hover:border-blue-500 dark:hover:border-blue-400 transition-colors">
				<p class="font-semibold text-gray-800 dark:text-gray-200 mb-1">Linux From Scratch（参考）</p>
				<p class="text-sm text-blue-600 dark:text-blue-400">linuxfromscratch.org</p>
			</a>
		</div>
	</section>

	<!-- ナビゲーション -->
	<div class="flex justify-between pt-6 border-t border-gray-200 dark:border-gray-700">
		<a href="/linux/rebranding" class="inline-flex items-center gap-2 px-4 py-2 rounded-lg border border-gray-300 dark:border-gray-600 hover:bg-gray-100 dark:hover:bg-gray-800 transition-colors">
			<svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
				<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 19l-7-7 7-7" />
			</svg>
			前へ：リブランディング
		</a>
		<span></span>
	</div>
</article>
