<script>
	import CodePreview from '$lib/components/CodePreview.svelte';
</script>

<svelte:head>
	<title>2025年人気のLinux OS - Linux | さとまたラボ</title>
</svelte:head>

<article>
	<h1 class="text-3xl font-bold mb-2">2025年人気のLinux OS</h1>
	<p class="text-lg text-gray-600 dark:text-gray-400 mb-8">
		用途別におすすめのLinuxディストリビューションを紹介
	</p>

	<!-- 概要 -->
	<section class="mb-10">
		<h2 id="overview" class="text-xl font-bold mb-4">Linuxディストリビューションとは</h2>

		<div class="p-6 rounded-xl bg-gradient-to-r from-amber-50 to-green-50 dark:from-amber-900/20 dark:to-green-900/20 border border-amber-200 dark:border-amber-800 mb-6">
			<div class="flex items-center gap-4 mb-4">
				<span class="text-3xl">🐧</span>
				<span class="text-2xl">×</span>
				<span class="text-3xl">🎨</span>
			</div>
			<p class="text-gray-700 dark:text-gray-300">
				LinuxはOSの<strong>カーネル（核）</strong>部分の名前。これに様々なソフトウェアを組み合わせてパッケージ化したものが<strong>ディストリビューション（ディストロ）</strong>です。用途や好みに合わせて選べます。
			</p>
		</div>

		<div class="p-4 rounded-lg bg-blue-50 dark:bg-blue-900/20 border border-blue-200 dark:border-blue-800 mb-6">
			<p class="font-semibold text-blue-800 dark:text-blue-200 mb-2">主なディストロ系統</p>
			<div class="text-sm text-blue-700 dark:text-blue-300 space-y-2">
				<p><strong>Debian系</strong>：Ubuntu, Linux Mint, Pop!_OS, MX Linux など（apt/dpkg）</p>
				<p><strong>Red Hat系</strong>：Fedora, CentOS, Rocky Linux, AlmaLinux など（dnf/rpm）</p>
				<p><strong>Arch系</strong>：Arch Linux, Manjaro, EndeavourOS など（pacman）</p>
				<p><strong>独立系</strong>：openSUSE, Gentoo, NixOS など</p>
			</div>
		</div>
	</section>

	<!-- DistroWatch ランキング -->
	<section class="mb-10">
		<h2 id="ranking" class="text-xl font-bold mb-4">2025年 DistroWatch人気ランキング</h2>

		<div class="p-4 rounded-lg bg-amber-50 dark:bg-amber-900/20 border border-amber-200 dark:border-amber-800 mb-6">
			<p class="text-sm text-amber-700 dark:text-amber-300">
				<a href="https://distrowatch.com/" class="underline font-medium" target="_blank" rel="noopener">DistroWatch</a>のPage Hit Ranking（PHR）に基づく。実際の使用シェアとは異なる場合があります。
			</p>
		</div>

		<div class="overflow-x-auto mb-6">
			<table class="w-full text-sm">
				<thead>
					<tr class="border-b border-gray-200 dark:border-gray-700 bg-gray-50 dark:bg-gray-800">
						<th class="text-left py-3 px-4">順位</th>
						<th class="text-left py-3 px-4">ディストロ</th>
						<th class="text-left py-3 px-4">ベース</th>
						<th class="text-left py-3 px-4">特徴</th>
					</tr>
				</thead>
				<tbody>
					<tr class="border-b border-gray-200 dark:border-gray-700">
						<td class="py-3 px-4 font-bold text-amber-600">1</td>
						<td class="py-3 px-4 font-medium">MX Linux</td>
						<td class="py-3 px-4 text-gray-600 dark:text-gray-400">Debian</td>
						<td class="py-3 px-4">軽量・高速、独自ツール群が充実</td>
					</tr>
					<tr class="border-b border-gray-200 dark:border-gray-700">
						<td class="py-3 px-4 font-bold text-gray-500">2</td>
						<td class="py-3 px-4 font-medium">EndeavourOS</td>
						<td class="py-3 px-4 text-gray-600 dark:text-gray-400">Arch</td>
						<td class="py-3 px-4">Archを簡単に導入、ローリングリリース</td>
					</tr>
					<tr class="border-b border-gray-200 dark:border-gray-700">
						<td class="py-3 px-4 font-bold text-amber-700">3</td>
						<td class="py-3 px-4 font-medium">Linux Mint</td>
						<td class="py-3 px-4 text-gray-600 dark:text-gray-400">Ubuntu</td>
						<td class="py-3 px-4">初心者に最適、Windowsライク</td>
					</tr>
					<tr class="border-b border-gray-200 dark:border-gray-700">
						<td class="py-3 px-4">4</td>
						<td class="py-3 px-4 font-medium">Manjaro</td>
						<td class="py-3 px-4 text-gray-600 dark:text-gray-400">Arch</td>
						<td class="py-3 px-4">Archベースで使いやすい、ゲーミング向け</td>
					</tr>
					<tr class="border-b border-gray-200 dark:border-gray-700">
						<td class="py-3 px-4">5</td>
						<td class="py-3 px-4 font-medium">Pop!_OS</td>
						<td class="py-3 px-4 text-gray-600 dark:text-gray-400">Ubuntu</td>
						<td class="py-3 px-4">System76製、ゲーミング・開発向け</td>
					</tr>
					<tr class="border-b border-gray-200 dark:border-gray-700">
						<td class="py-3 px-4">6</td>
						<td class="py-3 px-4 font-medium">Fedora</td>
						<td class="py-3 px-4 text-gray-600 dark:text-gray-400">独自（Red Hat）</td>
						<td class="py-3 px-4">最新技術を積極採用、開発者向け</td>
					</tr>
					<tr class="border-b border-gray-200 dark:border-gray-700">
						<td class="py-3 px-4">7</td>
						<td class="py-3 px-4 font-medium">Ubuntu</td>
						<td class="py-3 px-4 text-gray-600 dark:text-gray-400">Debian</td>
						<td class="py-3 px-4">最も有名、情報量が豊富</td>
					</tr>
					<tr class="border-b border-gray-200 dark:border-gray-700">
						<td class="py-3 px-4">8</td>
						<td class="py-3 px-4 font-medium">Debian</td>
						<td class="py-3 px-4 text-gray-600 dark:text-gray-400">独自</td>
						<td class="py-3 px-4">安定性重視、サーバー定番</td>
					</tr>
					<tr class="border-b border-gray-200 dark:border-gray-700">
						<td class="py-3 px-4">9</td>
						<td class="py-3 px-4 font-medium">Zorin OS</td>
						<td class="py-3 px-4 text-gray-600 dark:text-gray-400">Ubuntu</td>
						<td class="py-3 px-4">Windows/Mac風UI、移行者向け</td>
					</tr>
					<tr>
						<td class="py-3 px-4">10</td>
						<td class="py-3 px-4 font-medium">openSUSE</td>
						<td class="py-3 px-4 text-gray-600 dark:text-gray-400">独自</td>
						<td class="py-3 px-4">YaSTツール、企業向け</td>
					</tr>
				</tbody>
			</table>
		</div>
	</section>

	<!-- 初心者向け -->
	<section class="mb-10">
		<h2 id="beginners" class="text-xl font-bold mb-4">
			<span class="text-2xl mr-2">🌱</span>
			初心者におすすめ
		</h2>

		<div class="grid grid-cols-1 md:grid-cols-2 gap-4">
			<!-- Linux Mint -->
			<div class="p-5 rounded-lg border-2 border-green-300 dark:border-green-700 bg-green-50 dark:bg-green-900/20">
				<div class="flex items-center gap-3 mb-3">
					<span class="text-2xl">🌿</span>
					<h3 class="font-bold text-lg">Linux Mint</h3>
					<span class="text-xs bg-green-500 text-white px-2 py-0.5 rounded">おすすめNo.1</span>
				</div>
				<p class="text-sm text-gray-700 dark:text-gray-300 mb-3">
					Windowsユーザーが最も違和感なく使える。Cinnamon/MATE/Xfceの3種類のデスクトップ環境から選択可能。
				</p>
				<ul class="text-xs text-gray-600 dark:text-gray-400 space-y-1">
					<li>✅ Windowsに似たUI</li>
					<li>✅ 日本語環境が簡単に構築可能</li>
					<li>✅ マルチメディアコーデック同梱</li>
					<li>✅ Ubuntuベースで情報豊富</li>
				</ul>
				<a href="https://linuxmint.com/" target="_blank" rel="noopener" class="inline-block mt-3 text-sm text-green-600 dark:text-green-400 hover:underline">公式サイト →</a>
			</div>

			<!-- Ubuntu -->
			<div class="p-5 rounded-lg border border-orange-300 dark:border-orange-700 bg-orange-50 dark:bg-orange-900/20">
				<div class="flex items-center gap-3 mb-3">
					<span class="text-2xl">🟠</span>
					<h3 class="font-bold text-lg">Ubuntu</h3>
					<span class="text-xs bg-orange-500 text-white px-2 py-0.5 rounded">最も有名</span>
				</div>
				<p class="text-sm text-gray-700 dark:text-gray-300 mb-3">
					世界で最も使われているLinuxディストロ。書籍・チュートリアル・フォーラムの情報が最も充実。
				</p>
				<ul class="text-xs text-gray-600 dark:text-gray-400 space-y-1">
					<li>✅ 圧倒的な情報量</li>
					<li>✅ 企業サポートあり（Canonical）</li>
					<li>✅ LTS版は5年サポート</li>
					<li>✅ WSL2で公式サポート</li>
				</ul>
				<a href="https://ubuntu.com/" target="_blank" rel="noopener" class="inline-block mt-3 text-sm text-orange-600 dark:text-orange-400 hover:underline">公式サイト →</a>
			</div>

			<!-- Zorin OS -->
			<div class="p-5 rounded-lg border border-blue-300 dark:border-blue-700 bg-blue-50 dark:bg-blue-900/20">
				<div class="flex items-center gap-3 mb-3">
					<span class="text-2xl">💎</span>
					<h3 class="font-bold text-lg">Zorin OS</h3>
					<span class="text-xs bg-blue-500 text-white px-2 py-0.5 rounded">Windows移行に</span>
				</div>
				<p class="text-sm text-gray-700 dark:text-gray-300 mb-3">
					WindowsやmacOSに似たレイアウトを選択可能。美しいデザインで移行のハードルを下げる。
				</p>
				<ul class="text-xs text-gray-600 dark:text-gray-400 space-y-1">
					<li>✅ Windows 11風のUI</li>
					<li>✅ Wineプリインストール</li>
					<li>✅ モダンで美しいデザイン</li>
					<li>✅ Lite版は古いPCにも対応</li>
				</ul>
				<a href="https://zorin.com/os/" target="_blank" rel="noopener" class="inline-block mt-3 text-sm text-blue-600 dark:text-blue-400 hover:underline">公式サイト →</a>
			</div>

			<!-- MX Linux -->
			<div class="p-5 rounded-lg border border-cyan-300 dark:border-cyan-700 bg-cyan-50 dark:bg-cyan-900/20">
				<div class="flex items-center gap-3 mb-3">
					<span class="text-2xl">🔷</span>
					<h3 class="font-bold text-lg">MX Linux</h3>
					<span class="text-xs bg-cyan-500 text-white px-2 py-0.5 rounded">人気No.1</span>
				</div>
				<p class="text-sm text-gray-700 dark:text-gray-300 mb-3">
					DistroWatch1位。軽量でありながら機能豊富。独自のMXツール群が便利。
				</p>
				<ul class="text-xs text-gray-600 dark:text-gray-400 space-y-1">
					<li>✅ 軽量で古いPCでも快適</li>
					<li>✅ MX Snapshot等の便利ツール</li>
					<li>✅ systemd非依存（選択可能）</li>
					<li>✅ 活発なコミュニティ</li>
				</ul>
				<a href="https://mxlinux.org/" target="_blank" rel="noopener" class="inline-block mt-3 text-sm text-cyan-600 dark:text-cyan-400 hover:underline">公式サイト →</a>
			</div>
		</div>
	</section>

	<!-- 開発者向け -->
	<section class="mb-10">
		<h2 id="developers" class="text-xl font-bold mb-4">
			<span class="text-2xl mr-2">💻</span>
			開発者におすすめ
		</h2>

		<div class="grid grid-cols-1 md:grid-cols-2 gap-4">
			<!-- Fedora -->
			<div class="p-5 rounded-lg border border-blue-300 dark:border-blue-700 bg-blue-50 dark:bg-blue-900/20">
				<div class="flex items-center gap-3 mb-3">
					<span class="text-2xl">🎩</span>
					<h3 class="font-bold text-lg">Fedora</h3>
					<span class="text-xs bg-blue-600 text-white px-2 py-0.5 rounded">最新技術</span>
				</div>
				<p class="text-sm text-gray-700 dark:text-gray-300 mb-3">
					Red Hat支援の先進的ディストロ。最新のカーネル、GNOME、開発ツールをいち早く採用。
				</p>
				<ul class="text-xs text-gray-600 dark:text-gray-400 space-y-1">
					<li>✅ 最新のソフトウェア</li>
					<li>✅ SELinuxによるセキュリティ</li>
					<li>✅ Podman（コンテナ）標準搭載</li>
					<li>✅ RHEL系の学習に最適</li>
				</ul>
				<a href="https://fedoraproject.org/" target="_blank" rel="noopener" class="inline-block mt-3 text-sm text-blue-600 dark:text-blue-400 hover:underline">公式サイト →</a>
			</div>

			<!-- Pop!_OS -->
			<div class="p-5 rounded-lg border border-cyan-300 dark:border-cyan-700 bg-cyan-50 dark:bg-cyan-900/20">
				<div class="flex items-center gap-3 mb-3">
					<span class="text-2xl">🚀</span>
					<h3 class="font-bold text-lg">Pop!_OS</h3>
					<span class="text-xs bg-cyan-600 text-white px-2 py-0.5 rounded">開発＆ゲーミング</span>
				</div>
				<p class="text-sm text-gray-700 dark:text-gray-300 mb-3">
					System76が開発。タイル型ウィンドウ管理、NVIDIAドライバ対応ISO、生産性重視。
				</p>
				<ul class="text-xs text-gray-600 dark:text-gray-400 space-y-1">
					<li>✅ 優れたタイルウィンドウ管理</li>
					<li>✅ NVIDIAドライバ同梱版あり</li>
					<li>✅ 開発者向けに最適化</li>
					<li>✅ クリーンなGNOME体験</li>
				</ul>
				<a href="https://pop.system76.com/" target="_blank" rel="noopener" class="inline-block mt-3 text-sm text-cyan-600 dark:text-cyan-400 hover:underline">公式サイト →</a>
			</div>

			<!-- Arch Linux -->
			<div class="p-5 rounded-lg border border-purple-300 dark:border-purple-700 bg-purple-50 dark:bg-purple-900/20">
				<div class="flex items-center gap-3 mb-3">
					<span class="text-2xl">🏔️</span>
					<h3 class="font-bold text-lg">Arch Linux</h3>
					<span class="text-xs bg-purple-600 text-white px-2 py-0.5 rounded">上級者向け</span>
				</div>
				<p class="text-sm text-gray-700 dark:text-gray-300 mb-3">
					DIY精神のローリングリリース。自分で構築することでLinuxを深く理解できる。
				</p>
				<ul class="text-xs text-gray-600 dark:text-gray-400 space-y-1">
					<li>✅ 常に最新のソフトウェア</li>
					<li>✅ AUR（膨大なパッケージ）</li>
					<li>✅ 優れたWiki（ArchWiki）</li>
					<li>✅ 最小構成から自由に構築</li>
				</ul>
				<a href="https://archlinux.org/" target="_blank" rel="noopener" class="inline-block mt-3 text-sm text-purple-600 dark:text-purple-400 hover:underline">公式サイト →</a>
			</div>

			<!-- EndeavourOS -->
			<div class="p-5 rounded-lg border border-indigo-300 dark:border-indigo-700 bg-indigo-50 dark:bg-indigo-900/20">
				<div class="flex items-center gap-3 mb-3">
					<span class="text-2xl">🌌</span>
					<h3 class="font-bold text-lg">EndeavourOS</h3>
					<span class="text-xs bg-indigo-600 text-white px-2 py-0.5 rounded">Arch入門</span>
				</div>
				<p class="text-sm text-gray-700 dark:text-gray-300 mb-3">
					Archの簡単インストーラー版。Archの利点を維持しつつ、導入の敷居を下げる。
				</p>
				<ul class="text-xs text-gray-600 dark:text-gray-400 space-y-1">
					<li>✅ Calamares GUIインストーラー</li>
					<li>✅ 複数のデスクトップ環境選択可</li>
					<li>✅ 素のArchに近い体験</li>
					<li>✅ フレンドリーなコミュニティ</li>
				</ul>
				<a href="https://endeavouros.com/" target="_blank" rel="noopener" class="inline-block mt-3 text-sm text-indigo-600 dark:text-indigo-400 hover:underline">公式サイト →</a>
			</div>
		</div>
	</section>

	<!-- ゲーミング向け -->
	<section class="mb-10">
		<h2 id="gaming" class="text-xl font-bold mb-4">
			<span class="text-2xl mr-2">🎮</span>
			ゲーミング向け
		</h2>

		<div class="grid grid-cols-1 md:grid-cols-2 gap-4">
			<!-- Pop!_OS -->
			<div class="p-5 rounded-lg border border-green-300 dark:border-green-700 bg-green-50 dark:bg-green-900/20">
				<div class="flex items-center gap-3 mb-3">
					<span class="text-2xl">🎯</span>
					<h3 class="font-bold text-lg">Pop!_OS</h3>
				</div>
				<p class="text-sm text-gray-700 dark:text-gray-300 mb-3">
					NVIDIA/AMDドライバ対応ISOを提供。Steamとの相性が良く、ゲーミングPCに最適。
				</p>
				<ul class="text-xs text-gray-600 dark:text-gray-400 space-y-1">
					<li>✅ NVIDIA ISO版でドライバ問題なし</li>
					<li>✅ Steamがすぐ使える</li>
					<li>✅ ハイブリッドGPU対応</li>
				</ul>
			</div>

			<!-- Manjaro -->
			<div class="p-5 rounded-lg border border-green-300 dark:border-green-700 bg-green-50 dark:bg-green-900/20">
				<div class="flex items-center gap-3 mb-3">
					<span class="text-2xl">🎲</span>
					<h3 class="font-bold text-lg">Manjaro</h3>
				</div>
				<p class="text-sm text-gray-700 dark:text-gray-300 mb-3">
					Arch系で最新のゲームドライバ対応。MHWDでハードウェアドライバを簡単管理。
				</p>
				<ul class="text-xs text-gray-600 dark:text-gray-400 space-y-1">
					<li>✅ 最新カーネル＆ドライバ</li>
					<li>✅ Steam/Lutris簡単導入</li>
					<li>✅ ゲーミングエディションあり</li>
				</ul>
				<a href="https://manjaro.org/" target="_blank" rel="noopener" class="inline-block mt-3 text-sm text-green-600 dark:text-green-400 hover:underline">公式サイト →</a>
			</div>

			<!-- Nobara -->
			<div class="p-5 rounded-lg border border-red-300 dark:border-red-700 bg-red-50 dark:bg-red-900/20">
				<div class="flex items-center gap-3 mb-3">
					<span class="text-2xl">🔥</span>
					<h3 class="font-bold text-lg">Nobara Linux</h3>
					<span class="text-xs bg-red-500 text-white px-2 py-0.5 rounded">注目</span>
				</div>
				<p class="text-sm text-gray-700 dark:text-gray-300 mb-3">
					Fedoraベースのゲーミング特化ディストロ。ProtonDB開発者が作成。
				</p>
				<ul class="text-xs text-gray-600 dark:text-gray-400 space-y-1">
					<li>✅ ゲーム向けカーネルパッチ</li>
					<li>✅ Wine/Proton最適化済み</li>
					<li>✅ OBS Studio等プリインストール</li>
				</ul>
				<a href="https://nobaraproject.org/" target="_blank" rel="noopener" class="inline-block mt-3 text-sm text-red-600 dark:text-red-400 hover:underline">公式サイト →</a>
			</div>

			<!-- Garuda -->
			<div class="p-5 rounded-lg border border-purple-300 dark:border-purple-700 bg-purple-50 dark:bg-purple-900/20">
				<div class="flex items-center gap-3 mb-3">
					<span class="text-2xl">🦅</span>
					<h3 class="font-bold text-lg">Garuda Linux</h3>
				</div>
				<p class="text-sm text-gray-700 dark:text-gray-300 mb-3">
					Arch系のゲーミング特化ディストロ。美しいUI、Btrfsスナップショット対応。
				</p>
				<ul class="text-xs text-gray-600 dark:text-gray-400 space-y-1">
					<li>✅ Gamer Edition提供</li>
					<li>✅ 自動Btrfsスナップショット</li>
					<li>✅ パフォーマンス最適化済み</li>
				</ul>
				<a href="https://garudalinux.org/" target="_blank" rel="noopener" class="inline-block mt-3 text-sm text-purple-600 dark:text-purple-400 hover:underline">公式サイト →</a>
			</div>
		</div>
	</section>

	<!-- サーバー向け -->
	<section class="mb-10">
		<h2 id="server" class="text-xl font-bold mb-4">
			<span class="text-2xl mr-2">🖥️</span>
			サーバー向け
		</h2>

		<div class="grid grid-cols-1 md:grid-cols-2 gap-4">
			<!-- Debian -->
			<div class="p-5 rounded-lg border border-red-300 dark:border-red-700 bg-red-50 dark:bg-red-900/20">
				<div class="flex items-center gap-3 mb-3">
					<span class="text-2xl">🍥</span>
					<h3 class="font-bold text-lg">Debian</h3>
					<span class="text-xs bg-red-500 text-white px-2 py-0.5 rounded">安定性重視</span>
				</div>
				<p class="text-sm text-gray-700 dark:text-gray-300 mb-3">
					圧倒的な安定性。多くのディストロの源流。長期サポートで運用コスト削減。
				</p>
				<ul class="text-xs text-gray-600 dark:text-gray-400 space-y-1">
					<li>✅ 5年以上のサポート</li>
					<li>✅ 50,000以上のパッケージ</li>
					<li>✅ 枯れた安定技術</li>
				</ul>
				<a href="https://www.debian.org/" target="_blank" rel="noopener" class="inline-block mt-3 text-sm text-red-600 dark:text-red-400 hover:underline">公式サイト →</a>
			</div>

			<!-- Ubuntu Server -->
			<div class="p-5 rounded-lg border border-orange-300 dark:border-orange-700 bg-orange-50 dark:bg-orange-900/20">
				<div class="flex items-center gap-3 mb-3">
					<span class="text-2xl">🟠</span>
					<h3 class="font-bold text-lg">Ubuntu Server</h3>
				</div>
				<p class="text-sm text-gray-700 dark:text-gray-300 mb-3">
					クラウド・コンテナ環境で広く使用。AWS、GCP、Azureで公式サポート。
				</p>
				<ul class="text-xs text-gray-600 dark:text-gray-400 space-y-1">
					<li>✅ クラウドで標準的</li>
					<li>✅ LTS版10年サポート（有償）</li>
					<li>✅ Snapパッケージ対応</li>
				</ul>
			</div>

			<!-- Rocky Linux -->
			<div class="p-5 rounded-lg border border-green-300 dark:border-green-700 bg-green-50 dark:bg-green-900/20">
				<div class="flex items-center gap-3 mb-3">
					<span class="text-2xl">🪨</span>
					<h3 class="font-bold text-lg">Rocky Linux</h3>
					<span class="text-xs bg-green-500 text-white px-2 py-0.5 rounded">CentOS後継</span>
				</div>
				<p class="text-sm text-gray-700 dark:text-gray-300 mb-3">
					CentOS創設者が開発。RHEL互換でエンタープライズ用途に最適。
				</p>
				<ul class="text-xs text-gray-600 dark:text-gray-400 space-y-1">
					<li>✅ RHEL 1:1互換</li>
					<li>✅ 長期サポート</li>
					<li>✅ 企業利用に最適</li>
				</ul>
				<a href="https://rockylinux.org/" target="_blank" rel="noopener" class="inline-block mt-3 text-sm text-green-600 dark:text-green-400 hover:underline">公式サイト →</a>
			</div>

			<!-- AlmaLinux -->
			<div class="p-5 rounded-lg border border-blue-300 dark:border-blue-700 bg-blue-50 dark:bg-blue-900/20">
				<div class="flex items-center gap-3 mb-3">
					<span class="text-2xl">🔵</span>
					<h3 class="font-bold text-lg">AlmaLinux</h3>
				</div>
				<p class="text-sm text-gray-700 dark:text-gray-300 mb-3">
					CloudLinux社支援のRHEL互換ディストロ。安定性と商用サポートを両立。
				</p>
				<ul class="text-xs text-gray-600 dark:text-gray-400 space-y-1">
					<li>✅ RHEL互換</li>
					<li>✅ 企業によるサポート</li>
					<li>✅ CentOSからの移行ツール</li>
				</ul>
				<a href="https://almalinux.org/" target="_blank" rel="noopener" class="inline-block mt-3 text-sm text-blue-600 dark:text-blue-400 hover:underline">公式サイト →</a>
			</div>
		</div>
	</section>

	<!-- 軽量・旧PC向け -->
	<section class="mb-10">
		<h2 id="lightweight" class="text-xl font-bold mb-4">
			<span class="text-2xl mr-2">🪶</span>
			軽量・旧PC向け
		</h2>

		<div class="grid grid-cols-1 md:grid-cols-2 gap-4">
			<div class="p-5 rounded-lg border border-gray-300 dark:border-gray-700 bg-gray-50 dark:bg-gray-900/20">
				<div class="flex items-center gap-3 mb-3">
					<span class="text-2xl">🦎</span>
					<h3 class="font-bold text-lg">antiX</h3>
				</div>
				<p class="text-sm text-gray-700 dark:text-gray-300 mb-3">
					256MB RAMでも動作。非常に古いPCを復活させる。
				</p>
				<ul class="text-xs text-gray-600 dark:text-gray-400 space-y-1">
					<li>✅ 最小要件: 256MB RAM</li>
					<li>✅ systemd非採用</li>
				</ul>
				<a href="https://antixlinux.com/" target="_blank" rel="noopener" class="inline-block mt-3 text-sm text-gray-600 dark:text-gray-400 hover:underline">公式サイト →</a>
			</div>

			<div class="p-5 rounded-lg border border-gray-300 dark:border-gray-700 bg-gray-50 dark:bg-gray-900/20">
				<div class="flex items-center gap-3 mb-3">
					<span class="text-2xl">🐶</span>
					<h3 class="font-bold text-lg">Puppy Linux</h3>
				</div>
				<p class="text-sm text-gray-700 dark:text-gray-300 mb-3">
					全体がRAM上で動作。超高速で古いPCに最適。
				</p>
				<ul class="text-xs text-gray-600 dark:text-gray-400 space-y-1">
					<li>✅ ISOサイズ約300MB</li>
					<li>✅ USBから即起動</li>
				</ul>
				<a href="https://puppylinux.com/" target="_blank" rel="noopener" class="inline-block mt-3 text-sm text-gray-600 dark:text-gray-400 hover:underline">公式サイト →</a>
			</div>

			<div class="p-5 rounded-lg border border-gray-300 dark:border-gray-700 bg-gray-50 dark:bg-gray-900/20">
				<div class="flex items-center gap-3 mb-3">
					<span class="text-2xl">💡</span>
					<h3 class="font-bold text-lg">Linux Lite</h3>
				</div>
				<p class="text-sm text-gray-700 dark:text-gray-300 mb-3">
					Windows XP/7ユーザー向け。軽量かつ初心者フレンドリー。
				</p>
				<ul class="text-xs text-gray-600 dark:text-gray-400 space-y-1">
					<li>✅ 1GB RAMで動作</li>
					<li>✅ Windowsに似た操作感</li>
				</ul>
				<a href="https://www.linuxliteos.com/" target="_blank" rel="noopener" class="inline-block mt-3 text-sm text-gray-600 dark:text-gray-400 hover:underline">公式サイト →</a>
			</div>

			<div class="p-5 rounded-lg border border-gray-300 dark:border-gray-700 bg-gray-50 dark:bg-gray-900/20">
				<div class="flex items-center gap-3 mb-3">
					<span class="text-2xl">🐧</span>
					<h3 class="font-bold text-lg">Lubuntu</h3>
				</div>
				<p class="text-sm text-gray-700 dark:text-gray-300 mb-3">
					Ubuntu公式フレーバー。LXQtデスクトップで軽量。
				</p>
				<ul class="text-xs text-gray-600 dark:text-gray-400 space-y-1">
					<li>✅ 公式Ubuntuサポート</li>
					<li>✅ 1GB RAMで動作</li>
				</ul>
				<a href="https://lubuntu.me/" target="_blank" rel="noopener" class="inline-block mt-3 text-sm text-gray-600 dark:text-gray-400 hover:underline">公式サイト →</a>
			</div>
		</div>
	</section>

	<!-- 選び方フローチャート -->
	<section class="mb-10">
		<h2 id="flowchart" class="text-xl font-bold mb-4">あなたに合ったディストロの選び方</h2>

		<div class="p-6 rounded-lg bg-gray-50 dark:bg-gray-800/50 border border-gray-200 dark:border-gray-700">
			<div class="space-y-4 text-sm">
				<div class="p-3 bg-white dark:bg-gray-800 rounded border-l-4 border-blue-500">
					<p class="font-bold text-blue-600 dark:text-blue-400">Q: Linuxは初めて？</p>
					<p class="text-gray-600 dark:text-gray-400 mt-1">
						→ はい: <strong>Linux Mint</strong> または <strong>Ubuntu</strong><br>
						→ いいえ: 次の質問へ
					</p>
				</div>

				<div class="p-3 bg-white dark:bg-gray-800 rounded border-l-4 border-green-500">
					<p class="font-bold text-green-600 dark:text-green-400">Q: ゲームをしたい？</p>
					<p class="text-gray-600 dark:text-gray-400 mt-1">
						→ はい: <strong>Pop!_OS</strong>（NVIDIA）または <strong>Nobara</strong><br>
						→ いいえ: 次の質問へ
					</p>
				</div>

				<div class="p-3 bg-white dark:bg-gray-800 rounded border-l-4 border-purple-500">
					<p class="font-bold text-purple-600 dark:text-purple-400">Q: 常に最新が欲しい？</p>
					<p class="text-gray-600 dark:text-gray-400 mt-1">
						→ はい: <strong>Fedora</strong> または <strong>Arch系</strong>（EndeavourOS）<br>
						→ いいえ: 次の質問へ
					</p>
				</div>

				<div class="p-3 bg-white dark:bg-gray-800 rounded border-l-4 border-amber-500">
					<p class="font-bold text-amber-600 dark:text-amber-400">Q: サーバー用途？</p>
					<p class="text-gray-600 dark:text-gray-400 mt-1">
						→ はい: <strong>Debian</strong> または <strong>Rocky Linux</strong><br>
						→ いいえ: 次の質問へ
					</p>
				</div>

				<div class="p-3 bg-white dark:bg-gray-800 rounded border-l-4 border-red-500">
					<p class="font-bold text-red-600 dark:text-red-400">Q: 古いPCを復活させたい？</p>
					<p class="text-gray-600 dark:text-gray-400 mt-1">
						→ はい: <strong>MX Linux</strong> または <strong>antiX</strong>
					</p>
				</div>
			</div>
		</div>
	</section>

	<!-- まとめ -->
	<section class="mb-10">
		<h2 id="summary" class="text-xl font-bold mb-4">まとめ</h2>

		<div class="p-4 rounded-lg bg-blue-50 dark:bg-blue-900/20 border border-blue-200 dark:border-blue-800">
			<ul class="text-sm text-blue-700 dark:text-blue-300 list-disc list-inside space-y-2">
				<li><strong>初心者</strong>：Linux Mint、Ubuntu、Zorin OS</li>
				<li><strong>開発者</strong>：Fedora、Pop!_OS、Arch/EndeavourOS</li>
				<li><strong>ゲーミング</strong>：Pop!_OS、Nobara、Manjaro</li>
				<li><strong>サーバー</strong>：Debian、Ubuntu Server、Rocky Linux</li>
				<li><strong>軽量</strong>：MX Linux、antiX、Puppy Linux</li>
				<li>迷ったら<strong>Linux Mint</strong>または<strong>Ubuntu</strong>から始めよう！</li>
			</ul>
		</div>

		<div class="mt-4 p-4 rounded-lg bg-amber-50 dark:bg-amber-900/20 border border-amber-200 dark:border-amber-800">
			<p class="text-sm text-amber-700 dark:text-amber-300">
				<strong>参考リンク</strong>：
				<a href="https://distrowatch.com/" class="underline" target="_blank" rel="noopener">DistroWatch</a>、
				<a href="https://www.techradar.com/best/best-linux-distros" class="underline" target="_blank" rel="noopener">TechRadar</a>、
				<a href="https://itsfoss.com/" class="underline" target="_blank" rel="noopener">It's FOSS</a>
			</p>
		</div>
	</section>

	<!-- ナビゲーション -->
	<div class="flex justify-between pt-6 border-t border-gray-200 dark:border-gray-700">
		<a href="/linux/switch-from-windows" class="inline-flex items-center gap-2 px-4 py-2 rounded-lg border border-gray-300 dark:border-gray-600 hover:bg-gray-100 dark:hover:bg-gray-800 transition-colors">
			<svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
				<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 19l-7-7 7-7" />
			</svg>
			前へ：Windowsからの移行
		</a>
		<a href="/linux/rebranding" class="inline-flex items-center gap-2 px-4 py-2 rounded-lg bg-primary-600 text-white hover:bg-primary-700 transition-colors">
			次へ：リブランディング
			<svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
				<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 5l7 7-7 7" />
			</svg>
		</a>
	</div>
</article>
