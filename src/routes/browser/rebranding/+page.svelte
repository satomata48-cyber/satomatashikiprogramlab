<script>
	import CodePreview from '$lib/components/CodePreview.svelte';
</script>

<svelte:head>
	<title>ブラウザのフォーク・リブランディング - さとまたプログラミングラボ</title>
	<meta name="description" content="ChromiumやFirefoxをフォークして独自ブラウザを作る方法。成功事例と技術的な手順を解説" />
</svelte:head>

<div class="max-w-4xl mx-auto">
	<h1 class="text-3xl sm:text-4xl font-bold text-gray-900 dark:text-white mb-6">
		ブラウザのフォーク・リブランディング
	</h1>

	<p class="text-lg text-gray-600 dark:text-gray-300 mb-8">
		ChromiumやFirefoxは オープンソースのため、フォーク（派生版作成）が可能です。
		独自ブラウザを作る方法と、成功しているプロジェクトの戦略を解説します。
	</p>

	<!-- フォークの概要 -->
	<section class="mb-12">
		<h2 class="text-2xl font-bold text-gray-900 dark:text-white mb-4 flex items-center gap-2">
			<span class="text-purple-500">🍴</span> ブラウザフォークとは
		</h2>

		<div class="bg-purple-50 dark:bg-purple-900/20 rounded-xl p-6 mb-6">
			<p class="text-gray-700 dark:text-gray-300 mb-4">
				<strong>フォーク</strong>とは、既存のオープンソースプロジェクトのソースコードをコピーし、
				独自の変更を加えて別のプロジェクトとして開発を続けることです。
			</p>
			<div class="grid md:grid-cols-2 gap-4 text-sm">
				<div class="bg-purple-100 dark:bg-purple-900/40 rounded-lg p-4">
					<h4 class="font-bold text-purple-700 dark:text-purple-400 mb-2">フォークする理由</h4>
					<ul class="space-y-1 text-purple-800 dark:text-purple-200">
						<li>• プライバシー強化（テレメトリ削除）</li>
						<li>• パフォーマンス最適化</li>
						<li>• 独自機能の追加</li>
						<li>• UI/UXの改善</li>
						<li>• 特定ユースケース向けカスタマイズ</li>
					</ul>
				</div>
				<div class="bg-purple-100 dark:bg-purple-900/40 rounded-lg p-4">
					<h4 class="font-bold text-purple-700 dark:text-purple-400 mb-2">維持の課題</h4>
					<ul class="space-y-1 text-purple-800 dark:text-purple-200">
						<li>• セキュリティパッチの適用</li>
						<li>• アップストリームとの同期</li>
						<li>• マージコンフリクトの解決</li>
						<li>• ビルドインフラの維持</li>
						<li>• コミュニティの構築</li>
					</ul>
				</div>
			</div>
		</div>
	</section>

	<!-- Firefoxフォーク -->
	<section class="mb-12">
		<h2 class="text-2xl font-bold text-gray-900 dark:text-white mb-4 flex items-center gap-2">
			<span class="text-orange-500">🦊</span> Firefox をフォークする
		</h2>

		<div class="bg-green-50 dark:bg-green-900/20 border border-green-200 dark:border-green-800 rounded-xl p-4 mb-6">
			<h4 class="font-bold text-green-700 dark:text-green-400 mb-2">✅ Firefoxがフォークしやすい理由</h4>
			<ul class="text-sm text-green-800 dark:text-green-200 space-y-1">
				<li>• <strong>CSSでUIをテーマ変更可能</strong> - Web開発者なら簡単にUI調整</li>
				<li>• <strong>設定ベースのアーキテクチャ</strong> - about:configで多くの動作を変更可能</li>
				<li>• <strong>リパッケージ配布のサポート</strong> - 公式にリブランディングをサポート</li>
				<li>• <strong>DevToolsでブラウザ自体をデバッグ</strong> - 開発が容易</li>
			</ul>
		</div>

		<h3 class="text-xl font-semibold text-gray-800 dark:text-gray-200 mb-4">基本的なフォーク手順</h3>

		<CodePreview
			title="1. Firefox ソースコードの取得"
			code={`# Mercurial をインストール（Firefoxはhgを使用）
sudo apt install mercurial

# mozilla-unified リポジトリをクローン
hg clone https://hg.mozilla.org/mozilla-unified

# または特定バージョン（ESR推奨）
hg clone https://hg.mozilla.org/releases/mozilla-esr115

cd mozilla-unified`}
			language="bash"
		/>

		<CodePreview
			title="2. ビルド環境のセットアップ"
			code={`# 依存関係のインストール（Ubuntu/Debian）
sudo apt install build-essential libgtk-3-dev libdbus-glib-1-dev \\
    libxt-dev python3 python3-pip nodejs npm yasm nasm clang llvm

# bootstrapスクリプトを実行
./mach bootstrap

# mozconfig ファイルを作成
cat > mozconfig << 'EOF'
# ブランディング設定
ac_add_options --with-branding=browser/branding/unofficial
ac_add_options --with-app-name=mybrowser
ac_add_options --with-distribution-id=com.example.mybrowser

# 最適化設定
ac_add_options --enable-optimize
ac_add_options --disable-debug

# テレメトリ無効化
ac_add_options --disable-crashreporter
ac_add_options --disable-telemetry
EOF`}
			language="bash"
		/>

		<CodePreview
			title="3. ブランディングのカスタマイズ"
			code={`# ブランディングディレクトリの構造
browser/branding/mybrowser/
├── branding.nsi          # Windowsインストーラー設定
├── configure.sh          # ビルド設定
├── content/
│   ├── aboutDialog.css   # Aboutダイアログのスタイル
│   └── about.png         # Aboutロゴ
├── locales/
│   └── en-US/
│       └── brand.dtd     # ブランド名の定義
│       └── brand.properties
└── mozicon128.png        # アプリアイコン

# brand.dtd の例
<!ENTITY  brandShortName  "MyBrowser">
<!ENTITY  brandFullName   "MyBrowser Web Browser">
<!ENTITY  vendorShortName "MyCompany">`}
			language="bash"
		/>

		<CodePreview
			title="4. user.js でデフォルト設定をカスタマイズ"
			code={`// browser/app/profile/firefox.js に追加または
// 別途 user.js を配布

// テレメトリ無効化
pref("toolkit.telemetry.enabled", false);
pref("toolkit.telemetry.unified", false);
pref("datareporting.healthreport.uploadEnabled", false);
pref("datareporting.policy.dataSubmissionEnabled", false);

// プライバシー強化
pref("privacy.trackingprotection.enabled", true);
pref("privacy.trackingprotection.socialtracking.enabled", true);
pref("network.cookie.cookieBehavior", 1);

// 検索エンジンをDuckDuckGoに
pref("browser.urlbar.placeholderName", "DuckDuckGo");

// ポケット無効化
pref("extensions.pocket.enabled", false);

// Firefox Sync 無効化（必要に応じて）
pref("identity.fxaccounts.enabled", false);`}
			language="javascript"
		/>

		<CodePreview
			title="5. ビルドと実行"
			code={`# ビルド開始（初回は数時間かかる）
./mach build

# 実行
./mach run

# パッケージ作成
./mach package`}
			language="bash"
		/>
	</section>

	<!-- Chromiumフォーク -->
	<section class="mb-12">
		<h2 class="text-2xl font-bold text-gray-900 dark:text-white mb-4 flex items-center gap-2">
			<span class="text-blue-500">🌐</span> Chromium をフォークする
		</h2>

		<div class="bg-yellow-50 dark:bg-yellow-900/20 border border-yellow-200 dark:border-yellow-800 rounded-xl p-4 mb-6">
			<h4 class="font-bold text-yellow-700 dark:text-yellow-400 mb-2">⚠️ Chromiumフォークの課題</h4>
			<ul class="text-sm text-yellow-800 dark:text-yellow-200 space-y-1">
				<li>• <strong>膨大なコードベース</strong> - 数千万行、ビルドに数時間〜十数時間</li>
				<li>• <strong>頻繁なアップデート</strong> - 毎週のように変更、追従が大変</li>
				<li>• <strong>ブランド名がハードコード</strong> - 多くの場所に分散して記述</li>
				<li>• <strong>必要リソース</strong> - 最低32GB RAM、100GB以上のディスク</li>
			</ul>
		</div>

		<h3 class="text-xl font-semibold text-gray-800 dark:text-gray-200 mb-4">推奨アプローチ</h3>

		<div class="grid md:grid-cols-2 gap-4 mb-6">
			<div class="bg-green-50 dark:bg-green-900/20 rounded-xl p-4">
				<h4 class="font-bold text-green-700 dark:text-green-400 mb-2">✅ Braveのアプローチ</h4>
				<p class="text-sm text-gray-700 dark:text-gray-300">
					最小限のパッチのみを維持。変更の大部分は別ファイルとして追加し、
					Chromiumに「織り込む」形で実装。アップデート追従が容易。
				</p>
			</div>
			<div class="bg-blue-50 dark:bg-blue-900/20 rounded-xl p-4">
				<h4 class="font-bold text-blue-700 dark:text-blue-400 mb-2">📦 自動化アプローチ</h4>
				<p class="text-sm text-gray-700 dark:text-gray-300">
					Chromiumの特定リビジョンを取得し、プログラム的に変更を適用する
					自動化スクリプトを維持。マージコンフリクトを最小化。
				</p>
			</div>
		</div>

		<CodePreview
			title="1. Chromium ソースコードの取得"
			code={`# depot_tools をインストール
git clone https://chromium.googlesource.com/chromium/tools/depot_tools.git
export PATH="$PATH:$PWD/depot_tools"

# ソースディレクトリを作成
mkdir chromium && cd chromium

# fetch（50GB以上ダウンロード、数時間かかる）
fetch --nohooks chromium

# 依存関係をインストール
cd src
./build/install-build-deps.sh
gclient runhooks`}
			language="bash"
		/>

		<CodePreview
			title="2. ビルド設定"
			code={`# GN 設定ファイルを作成
gn gen out/Release --args='
  is_official_build = true
  is_debug = false
  symbol_level = 0
  enable_nacl = false

  # Google API キーを削除
  google_api_key = ""
  google_default_client_id = ""
  google_default_client_secret = ""

  # プロプライエタリコーデックを含める場合
  proprietary_codecs = true
  ffmpeg_branding = "Chrome"
'`}
			language="bash"
		/>

		<CodePreview
			title="3. ブランディング変更（主な箇所）"
			code={`# ブランド名が定義されている主なファイル
chrome/app/chromium_strings.grd
chrome/app/generated_resources.grd
chrome/app/theme/chromium/BRANDING
chrome/installer/util/google_chrome_distribution.cc

# BRANDING ファイルの例
COMPANY_FULLNAME=My Company
COMPANY_SHORTNAME=MyCompany
PRODUCT_FULLNAME=MyBrowser
PRODUCT_SHORTNAME=MyBrowser
PRODUCT_INSTALLER_FULLNAME=MyBrowser Installer
PRODUCT_INSTALLER_SHORTNAME=MyBrowser Installer`}
			language="bash"
		/>

		<CodePreview
			title="4. ビルド実行"
			code={`# ビルド（数時間かかる、並列度を指定）
autoninja -C out/Release chrome

# 実行
./out/Release/chrome

# パッケージ作成（Linux）
autoninja -C out/Release installer`}
			language="bash"
		/>

		<h3 class="text-xl font-semibold text-gray-800 dark:text-gray-200 mb-4 mt-8">簡易リブランディングツール: Rebel</h3>

		<div class="bg-blue-50 dark:bg-blue-900/20 rounded-xl p-6">
			<p class="text-gray-700 dark:text-gray-300 mb-4">
				<strong>Viasat Rebel</strong>は、Chromiumのリブランディングを容易にする代替フォーク。
				ブランド名の変更が少数のファイルで完結するよう設計されています。
			</p>
			<a href="https://github.com/nicotine-it/nicotine" target="_blank" rel="noopener"
			   class="text-blue-600 dark:text-blue-400 hover:underline text-sm">
				参考: Nicotine (Rebel使用例) →
			</a>
		</div>
	</section>

	<!-- 成功事例 -->
	<section class="mb-12">
		<h2 class="text-2xl font-bold text-gray-900 dark:text-white mb-4 flex items-center gap-2">
			<span class="text-green-500">🏆</span> 成功しているフォークの戦略
		</h2>

		<!-- LibreWolf -->
		<div class="bg-white dark:bg-gray-800 rounded-xl shadow-lg p-6 mb-6 border-l-4 border-blue-700">
			<h3 class="text-xl font-bold text-gray-900 dark:text-white mb-2">LibreWolf</h3>
			<p class="text-sm text-gray-500 dark:text-gray-400 mb-4">Firefox ESR ベース</p>

			<div class="grid md:grid-cols-2 gap-4 mb-4">
				<div>
					<h4 class="font-semibold text-gray-800 dark:text-gray-200 mb-2">成功要因</h4>
					<ul class="text-sm text-gray-600 dark:text-gray-400 space-y-1">
						<li>• ESR（延長サポート版）ベースで安定</li>
						<li>• 明確なミッション（プライバシー）</li>
						<li>• 最小限の変更で維持コスト削減</li>
						<li>• コミュニティ主導の開発</li>
					</ul>
				</div>
				<div>
					<h4 class="font-semibold text-gray-800 dark:text-gray-200 mb-2">技術的アプローチ</h4>
					<ul class="text-sm text-gray-600 dark:text-gray-400 space-y-1">
						<li>• 設定ファイル（prefs）による変更が中心</li>
						<li>• ソースコード変更は最小限</li>
						<li>• 自動ビルドパイプライン</li>
						<li>• 複数プラットフォーム対応</li>
					</ul>
				</div>
			</div>
		</div>

		<!-- Brave -->
		<div class="bg-white dark:bg-gray-800 rounded-xl shadow-lg p-6 mb-6 border-l-4 border-orange-600">
			<h3 class="text-xl font-bold text-gray-900 dark:text-white mb-2">Brave</h3>
			<p class="text-sm text-gray-500 dark:text-gray-400 mb-4">Chromium ベース</p>

			<div class="grid md:grid-cols-2 gap-4 mb-4">
				<div>
					<h4 class="font-semibold text-gray-800 dark:text-gray-200 mb-2">成功要因</h4>
					<ul class="text-sm text-gray-600 dark:text-gray-400 space-y-1">
						<li>• 企業としての資金力・開発リソース</li>
						<li>• 明確な差別化（広告ブロック、Rewards）</li>
						<li>• フルタイム開発者チーム</li>
						<li>• 積極的なマーケティング</li>
					</ul>
				</div>
				<div>
					<h4 class="font-semibold text-gray-800 dark:text-gray-200 mb-2">技術的アプローチ</h4>
					<ul class="text-sm text-gray-600 dark:text-gray-400 space-y-1">
						<li>• パッチファイルを最小化</li>
						<li>• 独自コードは別モジュールとして追加</li>
						<li>• Chromiumへの織り込み自動化</li>
						<li>• CI/CDで頻繁なリリース</li>
					</ul>
				</div>
			</div>
		</div>

		<!-- Floorp -->
		<div class="bg-white dark:bg-gray-800 rounded-xl shadow-lg p-6 mb-6 border-l-4 border-purple-500">
			<h3 class="text-xl font-bold text-gray-900 dark:text-white mb-2">Floorp</h3>
			<p class="text-sm text-gray-500 dark:text-gray-400 mb-4">Firefox ESR ベース（日本発）</p>

			<div class="grid md:grid-cols-2 gap-4 mb-4">
				<div>
					<h4 class="font-semibold text-gray-800 dark:text-gray-200 mb-2">成功要因</h4>
					<ul class="text-sm text-gray-600 dark:text-gray-400 space-y-1">
						<li>• 明確なターゲット（パワーユーザー）</li>
						<li>• 積極的な機能追加</li>
						<li>• 活発なコミュニティ</li>
						<li>• 日本語ドキュメント充実</li>
					</ul>
				</div>
				<div>
					<h4 class="font-semibold text-gray-800 dark:text-gray-200 mb-2">技術的アプローチ</h4>
					<ul class="text-sm text-gray-600 dark:text-gray-400 space-y-1">
						<li>• ESRベースで安定性確保</li>
						<li>• CSS/JSによるUI拡張</li>
						<li>• WebExtensions活用</li>
						<li>• GitHub Actionsでビルド自動化</li>
					</ul>
				</div>
			</div>
		</div>

		<!-- Thorium -->
		<div class="bg-white dark:bg-gray-800 rounded-xl shadow-lg p-6 mb-6 border-l-4 border-cyan-500">
			<h3 class="text-xl font-bold text-gray-900 dark:text-white mb-2">Thorium</h3>
			<p class="text-sm text-gray-500 dark:text-gray-400 mb-4">Chromium ベース</p>

			<div class="grid md:grid-cols-2 gap-4 mb-4">
				<div>
					<h4 class="font-semibold text-gray-800 dark:text-gray-200 mb-2">成功要因</h4>
					<ul class="text-sm text-gray-600 dark:text-gray-400 space-y-1">
						<li>• 明確な差別化（最高速度）</li>
						<li>• 実測可能な性能向上（8-38%）</li>
						<li>• 軽量・シンプル志向</li>
						<li>• 複数プラットフォーム対応</li>
					</ul>
				</div>
				<div>
					<h4 class="font-semibold text-gray-800 dark:text-gray-200 mb-2">技術的アプローチ</h4>
					<ul class="text-sm text-gray-600 dark:text-gray-400 space-y-1">
						<li>• コンパイラ最適化フラグ（AVX、SSE4.2）</li>
						<li>• LTO（Link Time Optimization）</li>
						<li>• 不要コンポーネント削除</li>
						<li>• パッチスクリプトによる自動化</li>
					</ul>
				</div>
			</div>
		</div>
	</section>

	<!-- 拡張機能アプローチ -->
	<section class="mb-12">
		<h2 class="text-2xl font-bold text-gray-900 dark:text-white mb-4 flex items-center gap-2">
			<span class="text-yellow-500">💡</span> 代替アプローチ：拡張機能
		</h2>

		<div class="bg-yellow-50 dark:bg-yellow-900/20 rounded-xl p-6">
			<p class="text-gray-700 dark:text-gray-300 mb-4">
				UIの軽微な変更やプライバシー設定のカスタマイズが目的なら、
				ブラウザ全体をフォークする必要はありません。
			</p>

			<div class="grid md:grid-cols-2 gap-4">
				<div class="bg-white dark:bg-gray-800 rounded-lg p-4">
					<h4 class="font-bold text-gray-900 dark:text-white mb-2">Firefox の場合</h4>
					<ul class="text-sm text-gray-600 dark:text-gray-400 space-y-1">
						<li>• <code>user.js</code> でプライバシー設定</li>
						<li>• <code>userChrome.css</code> でUI変更</li>
						<li>• WebExtensionsで機能追加</li>
						<li>• <code>policies.json</code> で企業配布</li>
					</ul>
				</div>
				<div class="bg-white dark:bg-gray-800 rounded-lg p-4">
					<h4 class="font-bold text-gray-900 dark:text-white mb-2">Chrome の場合</h4>
					<ul class="text-sm text-gray-600 dark:text-gray-400 space-y-1">
						<li>• Chrome拡張機能でカスタマイズ</li>
						<li>• ポリシー設定で企業配布</li>
						<li>• Headless Chromeでバックエンド利用</li>
					</ul>
				</div>
			</div>
		</div>
	</section>

	<!-- 持続可能な開発のコツ -->
	<section class="mb-12">
		<h2 class="text-2xl font-bold text-gray-900 dark:text-white mb-4 flex items-center gap-2">
			<span class="text-green-500">♻️</span> 持続可能なフォーク開発のコツ
		</h2>

		<div class="space-y-4">
			<div class="bg-white dark:bg-gray-800 rounded-xl p-4 border border-gray-200 dark:border-gray-700">
				<h4 class="font-bold text-gray-900 dark:text-white mb-2">1. アップストリームからの乖離を最小化</h4>
				<p class="text-sm text-gray-600 dark:text-gray-400">
					セキュリティパッチの適用を容易にするため、ソースコードの変更は最小限に。
					設定ファイルや別モジュールとして追加する方式を優先。
				</p>
			</div>

			<div class="bg-white dark:bg-gray-800 rounded-xl p-4 border border-gray-200 dark:border-gray-700">
				<h4 class="font-bold text-gray-900 dark:text-white mb-2">2. ESR/LTS バージョンの使用</h4>
				<p class="text-sm text-gray-600 dark:text-gray-400">
					最新版ではなく、延長サポート版（Firefox ESR など）をベースにすることで、
					アップデート頻度を下げ、安定したメンテナンスが可能。
				</p>
			</div>

			<div class="bg-white dark:bg-gray-800 rounded-xl p-4 border border-gray-200 dark:border-gray-700">
				<h4 class="font-bold text-gray-900 dark:text-white mb-2">3. CI/CD パイプラインの構築</h4>
				<p class="text-sm text-gray-600 dark:text-gray-400">
					GitHub Actionsなどでビルドとテストを自動化。
					アップストリーム更新時の自動マージとビルド検証を行う。
				</p>
			</div>

			<div class="bg-white dark:bg-gray-800 rounded-xl p-4 border border-gray-200 dark:border-gray-700">
				<h4 class="font-bold text-gray-900 dark:text-white mb-2">4. 明確な差別化ポイント</h4>
				<p class="text-sm text-gray-600 dark:text-gray-400">
					「なぜこのフォークを使うべきか」が明確でないと、ユーザーもコントリビューターも集まらない。
					プライバシー、速度、特定機能など、一点突破の強みを持つ。
				</p>
			</div>

			<div class="bg-white dark:bg-gray-800 rounded-xl p-4 border border-gray-200 dark:border-gray-700">
				<h4 class="font-bold text-gray-900 dark:text-white mb-2">5. コミュニティの構築</h4>
				<p class="text-sm text-gray-600 dark:text-gray-400">
					一人での長期メンテナンスは困難。Discord/Matrixでコミュニティを作り、
					ドキュメント整備、バグ報告、翻訳などで貢献者を増やす。
				</p>
			</div>
		</div>
	</section>

	<!-- まとめ -->
	<section class="mb-12">
		<h2 class="text-2xl font-bold text-gray-900 dark:text-white mb-4">まとめ</h2>

		<div class="bg-gradient-to-r from-purple-50 to-blue-50 dark:from-purple-900/20 dark:to-blue-900/20 rounded-xl p-6">
			<div class="overflow-x-auto">
				<table class="w-full text-sm">
					<thead>
						<tr class="border-b border-gray-200 dark:border-gray-700">
							<th class="px-4 py-2 text-left">項目</th>
							<th class="px-4 py-2 text-left">Firefox</th>
							<th class="px-4 py-2 text-left">Chromium</th>
						</tr>
					</thead>
					<tbody class="divide-y divide-gray-200 dark:divide-gray-700">
						<tr>
							<td class="px-4 py-2 font-medium">フォーク難易度</td>
							<td class="px-4 py-2 text-green-600 dark:text-green-400">比較的容易</td>
							<td class="px-4 py-2 text-red-600 dark:text-red-400">難しい</td>
						</tr>
						<tr>
							<td class="px-4 py-2 font-medium">リソース要件</td>
							<td class="px-4 py-2">16GB RAM〜</td>
							<td class="px-4 py-2">32GB RAM〜</td>
						</tr>
						<tr>
							<td class="px-4 py-2 font-medium">ビルド時間</td>
							<td class="px-4 py-2">1〜3時間</td>
							<td class="px-4 py-2">3〜10時間</td>
						</tr>
						<tr>
							<td class="px-4 py-2 font-medium">UIカスタマイズ</td>
							<td class="px-4 py-2">CSS（容易）</td>
							<td class="px-4 py-2">C++（困難）</td>
						</tr>
						<tr>
							<td class="px-4 py-2 font-medium">おすすめ</td>
							<td class="px-4 py-2">個人・小規模チーム</td>
							<td class="px-4 py-2">企業・大規模チーム</td>
						</tr>
					</tbody>
				</table>
			</div>

			<div class="mt-6 p-4 bg-white dark:bg-gray-800 rounded-lg">
				<p class="text-gray-700 dark:text-gray-300 text-sm">
					<strong>初心者へのおすすめ：</strong>
					まずはFirefoxの <code>user.js</code> と <code>userChrome.css</code> で
					カスタマイズを試し、物足りなくなったらフォークを検討しましょう。
					LibreWolfのソースコードを参考にするのも良い学習になります。
				</p>
			</div>
		</div>
	</section>
</div>
