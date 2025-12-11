<script>
	import CodePreview from '$lib/components/CodePreview.svelte';
</script>

<svelte:head>
	<title>WindowsからLinuxへの移行 - Linux | さとまたラボ</title>
</svelte:head>

<article>
	<h1 class="text-3xl font-bold mb-2">WindowsからLinuxへの移行</h1>
	<p class="text-lg text-gray-600 dark:text-gray-400 mb-8">
		Windows PCをLinuxに移行するための完全ロードマップ
	</p>

	<!-- 概要 -->
	<section class="mb-10">
		<h2 id="overview" class="text-xl font-bold mb-4">移行の全体像</h2>

		<div class="p-6 rounded-xl bg-gradient-to-r from-blue-50 to-green-50 dark:from-blue-900/20 dark:to-green-900/20 border border-blue-200 dark:border-blue-800 mb-6">
			<div class="flex items-center gap-4 mb-4">
				<span class="text-3xl">🪟</span>
				<span class="text-2xl">→</span>
				<span class="text-3xl">🐧</span>
			</div>
			<p class="text-gray-700 dark:text-gray-300">
				WindowsがインストールされているPCに、Linux（Ubuntu、Linux Mint、Zorin OS等）をインストールして移行する手順を解説します。<strong>デュアルブート</strong>（WindowsとLinuxを共存）と<strong>完全移行</strong>（Windowsを削除）の両方に対応。
			</p>
		</div>

		<!-- ロードマップ -->
		<div class="p-4 rounded-lg bg-amber-50 dark:bg-amber-900/20 border border-amber-200 dark:border-amber-800 mb-6">
			<p class="font-semibold text-amber-800 dark:text-amber-200 mb-3">移行ロードマップ（所要時間目安）</p>
			<div class="flex flex-wrap gap-2 text-sm">
				<span class="px-3 py-1 bg-amber-200 dark:bg-amber-800 rounded-full">1. 準備（30分）</span>
				<span class="text-amber-600">→</span>
				<span class="px-3 py-1 bg-amber-200 dark:bg-amber-800 rounded-full">2. バックアップ（1〜2時間）</span>
				<span class="text-amber-600">→</span>
				<span class="px-3 py-1 bg-amber-200 dark:bg-amber-800 rounded-full">3. USB作成（15分）</span>
				<span class="text-amber-600">→</span>
				<span class="px-3 py-1 bg-amber-200 dark:bg-amber-800 rounded-full">4. インストール（30分）</span>
				<span class="text-amber-600">→</span>
				<span class="px-3 py-1 bg-amber-200 dark:bg-amber-800 rounded-full">5. 初期設定（1時間）</span>
			</div>
		</div>
	</section>

	<!-- Phase 1: 準備 -->
	<section class="mb-10">
		<h2 id="phase1" class="text-xl font-bold mb-4">
			<span class="inline-flex items-center justify-center w-8 h-8 bg-blue-500 text-white rounded-full text-sm mr-2">1</span>
			準備フェーズ
		</h2>

		<!-- ディストロ選び -->
		<div class="p-4 rounded-lg bg-green-50 dark:bg-green-900/20 border border-green-200 dark:border-green-800 mb-6">
			<p class="font-semibold text-green-800 dark:text-green-200 mb-3">Step 1-1: Linuxディストロを選ぶ</p>
			<p class="text-sm text-green-700 dark:text-green-300 mb-4">
				Windows移行者におすすめのGUI付きディストロ：
			</p>
			<div class="grid grid-cols-1 md:grid-cols-3 gap-3">
				<div class="p-3 bg-white dark:bg-gray-800 rounded border border-green-300 dark:border-green-700">
					<p class="font-bold text-green-600">🌿 Linux Mint</p>
					<p class="text-xs text-gray-600 dark:text-gray-400 mt-1">最もおすすめ。Windowsに似た操作感で違和感なく使える。</p>
					<a href="https://linuxmint.com/download.php" target="_blank" rel="noopener" class="text-xs text-blue-500 hover:underline">ダウンロード →</a>
				</div>
				<div class="p-3 bg-white dark:bg-gray-800 rounded border border-green-300 dark:border-green-700">
					<p class="font-bold text-orange-600">🟠 Ubuntu</p>
					<p class="text-xs text-gray-600 dark:text-gray-400 mt-1">最も有名で情報が多い。困った時に検索しやすい。</p>
					<a href="https://ubuntu.com/download/desktop" target="_blank" rel="noopener" class="text-xs text-blue-500 hover:underline">ダウンロード →</a>
				</div>
				<div class="p-3 bg-white dark:bg-gray-800 rounded border border-green-300 dark:border-green-700">
					<p class="font-bold text-blue-600">💎 Zorin OS</p>
					<p class="text-xs text-gray-600 dark:text-gray-400 mt-1">Windows 11風のUIを選択可能。移行者向けに設計。</p>
					<a href="https://zorin.com/os/download/" target="_blank" rel="noopener" class="text-xs text-blue-500 hover:underline">ダウンロード →</a>
				</div>
			</div>
		</div>

		<!-- 必要なもの -->
		<div class="p-4 rounded-lg bg-blue-50 dark:bg-blue-900/20 border border-blue-200 dark:border-blue-800 mb-6">
			<p class="font-semibold text-blue-800 dark:text-blue-200 mb-3">Step 1-2: 必要なものを準備</p>
			<ul class="text-sm text-blue-700 dark:text-blue-300 space-y-2">
				<li class="flex items-start gap-2">
					<span class="text-green-500">✓</span>
					<div>
						<strong>USBメモリ（8GB以上）</strong><br>
						<span class="text-xs text-gray-500">インストール用のブータブルUSBを作成します</span>
					</div>
				</li>
				<li class="flex items-start gap-2">
					<span class="text-green-500">✓</span>
					<div>
						<strong>Linux ISOファイル</strong><br>
						<span class="text-xs text-gray-500">選んだディストロの公式サイトからダウンロード（2〜4GB）</span>
					</div>
				</li>
				<li class="flex items-start gap-2">
					<span class="text-green-500">✓</span>
					<div>
						<strong>バックアップ用の外付けHDD/SSD</strong><br>
						<span class="text-xs text-gray-500">大切なデータを退避させるため</span>
					</div>
				</li>
				<li class="flex items-start gap-2">
					<span class="text-green-500">✓</span>
					<div>
						<strong>安定したインターネット接続</strong><br>
						<span class="text-xs text-gray-500">ISOダウンロードとインストール後のアップデートに必要</span>
					</div>
				</li>
			</ul>
		</div>

		<!-- PCの確認 -->
		<div class="p-4 rounded-lg bg-gray-50 dark:bg-gray-800/50 border border-gray-200 dark:border-gray-700 mb-6">
			<p class="font-semibold text-gray-800 dark:text-gray-200 mb-3">Step 1-3: PCのスペックを確認</p>
			<div class="text-sm text-gray-700 dark:text-gray-300">
				<p class="mb-2">Windowsで確認する方法：</p>
				<ol class="list-decimal list-inside space-y-1 mb-4">
					<li><code class="bg-gray-200 dark:bg-gray-700 px-1 rounded">Win + R</code> → <code class="bg-gray-200 dark:bg-gray-700 px-1 rounded">msinfo32</code> と入力してEnter</li>
					<li>「システム情報」でCPU、RAM、BIOSモードを確認</li>
				</ol>
				<div class="p-3 bg-white dark:bg-gray-800 rounded">
					<p class="font-medium mb-2">最低要件（Ubuntu/Mint/Zorin）</p>
					<ul class="space-y-1 text-xs">
						<li>CPU: 2GHz デュアルコア以上</li>
						<li>RAM: 4GB以上（8GB推奨）</li>
						<li>ストレージ: 25GB以上の空き容量</li>
						<li>BIOSモード: UEFI推奨（Legacyも可）</li>
					</ul>
				</div>
			</div>
		</div>

		<!-- インストール方法の選択 -->
		<div class="p-4 rounded-lg bg-purple-50 dark:bg-purple-900/20 border border-purple-200 dark:border-purple-800">
			<p class="font-semibold text-purple-800 dark:text-purple-200 mb-3">Step 1-4: インストール方法を決める</p>
			<div class="grid grid-cols-1 md:grid-cols-2 gap-4 text-sm">
				<div class="p-3 bg-white dark:bg-gray-800 rounded border-2 border-green-400">
					<p class="font-bold text-green-600 mb-2">A. デュアルブート（推奨）</p>
					<p class="text-gray-600 dark:text-gray-400 text-xs mb-2">WindowsとLinuxを共存させる</p>
					<ul class="text-xs space-y-1">
						<li>✅ Windowsを残したまま試せる</li>
						<li>✅ 起動時にOS選択可能</li>
						<li>✅ 戻りたくなったらWindowsを使える</li>
						<li>⚠️ ディスク容量を分割する必要あり</li>
					</ul>
				</div>
				<div class="p-3 bg-white dark:bg-gray-800 rounded border border-gray-300 dark:border-gray-600">
					<p class="font-bold text-red-600 mb-2">B. 完全移行</p>
					<p class="text-gray-600 dark:text-gray-400 text-xs mb-2">Windowsを削除してLinuxのみ</p>
					<ul class="text-xs space-y-1">
						<li>✅ ディスク全体をLinuxで使用</li>
						<li>✅ シンプルな構成</li>
						<li>⚠️ Windowsには戻れない</li>
						<li>⚠️ 事前にデータ完全バックアップ必須</li>
					</ul>
				</div>
			</div>
		</div>
	</section>

	<!-- Phase 2: バックアップ -->
	<section class="mb-10">
		<h2 id="phase2" class="text-xl font-bold mb-4">
			<span class="inline-flex items-center justify-center w-8 h-8 bg-red-500 text-white rounded-full text-sm mr-2">2</span>
			バックアップフェーズ（超重要！）
		</h2>

		<div class="p-4 rounded-lg bg-red-50 dark:bg-red-900/20 border border-red-200 dark:border-red-800 mb-6">
			<p class="font-semibold text-red-800 dark:text-red-200 mb-2">⚠️ 必ずバックアップを取ってください</p>
			<p class="text-sm text-red-700 dark:text-red-300">
				インストール中のミスやパーティション操作でデータが消える可能性があります。後悔する前に、必ず大切なデータを外部に退避させてください。
			</p>
		</div>

		<div class="space-y-4">
			<div class="p-4 rounded-lg bg-gray-50 dark:bg-gray-800/50 border border-gray-200 dark:border-gray-700">
				<p class="font-semibold text-gray-800 dark:text-gray-200 mb-3">バックアップすべきデータ</p>
				<div class="grid grid-cols-1 md:grid-cols-2 gap-4 text-sm">
					<div>
						<p class="font-medium text-blue-600 dark:text-blue-400 mb-2">📁 ユーザーフォルダ</p>
						<ul class="text-xs text-gray-600 dark:text-gray-400 space-y-1">
							<li>• ドキュメント</li>
							<li>• ピクチャ</li>
							<li>• ビデオ</li>
							<li>• ミュージック</li>
							<li>• ダウンロード</li>
							<li>• デスクトップ</li>
						</ul>
					</div>
					<div>
						<p class="font-medium text-green-600 dark:text-green-400 mb-2">🔑 重要データ</p>
						<ul class="text-xs text-gray-600 dark:text-gray-400 space-y-1">
							<li>• ブラウザのブックマーク</li>
							<li>• パスワードマネージャーのデータ</li>
							<li>• メールデータ（ローカル保存の場合）</li>
							<li>• ゲームのセーブデータ</li>
							<li>• ソフトウェアのライセンスキー</li>
							<li>• SSH鍵、証明書など</li>
						</ul>
					</div>
				</div>
			</div>

			<div class="p-4 rounded-lg bg-gray-50 dark:bg-gray-800/50 border border-gray-200 dark:border-gray-700">
				<p class="font-semibold text-gray-800 dark:text-gray-200 mb-3">バックアップ方法</p>
				<div class="space-y-3 text-sm">
					<div class="p-3 bg-white dark:bg-gray-800 rounded">
						<p class="font-medium">方法1: 外付けHDD/SSDにコピー（推奨）</p>
						<p class="text-xs text-gray-500 mt-1">エクスプローラーでドラッグ&ドロップ。最も確実。</p>
					</div>
					<div class="p-3 bg-white dark:bg-gray-800 rounded">
						<p class="font-medium">方法2: クラウドストレージ</p>
						<p class="text-xs text-gray-500 mt-1">Google Drive、OneDrive、Dropbox等にアップロード。</p>
					</div>
					<div class="p-3 bg-white dark:bg-gray-800 rounded">
						<p class="font-medium">方法3: Windowsバックアップ機能</p>
						<p class="text-xs text-gray-500 mt-1">設定 → 更新とセキュリティ → バックアップ</p>
					</div>
				</div>
			</div>
		</div>
	</section>

	<!-- Phase 3: ブータブルUSB作成 -->
	<section class="mb-10">
		<h2 id="phase3" class="text-xl font-bold mb-4">
			<span class="inline-flex items-center justify-center w-8 h-8 bg-orange-500 text-white rounded-full text-sm mr-2">3</span>
			ブータブルUSB作成
		</h2>

		<div class="p-4 rounded-lg bg-orange-50 dark:bg-orange-900/20 border border-orange-200 dark:border-orange-800 mb-6">
			<p class="font-semibold text-orange-800 dark:text-orange-200 mb-2">Rufusを使用（Windows用）</p>
			<p class="text-sm text-orange-700 dark:text-orange-300">
				<a href="https://rufus.ie/" target="_blank" rel="noopener" class="underline font-medium">Rufus</a>は、ISOファイルからブータブルUSBを作成するWindows用の無料ツールです。
			</p>
		</div>

		<div class="space-y-4">
			<div class="p-4 rounded-lg bg-gray-50 dark:bg-gray-800/50 border border-gray-200 dark:border-gray-700">
				<p class="font-semibold text-gray-800 dark:text-gray-200 mb-3">Step 3-1: Rufusをダウンロード</p>
				<ol class="text-sm text-gray-700 dark:text-gray-300 list-decimal list-inside space-y-2">
					<li><a href="https://rufus.ie/" target="_blank" rel="noopener" class="text-blue-500 hover:underline">rufus.ie</a> にアクセス</li>
					<li>「Rufus x.x」または「Rufus x.x Portable」をダウンロード</li>
					<li>ダウンロードした.exeを実行（インストール不要）</li>
				</ol>
			</div>

			<div class="p-4 rounded-lg bg-gray-50 dark:bg-gray-800/50 border border-gray-200 dark:border-gray-700">
				<p class="font-semibold text-gray-800 dark:text-gray-200 mb-3">Step 3-2: USBを作成</p>
				<ol class="text-sm text-gray-700 dark:text-gray-300 list-decimal list-inside space-y-2">
					<li>USBメモリをPCに挿入</li>
					<li>Rufusを起動</li>
					<li><strong>デバイス</strong>：USBメモリを選択</li>
					<li><strong>ブートの種類</strong>：「選択」をクリックしてダウンロードしたISOファイルを指定</li>
					<li><strong>パーティション構成</strong>：GPT（UEFI）を選択（古いPCはMBR）</li>
					<li><strong>ファイルシステム</strong>：FAT32（デフォルトでOK）</li>
					<li>「スタート」をクリック</li>
					<li>警告が出たら「OK」を押して続行</li>
					<li>完了まで待つ（5〜10分）</li>
				</ol>
			</div>

			<div class="p-3 rounded bg-amber-100 dark:bg-amber-900/30 text-sm text-amber-800 dark:text-amber-200">
				⚠️ USBメモリの中身は全て消去されます。大切なデータがないか確認してください。
			</div>
		</div>
	</section>

	<!-- Phase 4: インストール -->
	<section class="mb-10">
		<h2 id="phase4" class="text-xl font-bold mb-4">
			<span class="inline-flex items-center justify-center w-8 h-8 bg-green-500 text-white rounded-full text-sm mr-2">4</span>
			Linuxインストール
		</h2>

		<!-- BIOS設定 -->
		<div class="p-4 rounded-lg bg-gray-50 dark:bg-gray-800/50 border border-gray-200 dark:border-gray-700 mb-6">
			<p class="font-semibold text-gray-800 dark:text-gray-200 mb-3">Step 4-1: USBから起動する</p>
			<div class="text-sm text-gray-700 dark:text-gray-300 space-y-3">
				<div class="p-3 bg-white dark:bg-gray-800 rounded">
					<p class="font-medium mb-2">方法A: ブートメニューから起動（簡単）</p>
					<ol class="list-decimal list-inside space-y-1 text-xs">
						<li>PCを再起動</li>
						<li>起動直後に<strong>ブートメニューキー</strong>を連打
							<div class="mt-1 p-2 bg-gray-100 dark:bg-gray-900 rounded">
								<span class="font-mono">F12</span>（多くのPC）、
								<span class="font-mono">F9</span>（HP）、
								<span class="font-mono">F2</span>（ASUS）、
								<span class="font-mono">Esc</span>（一部）
							</div>
						</li>
						<li>ブートメニューが表示されたらUSBを選択</li>
					</ol>
				</div>

				<div class="p-3 bg-white dark:bg-gray-800 rounded">
					<p class="font-medium mb-2">方法B: BIOS/UEFI設定から変更</p>
					<ol class="list-decimal list-inside space-y-1 text-xs">
						<li>PCを再起動</li>
						<li>起動直後に<strong>BIOS/UEFIキー</strong>を連打（<span class="font-mono">F2</span>、<span class="font-mono">Del</span>、<span class="font-mono">F10</span>など）</li>
						<li>Boot（起動）設定でUSBを最優先に変更</li>
						<li>保存して再起動</li>
					</ol>
				</div>

				<div class="p-3 bg-blue-100 dark:bg-blue-900/30 rounded">
					<p class="font-medium text-blue-800 dark:text-blue-200 mb-1">Windows 11からの起動方法</p>
					<p class="text-xs text-blue-700 dark:text-blue-300">
						設定 → システム → 回復 → 「今すぐ再起動」→「デバイスの使用」→ USBを選択
					</p>
				</div>
			</div>
		</div>

		<!-- Live環境 -->
		<div class="p-4 rounded-lg bg-gray-50 dark:bg-gray-800/50 border border-gray-200 dark:border-gray-700 mb-6">
			<p class="font-semibold text-gray-800 dark:text-gray-200 mb-3">Step 4-2: Live環境で試す</p>
			<div class="text-sm text-gray-700 dark:text-gray-300">
				<p class="mb-3">USBから起動すると、インストールせずにLinuxを試せる「Live環境」が立ち上がります。</p>
				<ul class="list-disc list-inside space-y-1">
					<li>Wi-Fiが繋がるか確認</li>
					<li>画面表示が正常か確認</li>
					<li>音が出るか確認</li>
					<li>ブラウザ等を触ってみる</li>
				</ul>
				<p class="mt-3 text-green-600 dark:text-green-400 font-medium">
					問題なければインストールに進みましょう！
				</p>
			</div>
		</div>

		<!-- インストール手順 -->
		<div class="p-4 rounded-lg bg-green-50 dark:bg-green-900/20 border border-green-200 dark:border-green-800 mb-6">
			<p class="font-semibold text-green-800 dark:text-green-200 mb-3">Step 4-3: インストール実行</p>
			<div class="text-sm text-green-700 dark:text-green-300 space-y-4">
				<p>デスクトップにある「Install」アイコンをダブルクリック</p>

				<div class="space-y-3">
					<div class="p-3 bg-white dark:bg-gray-800 rounded">
						<p class="font-medium">1. 言語選択</p>
						<p class="text-xs text-gray-500">「日本語」を選択</p>
					</div>

					<div class="p-3 bg-white dark:bg-gray-800 rounded">
						<p class="font-medium">2. キーボードレイアウト</p>
						<p class="text-xs text-gray-500">「Japanese」または使用しているキーボードを選択</p>
					</div>

					<div class="p-3 bg-white dark:bg-gray-800 rounded">
						<p class="font-medium">3. Wi-Fi接続（有線の場合はスキップ）</p>
						<p class="text-xs text-gray-500">ネットワークに接続</p>
					</div>

					<div class="p-3 bg-white dark:bg-gray-800 rounded">
						<p class="font-medium">4. インストールの種類（重要！）</p>
						<div class="mt-2 space-y-2">
							<div class="p-2 bg-green-100 dark:bg-green-900/30 rounded text-xs">
								<strong>「Windowsとは別にインストール」</strong>（デュアルブート）<br>
								→ Windowsを残したまま、空き領域にLinuxをインストール
							</div>
							<div class="p-2 bg-red-100 dark:bg-red-900/30 rounded text-xs">
								<strong>「ディスクを削除してインストール」</strong>（完全移行）<br>
								→ Windowsを消去してLinuxのみインストール
							</div>
							<div class="p-2 bg-gray-100 dark:bg-gray-700 rounded text-xs">
								<strong>「その他」</strong>（上級者向け）<br>
								→ パーティションを手動で設定
							</div>
						</div>
					</div>

					<div class="p-3 bg-white dark:bg-gray-800 rounded">
						<p class="font-medium">5. タイムゾーン</p>
						<p class="text-xs text-gray-500">「Tokyo」を選択</p>
					</div>

					<div class="p-3 bg-white dark:bg-gray-800 rounded">
						<p class="font-medium">6. ユーザー作成</p>
						<ul class="text-xs text-gray-500 list-disc list-inside mt-1">
							<li>名前（表示名）</li>
							<li>コンピュータ名（ホスト名）</li>
							<li>ユーザー名（ログインID）</li>
							<li>パスワード（sudo時にも使用）</li>
						</ul>
					</div>

					<div class="p-3 bg-white dark:bg-gray-800 rounded">
						<p class="font-medium">7. インストール開始</p>
						<p class="text-xs text-gray-500">「インストール」をクリックして待つ（15〜30分）</p>
					</div>
				</div>
			</div>
		</div>

		<div class="p-4 rounded-lg bg-blue-50 dark:bg-blue-900/20 border border-blue-200 dark:border-blue-800">
			<p class="font-semibold text-blue-800 dark:text-blue-200 mb-2">Step 4-4: 再起動</p>
			<p class="text-sm text-blue-700 dark:text-blue-300">
				インストール完了後、「今すぐ再起動」をクリック。USBメモリを抜くよう指示されたら抜いてEnter。
			</p>
		</div>
	</section>

	<!-- Phase 5: 初期設定 -->
	<section class="mb-10">
		<h2 id="phase5" class="text-xl font-bold mb-4">
			<span class="inline-flex items-center justify-center w-8 h-8 bg-purple-500 text-white rounded-full text-sm mr-2">5</span>
			初期設定フェーズ
		</h2>

		<div class="space-y-4">
			<div class="p-4 rounded-lg bg-gray-50 dark:bg-gray-800/50 border border-gray-200 dark:border-gray-700">
				<p class="font-semibold text-gray-800 dark:text-gray-200 mb-3">Step 5-1: システムアップデート</p>
				<CodePreview
					title="ターミナルでアップデート"
					description="最新の状態にする"
					language="bash"
					code={`# パッケージリストを更新
sudo apt update

# パッケージをアップグレード
sudo apt upgrade -y

# 再起動（カーネル更新時）
sudo reboot`}
					previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:12px;"><div style="color:#4ec9b0;">243 packages upgraded</div></div>`}
				/>
				<p class="text-xs text-gray-500 mt-2">
					または GUI: 「ソフトウェアの更新」アプリを使用
				</p>
			</div>

			<div class="p-4 rounded-lg bg-gray-50 dark:bg-gray-800/50 border border-gray-200 dark:border-gray-700">
				<p class="font-semibold text-gray-800 dark:text-gray-200 mb-3">Step 5-2: 日本語入力の設定</p>
				<div class="text-sm text-gray-700 dark:text-gray-300">
					<p class="mb-2">Ubuntu/Mintの場合：</p>
					<ol class="list-decimal list-inside space-y-1 text-xs">
						<li>設定 → 「言語サポート」を開く</li>
						<li>「言語のインストール」で日本語を確認</li>
						<li>キーボード入力に「Fcitx」または「IBus」を選択</li>
						<li>再ログインして <code class="bg-gray-200 dark:bg-gray-700 px-1 rounded">半角/全角</code> キーで切り替え</li>
					</ol>
				</div>
			</div>

			<div class="p-4 rounded-lg bg-gray-50 dark:bg-gray-800/50 border border-gray-200 dark:border-gray-700">
				<p class="font-semibold text-gray-800 dark:text-gray-200 mb-3">Step 5-3: 必要なソフトウェアをインストール</p>
				<CodePreview
					title="よく使うソフトのインストール"
					description="apt または ソフトウェアセンターから"
					language="bash"
					code={`# ブラウザ（Chrome）
wget https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb
sudo dpkg -i google-chrome-stable_current_amd64.deb

# VS Code
sudo snap install code --classic

# Git
sudo apt install git

# Node.js（nvm経由）
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.0/install.sh | bash
source ~/.bashrc
nvm install 20

# VLC（動画プレイヤー）
sudo apt install vlc

# GIMP（画像編集）
sudo apt install gimp`}
					previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:12px;"><div style="color:#4ec9b0;">✓ Chrome installed</div><div style="color:#4ec9b0;">✓ VS Code installed</div></div>`}
				/>
			</div>

			<div class="p-4 rounded-lg bg-gray-50 dark:bg-gray-800/50 border border-gray-200 dark:border-gray-700">
				<p class="font-semibold text-gray-800 dark:text-gray-200 mb-3">Step 5-4: バックアップデータを復元</p>
				<ul class="text-sm text-gray-700 dark:text-gray-300 list-disc list-inside space-y-1">
					<li>外付けHDDを接続してファイルをコピー</li>
					<li>ドキュメント、写真等を適切なフォルダに配置</li>
					<li>ブラウザにブックマークをインポート</li>
				</ul>
			</div>
		</div>
	</section>

	<!-- Windows代替ソフト -->
	<section class="mb-10">
		<h2 id="alternatives" class="text-xl font-bold mb-4">Windowsソフトの代替</h2>

		<div class="overflow-x-auto">
			<table class="w-full text-sm">
				<thead>
					<tr class="border-b border-gray-200 dark:border-gray-700 bg-gray-50 dark:bg-gray-800">
						<th class="text-left py-3 px-4">用途</th>
						<th class="text-left py-3 px-4">Windows</th>
						<th class="text-left py-3 px-4">Linux代替</th>
					</tr>
				</thead>
				<tbody>
					<tr class="border-b border-gray-200 dark:border-gray-700">
						<td class="py-3 px-4">ブラウザ</td>
						<td class="py-3 px-4">Chrome / Edge</td>
						<td class="py-3 px-4 text-green-600">Chrome / Firefox（そのまま使える）</td>
					</tr>
					<tr class="border-b border-gray-200 dark:border-gray-700">
						<td class="py-3 px-4">オフィス</td>
						<td class="py-3 px-4">Microsoft Office</td>
						<td class="py-3 px-4 text-green-600">LibreOffice / OnlyOffice / Google Docs</td>
					</tr>
					<tr class="border-b border-gray-200 dark:border-gray-700">
						<td class="py-3 px-4">画像編集</td>
						<td class="py-3 px-4">Photoshop</td>
						<td class="py-3 px-4 text-green-600">GIMP / Krita</td>
					</tr>
					<tr class="border-b border-gray-200 dark:border-gray-700">
						<td class="py-3 px-4">動画編集</td>
						<td class="py-3 px-4">Premiere Pro</td>
						<td class="py-3 px-4 text-green-600">DaVinci Resolve / Kdenlive</td>
					</tr>
					<tr class="border-b border-gray-200 dark:border-gray-700">
						<td class="py-3 px-4">動画プレイヤー</td>
						<td class="py-3 px-4">Windows Media Player</td>
						<td class="py-3 px-4 text-green-600">VLC</td>
					</tr>
					<tr class="border-b border-gray-200 dark:border-gray-700">
						<td class="py-3 px-4">コードエディタ</td>
						<td class="py-3 px-4">VS Code</td>
						<td class="py-3 px-4 text-green-600">VS Code（そのまま使える）</td>
					</tr>
					<tr class="border-b border-gray-200 dark:border-gray-700">
						<td class="py-3 px-4">ターミナル</td>
						<td class="py-3 px-4">PowerShell / cmd</td>
						<td class="py-3 px-4 text-green-600">GNOME Terminal / Konsole</td>
					</tr>
					<tr class="border-b border-gray-200 dark:border-gray-700">
						<td class="py-3 px-4">ゲーム</td>
						<td class="py-3 px-4">Steam / Epic</td>
						<td class="py-3 px-4 text-green-600">Steam（Proton対応）/ Lutris</td>
					</tr>
					<tr>
						<td class="py-3 px-4">Windowsアプリ</td>
						<td class="py-3 px-4">—</td>
						<td class="py-3 px-4 text-amber-600">Wine / Bottles（互換レイヤー）</td>
					</tr>
				</tbody>
			</table>
		</div>
	</section>

	<!-- トラブルシューティング -->
	<section class="mb-10">
		<h2 id="troubleshooting" class="text-xl font-bold mb-4">よくあるトラブルと解決策</h2>

		<div class="space-y-4">
			<div class="p-4 rounded-lg bg-gray-50 dark:bg-gray-800/50 border border-gray-200 dark:border-gray-700">
				<p class="font-semibold text-gray-800 dark:text-gray-200 mb-2">❓ USBから起動できない</p>
				<ul class="text-sm text-gray-700 dark:text-gray-300 list-disc list-inside space-y-1">
					<li>Secure Bootを無効にする（BIOS設定）</li>
					<li>Fast Boot（高速起動）を無効にする</li>
					<li>別のUSBポート（USB 2.0）を試す</li>
					<li>Rufusで再度USBを作り直す</li>
				</ul>
			</div>

			<div class="p-4 rounded-lg bg-gray-50 dark:bg-gray-800/50 border border-gray-200 dark:border-gray-700">
				<p class="font-semibold text-gray-800 dark:text-gray-200 mb-2">❓ Wi-Fiが繋がらない</p>
				<ul class="text-sm text-gray-700 dark:text-gray-300 list-disc list-inside space-y-1">
					<li>有線LANで接続してドライバをインストール</li>
					<li>「追加のドライバー」アプリを確認</li>
					<li>無線LANアダプタのメーカーを検索してドライバを探す</li>
				</ul>
			</div>

			<div class="p-4 rounded-lg bg-gray-50 dark:bg-gray-800/50 border border-gray-200 dark:border-gray-700">
				<p class="font-semibold text-gray-800 dark:text-gray-200 mb-2">❓ 画面がおかしい（解像度、ちらつき）</p>
				<ul class="text-sm text-gray-700 dark:text-gray-300 list-disc list-inside space-y-1">
					<li>NVIDIAの場合：「追加のドライバー」からプロプライエタリドライバをインストール</li>
					<li>設定 → ディスプレイで解像度を変更</li>
				</ul>
			</div>

			<div class="p-4 rounded-lg bg-gray-50 dark:bg-gray-800/50 border border-gray-200 dark:border-gray-700">
				<p class="font-semibold text-gray-800 dark:text-gray-200 mb-2">❓ デュアルブートでWindowsが起動しない</p>
				<ul class="text-sm text-gray-700 dark:text-gray-300 list-disc list-inside space-y-1">
					<li><code class="bg-gray-200 dark:bg-gray-700 px-1 rounded">sudo update-grub</code> を実行</li>
					<li>GRUBメニューが表示されない場合は起動時にShiftキーを押し続ける</li>
				</ul>
			</div>
		</div>
	</section>

	<!-- チェックリスト -->
	<section class="mb-10">
		<h2 id="checklist" class="text-xl font-bold mb-4">移行完了チェックリスト</h2>

		<div class="p-4 rounded-lg bg-green-50 dark:bg-green-900/20 border border-green-200 dark:border-green-800">
			<ul class="text-sm text-green-700 dark:text-green-300 space-y-2">
				<li class="flex items-center gap-2"><span class="text-lg">☐</span> Linuxが正常に起動する</li>
				<li class="flex items-center gap-2"><span class="text-lg">☐</span> Wi-Fi / 有線LANが繋がる</li>
				<li class="flex items-center gap-2"><span class="text-lg">☐</span> 画面表示が正常</li>
				<li class="flex items-center gap-2"><span class="text-lg">☐</span> 音が出る</li>
				<li class="flex items-center gap-2"><span class="text-lg">☐</span> 日本語入力ができる</li>
				<li class="flex items-center gap-2"><span class="text-lg">☐</span> システムアップデート完了</li>
				<li class="flex items-center gap-2"><span class="text-lg">☐</span> 必要なソフトをインストール</li>
				<li class="flex items-center gap-2"><span class="text-lg">☐</span> バックアップデータを復元</li>
				<li class="flex items-center gap-2"><span class="text-lg">☐</span> （デュアルブートの場合）Windowsも起動できる</li>
			</ul>
		</div>
	</section>

	<!-- まとめ -->
	<section class="mb-10">
		<h2 id="summary" class="text-xl font-bold mb-4">まとめ</h2>

		<div class="p-4 rounded-lg bg-blue-50 dark:bg-blue-900/20 border border-blue-200 dark:border-blue-800">
			<ul class="text-sm text-blue-700 dark:text-blue-300 list-disc list-inside space-y-2">
				<li><strong>準備</strong>：ディストロ選び、USBメモリ、バックアップ用HDD</li>
				<li><strong>バックアップ</strong>：必ず全データを外部に退避</li>
				<li><strong>USB作成</strong>：Rufusでブータブル作成</li>
				<li><strong>インストール</strong>：デュアルブートか完全移行かを選択</li>
				<li><strong>初期設定</strong>：アップデート、日本語入力、ソフト導入</li>
				<li>困ったら「Ubuntu 〇〇 できない」で検索すると情報が見つかる</li>
			</ul>
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
		<a href="/linux/popular-2025" class="inline-flex items-center gap-2 px-4 py-2 rounded-lg bg-primary-600 text-white hover:bg-primary-700 transition-colors">
			次へ：2025年人気のOS
			<svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
				<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 5l7 7-7 7" />
			</svg>
		</a>
	</div>
</article>
