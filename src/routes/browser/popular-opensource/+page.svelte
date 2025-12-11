<script>
	import CodePreview from '$lib/components/CodePreview.svelte';
</script>

<svelte:head>
	<title>人気オープンソースブラウザ - さとまたプログラミングラボ</title>
	<meta name="description" content="Linux向け人気オープンソースブラウザを徹底比較。Firefox、Chromium、Brave、LibreWolf、Florpなど" />
</svelte:head>

<div class="max-w-4xl mx-auto">
	<h1 class="text-3xl sm:text-4xl font-bold text-gray-900 dark:text-white mb-6">
		人気オープンソースブラウザ 2025
	</h1>

	<p class="text-lg text-gray-600 dark:text-gray-300 mb-8">
		プライバシーを重視したオープンソースブラウザが注目を集めています。
		FirefoxベースとChromiumベース、それぞれの特徴と選び方を解説します。
	</p>

	<!-- なぜオープンソースブラウザか -->
	<section class="mb-12">
		<h2 class="text-2xl font-bold text-gray-900 dark:text-white mb-4 flex items-center gap-2">
			<span class="text-green-500">🔓</span> なぜオープンソースブラウザか
		</h2>

		<div class="grid md:grid-cols-3 gap-4 mb-6">
			<div class="bg-green-50 dark:bg-green-900/20 rounded-xl p-4 text-center">
				<div class="text-3xl mb-2">🔍</div>
				<h3 class="font-bold text-green-700 dark:text-green-400 mb-2">透明性</h3>
				<p class="text-sm text-gray-600 dark:text-gray-400">ソースコードが公開されており、何をしているか確認可能</p>
			</div>
			<div class="bg-blue-50 dark:bg-blue-900/20 rounded-xl p-4 text-center">
				<div class="text-3xl mb-2">🛡️</div>
				<h3 class="font-bold text-blue-700 dark:text-blue-400 mb-2">プライバシー</h3>
				<p class="text-sm text-gray-600 dark:text-gray-400">テレメトリや追跡を削除・無効化した派生版が多数</p>
			</div>
			<div class="bg-purple-50 dark:bg-purple-900/20 rounded-xl p-4 text-center">
				<div class="text-3xl mb-2">⚡</div>
				<h3 class="font-bold text-purple-700 dark:text-purple-400 mb-2">カスタマイズ</h3>
				<p class="text-sm text-gray-600 dark:text-gray-400">UIや機能を自由にカスタマイズ可能</p>
			</div>
		</div>

		<div class="bg-yellow-50 dark:bg-yellow-900/20 border border-yellow-200 dark:border-yellow-800 rounded-xl p-4">
			<h4 class="font-bold text-yellow-700 dark:text-yellow-400 mb-2">Manifest V3 問題</h4>
			<p class="text-sm text-yellow-800 dark:text-yellow-200">
				GoogleはChrome拡張機能のManifest V2を廃止予定。これにより <strong>uBlock Origin</strong>、
				<strong>Dark Reader</strong>、<strong>Adguard</strong> などの人気拡張機能が動作しなくなります。
				Firefoxベースブラウザはこの影響を受けません。
			</p>
		</div>
	</section>

	<!-- ブラウザエンジン解説 -->
	<section class="mb-12">
		<h2 class="text-2xl font-bold text-gray-900 dark:text-white mb-4 flex items-center gap-2">
			<span class="text-gray-500">⚙️</span> ブラウザエンジンを理解する
		</h2>

		<div class="grid md:grid-cols-2 gap-6">
			<div class="bg-orange-50 dark:bg-orange-900/20 rounded-xl p-6">
				<h3 class="font-bold text-orange-700 dark:text-orange-400 mb-3 flex items-center gap-2">
					<span>🦊</span> Gecko (Firefox系)
				</h3>
				<ul class="space-y-2 text-sm text-gray-700 dark:text-gray-300">
					<li>• Mozillaが開発するエンジン</li>
					<li>• 独自のJSエンジン「SpiderMonkey」</li>
					<li>• Manifest V2拡張機能を継続サポート</li>
					<li>• userChrome.cssでUI完全カスタマイズ</li>
					<li>• about:configで詳細設定可能</li>
				</ul>
			</div>
			<div class="bg-blue-50 dark:bg-blue-900/20 rounded-xl p-6">
				<h3 class="font-bold text-blue-700 dark:text-blue-400 mb-3 flex items-center gap-2">
					<span>🌐</span> Blink (Chromium系)
				</h3>
				<ul class="space-y-2 text-sm text-gray-700 dark:text-gray-300">
					<li>• Googleが開発するエンジン</li>
					<li>• 高速なJSエンジン「V8」</li>
					<li>• Chrome Web Storeの拡張機能対応</li>
					<li>• Webサイトとの互換性が最も高い</li>
					<li>• PWAのサポートが充実</li>
				</ul>
			</div>
		</div>
	</section>

	<!-- Firefoxベースブラウザ -->
	<section class="mb-12">
		<h2 class="text-2xl font-bold text-gray-900 dark:text-white mb-4 flex items-center gap-2">
			<span class="text-orange-500">🦊</span> Firefox ベースブラウザ
		</h2>

		<!-- Firefox -->
		<div class="bg-white dark:bg-gray-800 rounded-xl shadow-lg p-6 mb-6 border-l-4 border-orange-500">
			<div class="flex items-start justify-between mb-4">
				<div>
					<h3 class="text-xl font-bold text-gray-900 dark:text-white">Mozilla Firefox</h3>
					<p class="text-sm text-gray-500 dark:text-gray-400">オリジナル・定番ブラウザ</p>
				</div>
				<span class="bg-orange-100 text-orange-800 px-3 py-1 rounded-full text-sm font-medium">本家</span>
			</div>
			<p class="text-gray-600 dark:text-gray-300 mb-4">
				多くのLinuxディストリビューションにプリインストール。
				Googleに依存しない独立したブラウザで、プライバシー保護機能が充実。
			</p>
			<div class="grid grid-cols-2 sm:grid-cols-4 gap-2 text-sm">
				<div class="bg-gray-100 dark:bg-gray-700 rounded px-3 py-2 text-center">
					<div class="font-bold text-gray-900 dark:text-white">エンジン</div>
					<div class="text-gray-600 dark:text-gray-400">Gecko</div>
				</div>
				<div class="bg-gray-100 dark:bg-gray-700 rounded px-3 py-2 text-center">
					<div class="font-bold text-gray-900 dark:text-white">プライバシー</div>
					<div class="text-gray-600 dark:text-gray-400">良好</div>
				</div>
				<div class="bg-gray-100 dark:bg-gray-700 rounded px-3 py-2 text-center">
					<div class="font-bold text-gray-900 dark:text-white">拡張機能</div>
					<div class="text-gray-600 dark:text-gray-400">豊富</div>
				</div>
				<div class="bg-gray-100 dark:bg-gray-700 rounded px-3 py-2 text-center">
					<div class="font-bold text-gray-900 dark:text-white">同期</div>
					<div class="text-gray-600 dark:text-gray-400">Firefox Account</div>
				</div>
			</div>
		</div>

		<!-- LibreWolf -->
		<div class="bg-white dark:bg-gray-800 rounded-xl shadow-lg p-6 mb-6 border-l-4 border-blue-700">
			<div class="flex items-start justify-between mb-4">
				<div>
					<h3 class="text-xl font-bold text-gray-900 dark:text-white">LibreWolf</h3>
					<p class="text-sm text-gray-500 dark:text-gray-400">プライバシー最重視のFirefoxフォーク</p>
				</div>
				<span class="bg-blue-100 text-blue-800 px-3 py-1 rounded-full text-sm font-medium">推奨</span>
			</div>
			<p class="text-gray-600 dark:text-gray-300 mb-4">
				Firefoxからテレメトリを完全削除。DuckDuckGo、Searx、Qwantなどプライバシー重視の検索エンジンがデフォルト。
				uBlock Originがプリインストール。
			</p>
			<div class="flex flex-wrap gap-2 mb-4">
				<span class="bg-green-100 text-green-800 px-2 py-1 rounded text-xs">テレメトリ削除</span>
				<span class="bg-green-100 text-green-800 px-2 py-1 rounded text-xs">uBlock Origin内蔵</span>
				<span class="bg-green-100 text-green-800 px-2 py-1 rounded text-xs">強化されたトラッキング防止</span>
				<span class="bg-green-100 text-green-800 px-2 py-1 rounded text-xs">Fingerprint対策</span>
			</div>
			<CodePreview
				title="LibreWolf インストール (Debian/Ubuntu)"
				code={`# リポジトリ追加
sudo apt update && sudo apt install -y wget gnupg lsb-release apt-transport-https ca-certificates

distro=$(if echo " una bookworm vanessa focal jammy bullseye vera ulyssa uma " | grep -q " $(lsb_release -sc) "; then lsb_release -sc; else echo focal; fi)

wget -O- https://deb.librewolf.net/keyring.gpg | sudo gpg --dearmor -o /usr/share/keyrings/librewolf.gpg

sudo tee /etc/apt/sources.list.d/librewolf.sources << EOF > /dev/null
Types: deb
URIs: https://deb.librewolf.net
Suites: $distro
Components: main
Architectures: amd64
Signed-By: /usr/share/keyrings/librewolf.gpg
EOF

sudo apt update && sudo apt install librewolf -y`}
				language="bash"
			/>
		</div>

		<!-- Floorp -->
		<div class="bg-white dark:bg-gray-800 rounded-xl shadow-lg p-6 mb-6 border-l-4 border-purple-500">
			<div class="flex items-start justify-between mb-4">
				<div>
					<h3 class="text-xl font-bold text-gray-900 dark:text-white">Floorp</h3>
					<p class="text-sm text-gray-500 dark:text-gray-400">日本発・高機能Firefoxフォーク</p>
				</div>
				<span class="bg-purple-100 text-purple-800 px-3 py-1 rounded-full text-sm font-medium">注目</span>
			</div>
			<p class="text-gray-600 dark:text-gray-300 mb-4">
				日本の学生が開発。Firefox ESRベースでテレメトリを削除。
				垂直タブ、分割画面、ワークスペースなどChromeパワーユーザー向け機能を搭載。
			</p>
			<div class="flex flex-wrap gap-2 mb-4">
				<span class="bg-purple-100 text-purple-800 px-2 py-1 rounded text-xs">垂直タブ</span>
				<span class="bg-purple-100 text-purple-800 px-2 py-1 rounded text-xs">分割ビュー</span>
				<span class="bg-purple-100 text-purple-800 px-2 py-1 rounded text-xs">ワークスペース</span>
				<span class="bg-purple-100 text-purple-800 px-2 py-1 rounded text-xs">デュアルサイドバー</span>
			</div>
		</div>

		<!-- Zen Browser -->
		<div class="bg-white dark:bg-gray-800 rounded-xl shadow-lg p-6 mb-6 border-l-4 border-cyan-500">
			<div class="flex items-start justify-between mb-4">
				<div>
					<h3 class="text-xl font-bold text-gray-900 dark:text-white">Zen Browser</h3>
					<p class="text-sm text-gray-500 dark:text-gray-400">美しいUI・Arcライクなブラウザ</p>
				</div>
				<span class="bg-cyan-100 text-cyan-800 px-3 py-1 rounded-full text-sm font-medium">新興</span>
			</div>
			<p class="text-gray-600 dark:text-gray-300 mb-4">
				Arc、Edge、Vivaldi、Operaの良い部分を取り入れた美しいUI。
				画面領域を最大化する垂直タブ設計。コミュニティ主導の開発。
			</p>
			<div class="flex flex-wrap gap-2">
				<span class="bg-cyan-100 text-cyan-800 px-2 py-1 rounded text-xs">Apple風デザイン</span>
				<span class="bg-cyan-100 text-cyan-800 px-2 py-1 rounded text-xs">画面最大化設計</span>
				<span class="bg-cyan-100 text-cyan-800 px-2 py-1 rounded text-xs">高カスタマイズ性</span>
			</div>
		</div>

		<!-- Waterfox -->
		<div class="bg-white dark:bg-gray-800 rounded-xl shadow-lg p-6 mb-6 border-l-4 border-teal-500">
			<div class="flex items-start justify-between mb-4">
				<div>
					<h3 class="text-xl font-bold text-gray-900 dark:text-white">Waterfox</h3>
					<p class="text-sm text-gray-500 dark:text-gray-400">レガシー拡張機能対応</p>
				</div>
				<span class="bg-teal-100 text-teal-800 px-3 py-1 rounded-full text-sm font-medium">安定</span>
			</div>
			<p class="text-gray-600 dark:text-gray-300 mb-4">
				Intel C++コンパイラで最適化された高速ブラウザ。
				レガシー拡張機能をサポートし、広告ブロックがデフォルトで有効。
			</p>
		</div>
	</section>

	<!-- Chromiumベースブラウザ -->
	<section class="mb-12">
		<h2 class="text-2xl font-bold text-gray-900 dark:text-white mb-4 flex items-center gap-2">
			<span class="text-blue-500">🌐</span> Chromium ベースブラウザ
		</h2>

		<!-- Chromium -->
		<div class="bg-white dark:bg-gray-800 rounded-xl shadow-lg p-6 mb-6 border-l-4 border-blue-500">
			<div class="flex items-start justify-between mb-4">
				<div>
					<h3 class="text-xl font-bold text-gray-900 dark:text-white">Chromium</h3>
					<p class="text-sm text-gray-500 dark:text-gray-400">Chromeのオープンソース版</p>
				</div>
				<span class="bg-blue-100 text-blue-800 px-3 py-1 rounded-full text-sm font-medium">本家</span>
			</div>
			<p class="text-gray-600 dark:text-gray-300 mb-4">
				Google Chromeの基盤となるオープンソースプロジェクト。
				Googleの独自機能やサービスは含まれず、軽量でプライバシーに配慮。
			</p>
			<CodePreview
				title="Chromium インストール"
				code={`# Debian/Ubuntu
sudo apt install chromium-browser

# Fedora
sudo dnf install chromium

# Arch Linux
sudo pacman -S chromium`}
				language="bash"
			/>
		</div>

		<!-- Brave -->
		<div class="bg-white dark:bg-gray-800 rounded-xl shadow-lg p-6 mb-6 border-l-4 border-orange-600">
			<div class="flex items-start justify-between mb-4">
				<div>
					<h3 class="text-xl font-bold text-gray-900 dark:text-white">Brave</h3>
					<p class="text-sm text-gray-500 dark:text-gray-400">プライバシー重視の人気ブラウザ</p>
				</div>
				<span class="bg-orange-100 text-orange-800 px-3 py-1 rounded-full text-sm font-medium">人気</span>
			</div>
			<p class="text-gray-600 dark:text-gray-300 mb-4">
				Chromiumからgoogleのコードを削除。広告・トラッカーブロック、
				HTTPS自動アップグレード、Fingerprint対策が標準搭載。
			</p>
			<div class="flex flex-wrap gap-2 mb-4">
				<span class="bg-orange-100 text-orange-800 px-2 py-1 rounded text-xs">広告ブロック内蔵</span>
				<span class="bg-orange-100 text-orange-800 px-2 py-1 rounded text-xs">Tor接続対応</span>
				<span class="bg-orange-100 text-orange-800 px-2 py-1 rounded text-xs">IPFS対応</span>
				<span class="bg-orange-100 text-orange-800 px-2 py-1 rounded text-xs">Brave Rewards</span>
			</div>
			<CodePreview
				title="Brave インストール (Debian/Ubuntu)"
				code={`sudo apt install curl

sudo curl -fsSLo /usr/share/keyrings/brave-browser-archive-keyring.gpg https://brave-browser-apt-release.s3.brave.com/brave-browser-archive-keyring.gpg

echo "deb [signed-by=/usr/share/keyrings/brave-browser-archive-keyring.gpg] https://brave-browser-apt-release.s3.brave.com/ stable main"|sudo tee /etc/apt/sources.list.d/brave-browser-release.list

sudo apt update && sudo apt install brave-browser`}
				language="bash"
			/>
		</div>

		<!-- Thorium -->
		<div class="bg-white dark:bg-gray-800 rounded-xl shadow-lg p-6 mb-6 border-l-4 border-cyan-600">
			<div class="flex items-start justify-between mb-4">
				<div>
					<h3 class="text-xl font-bold text-gray-900 dark:text-white">Thorium</h3>
					<p class="text-sm text-gray-500 dark:text-gray-400">最速のChromiumフォーク</p>
				</div>
				<span class="bg-cyan-100 text-cyan-800 px-3 py-1 rounded-full text-sm font-medium">高速</span>
			</div>
			<p class="text-gray-600 dark:text-gray-300 mb-4">
				コンパイラレベルの最適化（SSE4.2、AVX、AES）により、
				Chromiumより8〜38%高速。UI改善やバグ修正も含む。
			</p>
			<div class="flex flex-wrap gap-2">
				<span class="bg-cyan-100 text-cyan-800 px-2 py-1 rounded text-xs">コンパイラ最適化</span>
				<span class="bg-cyan-100 text-cyan-800 px-2 py-1 rounded text-xs">8-38%高速化</span>
				<span class="bg-cyan-100 text-cyan-800 px-2 py-1 rounded text-xs">最小限のUI</span>
			</div>
		</div>

		<!-- Ungoogled Chromium -->
		<div class="bg-white dark:bg-gray-800 rounded-xl shadow-lg p-6 mb-6 border-l-4 border-gray-600">
			<div class="flex items-start justify-between mb-4">
				<div>
					<h3 class="text-xl font-bold text-gray-900 dark:text-white">Ungoogled Chromium</h3>
					<p class="text-sm text-gray-500 dark:text-gray-400">Google完全排除版</p>
				</div>
				<span class="bg-gray-100 text-gray-800 px-3 py-1 rounded-full text-sm font-medium">硬派</span>
			</div>
			<p class="text-gray-600 dark:text-gray-300 mb-4">
				Chromiumから Google へのすべての接続を削除。
				プライバシー最優先だが、同期機能やChromeウェブストアは使用不可。
			</p>
			<div class="flex flex-wrap gap-2">
				<span class="bg-gray-100 text-gray-800 px-2 py-1 rounded text-xs">Google完全排除</span>
				<span class="bg-gray-100 text-gray-800 px-2 py-1 rounded text-xs">手動拡張インストール</span>
			</div>
		</div>
	</section>

	<!-- 軽量ブラウザ -->
	<section class="mb-12">
		<h2 class="text-2xl font-bold text-gray-900 dark:text-white mb-4 flex items-center gap-2">
			<span class="text-green-500">🪶</span> 軽量ブラウザ
		</h2>

		<p class="text-gray-600 dark:text-gray-300 mb-6">
			古いハードウェアやリソースを節約したい場合に最適なブラウザ。
		</p>

		<div class="grid md:grid-cols-2 gap-4">
			<div class="bg-white dark:bg-gray-800 rounded-xl p-4 border border-gray-200 dark:border-gray-700">
				<h3 class="font-bold text-gray-900 dark:text-white mb-2">Falkon (KDE)</h3>
				<p class="text-sm text-gray-600 dark:text-gray-400 mb-2">
					KDE開発のQtWebEngineブラウザ。サイドバーにブックマーク・履歴表示、広告ブロッカー内蔵。
				</p>
				<code class="text-xs bg-gray-100 dark:bg-gray-700 px-2 py-1 rounded">sudo apt install falkon</code>
			</div>
			<div class="bg-white dark:bg-gray-800 rounded-xl p-4 border border-gray-200 dark:border-gray-700">
				<h3 class="font-bold text-gray-900 dark:text-white mb-2">GNOME Web (Epiphany)</h3>
				<p class="text-sm text-gray-600 dark:text-gray-400 mb-2">
					GNOMEデスクトップ標準ブラウザ。シンプルで軽量、WebKitエンジン採用。
				</p>
				<code class="text-xs bg-gray-100 dark:bg-gray-700 px-2 py-1 rounded">sudo apt install epiphany-browser</code>
			</div>
			<div class="bg-white dark:bg-gray-800 rounded-xl p-4 border border-gray-200 dark:border-gray-700">
				<h3 class="font-bold text-gray-900 dark:text-white mb-2">Midori</h3>
				<p class="text-sm text-gray-600 dark:text-gray-400 mb-2">
					軽量・高速・セキュアなプライバシー重視ブラウザ。Windows/Linux/Android対応。
				</p>
				<code class="text-xs bg-gray-100 dark:bg-gray-700 px-2 py-1 rounded">flatpak install midori</code>
			</div>
			<div class="bg-white dark:bg-gray-800 rounded-xl p-4 border border-gray-200 dark:border-gray-700">
				<h3 class="font-bold text-gray-900 dark:text-white mb-2">Konqueror (KDE)</h3>
				<p class="text-sm text-gray-600 dark:text-gray-400 mb-2">
					KHTMLエンジンの元祖（Safari/Chromeの祖先）。ファイルマネージャー機能も持つ。
				</p>
				<code class="text-xs bg-gray-100 dark:bg-gray-700 px-2 py-1 rounded">sudo apt install konqueror</code>
			</div>
		</div>
	</section>

	<!-- 比較表 -->
	<section class="mb-12">
		<h2 class="text-2xl font-bold text-gray-900 dark:text-white mb-4 flex items-center gap-2">
			<span class="text-purple-500">📊</span> ブラウザ比較表
		</h2>

		<div class="overflow-x-auto">
			<table class="w-full text-sm">
				<thead class="bg-gray-100 dark:bg-gray-700">
					<tr>
						<th class="px-3 py-3 text-left font-semibold">ブラウザ</th>
						<th class="px-3 py-3 text-left font-semibold">エンジン</th>
						<th class="px-3 py-3 text-left font-semibold">プライバシー</th>
						<th class="px-3 py-3 text-left font-semibold">速度</th>
						<th class="px-3 py-3 text-left font-semibold">おすすめ用途</th>
					</tr>
				</thead>
				<tbody class="divide-y divide-gray-200 dark:divide-gray-600">
					<tr class="bg-white dark:bg-gray-800">
						<td class="px-3 py-3 font-medium">Firefox</td>
						<td class="px-3 py-3">Gecko</td>
						<td class="px-3 py-3">⭐⭐⭐⭐</td>
						<td class="px-3 py-3">⭐⭐⭐⭐</td>
						<td class="px-3 py-3">一般用途、安定性重視</td>
					</tr>
					<tr class="bg-gray-50 dark:bg-gray-800/50">
						<td class="px-3 py-3 font-medium">LibreWolf</td>
						<td class="px-3 py-3">Gecko</td>
						<td class="px-3 py-3">⭐⭐⭐⭐⭐</td>
						<td class="px-3 py-3">⭐⭐⭐⭐</td>
						<td class="px-3 py-3">プライバシー最優先</td>
					</tr>
					<tr class="bg-white dark:bg-gray-800">
						<td class="px-3 py-3 font-medium">Floorp</td>
						<td class="px-3 py-3">Gecko</td>
						<td class="px-3 py-3">⭐⭐⭐⭐</td>
						<td class="px-3 py-3">⭐⭐⭐⭐</td>
						<td class="px-3 py-3">パワーユーザー、タブ管理</td>
					</tr>
					<tr class="bg-gray-50 dark:bg-gray-800/50">
						<td class="px-3 py-3 font-medium">Brave</td>
						<td class="px-3 py-3">Blink</td>
						<td class="px-3 py-3">⭐⭐⭐⭐⭐</td>
						<td class="px-3 py-3">⭐⭐⭐⭐⭐</td>
						<td class="px-3 py-3">Chrome互換+プライバシー</td>
					</tr>
					<tr class="bg-white dark:bg-gray-800">
						<td class="px-3 py-3 font-medium">Thorium</td>
						<td class="px-3 py-3">Blink</td>
						<td class="px-3 py-3">⭐⭐⭐</td>
						<td class="px-3 py-3">⭐⭐⭐⭐⭐</td>
						<td class="px-3 py-3">最高速度を求める人</td>
					</tr>
					<tr class="bg-gray-50 dark:bg-gray-800/50">
						<td class="px-3 py-3 font-medium">Chromium</td>
						<td class="px-3 py-3">Blink</td>
						<td class="px-3 py-3">⭐⭐⭐</td>
						<td class="px-3 py-3">⭐⭐⭐⭐⭐</td>
						<td class="px-3 py-3">Chrome互換、開発者</td>
					</tr>
				</tbody>
			</table>
		</div>
	</section>

	<!-- おすすめの選び方 -->
	<section class="mb-12">
		<h2 class="text-2xl font-bold text-gray-900 dark:text-white mb-4 flex items-center gap-2">
			<span class="text-yellow-500">💡</span> 目的別おすすめブラウザ
		</h2>

		<div class="grid md:grid-cols-2 gap-4">
			<div class="bg-gradient-to-br from-green-50 to-emerald-50 dark:from-green-900/20 dark:to-emerald-900/20 rounded-xl p-4">
				<h3 class="font-bold text-green-700 dark:text-green-400 mb-2">🛡️ プライバシー最優先</h3>
				<p class="text-sm text-gray-700 dark:text-gray-300 mb-2">テレメトリ・追跡を完全排除したい</p>
				<div class="font-bold text-green-800 dark:text-green-300">→ LibreWolf または Brave</div>
			</div>
			<div class="bg-gradient-to-br from-blue-50 to-cyan-50 dark:from-blue-900/20 dark:to-cyan-900/20 rounded-xl p-4">
				<h3 class="font-bold text-blue-700 dark:text-blue-400 mb-2">⚡ 最高速度</h3>
				<p class="text-sm text-gray-700 dark:text-gray-300 mb-2">とにかく速いブラウザがほしい</p>
				<div class="font-bold text-blue-800 dark:text-blue-300">→ Thorium</div>
			</div>
			<div class="bg-gradient-to-br from-purple-50 to-pink-50 dark:from-purple-900/20 dark:to-pink-900/20 rounded-xl p-4">
				<h3 class="font-bold text-purple-700 dark:text-purple-400 mb-2">🎨 カスタマイズ</h3>
				<p class="text-sm text-gray-700 dark:text-gray-300 mb-2">UIを自分好みに変えたい</p>
				<div class="font-bold text-purple-800 dark:text-purple-300">→ Floorp または Zen Browser</div>
			</div>
			<div class="bg-gradient-to-br from-orange-50 to-yellow-50 dark:from-orange-900/20 dark:to-yellow-900/20 rounded-xl p-4">
				<h3 class="font-bold text-orange-700 dark:text-orange-400 mb-2">🔧 Chrome互換</h3>
				<p class="text-sm text-gray-700 dark:text-gray-300 mb-2">Chrome拡張・サイト互換性重視</p>
				<div class="font-bold text-orange-800 dark:text-orange-300">→ Brave または Chromium</div>
			</div>
			<div class="bg-gradient-to-br from-gray-50 to-slate-50 dark:from-gray-900/20 dark:to-slate-900/20 rounded-xl p-4">
				<h3 class="font-bold text-gray-700 dark:text-gray-400 mb-2">🪶 軽量・低スペック</h3>
				<p class="text-sm text-gray-700 dark:text-gray-300 mb-2">古いPCで使いたい</p>
				<div class="font-bold text-gray-800 dark:text-gray-300">→ Falkon または Midori</div>
			</div>
			<div class="bg-gradient-to-br from-red-50 to-rose-50 dark:from-red-900/20 dark:to-rose-900/20 rounded-xl p-4">
				<h3 class="font-bold text-red-700 dark:text-red-400 mb-2">📦 安定・標準</h3>
				<p class="text-sm text-gray-700 dark:text-gray-300 mb-2">問題なく普通に使いたい</p>
				<div class="font-bold text-red-800 dark:text-red-300">→ Firefox</div>
			</div>
		</div>
	</section>

	<!-- 今後注目 -->
	<section class="mb-12">
		<h2 class="text-2xl font-bold text-gray-900 dark:text-white mb-4 flex items-center gap-2">
			<span class="text-cyan-500">🔮</span> 今後注目のプロジェクト
		</h2>

		<div class="bg-gradient-to-r from-cyan-50 to-blue-50 dark:from-cyan-900/20 dark:to-blue-900/20 rounded-xl p-6">
			<h3 class="font-bold text-cyan-700 dark:text-cyan-400 mb-3">Ladybird</h3>
			<p class="text-gray-700 dark:text-gray-300 mb-4">
				Chromium/Firefoxに依存しない完全に新しいブラウザエンジンを開発中。
				SerenityOSプロジェクトから派生し、2026年にアルファ版リリース予定。
				ブラウザエンジンの多様性を取り戻す野心的なプロジェクト。
			</p>
			<div class="flex flex-wrap gap-2">
				<span class="bg-cyan-100 text-cyan-800 px-2 py-1 rounded text-xs">独自エンジン</span>
				<span class="bg-cyan-100 text-cyan-800 px-2 py-1 rounded text-xs">2026年予定</span>
				<span class="bg-cyan-100 text-cyan-800 px-2 py-1 rounded text-xs">ブラウザ多様性</span>
			</div>
		</div>
	</section>
</div>
