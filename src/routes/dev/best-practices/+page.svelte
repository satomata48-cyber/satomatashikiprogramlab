<script>
	import CodePreview from '$lib/components/CodePreview.svelte';
</script>

<svelte:head>
	<title>開発ベストプラクティス | さとまたラボ</title>
</svelte:head>

<article>
	<h1 class="text-3xl font-bold mb-2">開発ベストプラクティス</h1>
	<p class="text-lg text-gray-600 dark:text-gray-400 mb-8">
		プロフェッショナルな開発現場で使われる手法を学ぶ
	</p>

	<!-- 概要 -->
	<section class="mb-12">
		<h2 id="overview" class="text-xl font-bold mb-4">プロの開発現場とは</h2>

		<div class="p-6 rounded-xl bg-gradient-to-r from-blue-50 to-purple-50 dark:from-blue-900/20 dark:to-purple-900/20 border border-blue-200 dark:border-blue-800 mb-6">
			<p class="text-lg text-blue-800 dark:text-blue-200 mb-4">
				<strong>お金をもらって開発する</strong> = 品質・信頼性・チームワークが求められる
			</p>
			<p class="text-sm text-blue-700 dark:text-blue-300">
				個人開発とは異なり、複数人での開発、本番環境の安定性、セキュリティ、
				継続的なメンテナンスを考慮した開発手法が必要です。
			</p>
		</div>

		<div class="p-4 rounded-lg bg-gray-100 dark:bg-gray-800 mb-6">
			<p class="font-semibold text-gray-800 dark:text-gray-200 mb-3">DevOps市場の成長</p>
			<p class="text-sm text-gray-600 dark:text-gray-400">
				DevOps市場は2028年までに<strong>255億ドル（約3.8兆円）</strong>規模に成長予測。
				CI/CDは「あると良い」から「必須」へと進化しています。
			</p>
		</div>
	</section>

	<!-- Git ワークフロー -->
	<section class="mb-12">
		<h2 id="git-workflow" class="text-xl font-bold mb-4">Git ワークフロー</h2>

		<p class="text-gray-700 dark:text-gray-300 mb-4">
			チーム開発では、Gitを使ったバージョン管理が必須です。
			ブランチ戦略を決めて、変更履歴を追跡・管理します。
		</p>

		<!-- GitHub Flow -->
		<div class="mb-8">
			<h3 class="text-lg font-semibold mb-4 flex items-center gap-2">
				<span class="w-8 h-8 bg-gray-800 dark:bg-white text-white dark:text-gray-800 rounded-full flex items-center justify-center text-sm">1</span>
				GitHub Flow（シンプル）
			</h3>

			<div class="p-4 rounded-lg bg-gray-50 dark:bg-gray-800 mb-4">
				<div class="flex flex-col items-center gap-2 font-mono text-sm">
					<div class="flex items-center gap-4">
						<div class="px-4 py-2 bg-blue-500 text-white rounded">main</div>
						<span class="text-gray-400">← 本番環境（常にデプロイ可能）</span>
					</div>
					<div class="text-gray-400">↑ Pull Request + レビュー</div>
					<div class="flex items-center gap-4">
						<div class="px-4 py-2 bg-green-500 text-white rounded">feature/xxx</div>
						<span class="text-gray-400">← 機能開発用ブランチ</span>
					</div>
				</div>
			</div>

			<CodePreview
				title="GitHub Flowの流れ"
				description="シンプルで小規模チーム向け"
				language="bash"
				code={`# 1. mainから新しいブランチを作成
git checkout main
git pull origin main
git checkout -b feature/add-login

# 2. 機能を開発・コミット
git add .
git commit -m "feat: ログイン機能を追加"

# 3. リモートにプッシュ
git push origin feature/add-login

# 4. GitHubでPull Requestを作成
#    → チームメンバーがコードレビュー
#    → 承認されたらmainにマージ

# 5. マージ後、自動でデプロイ（CI/CD）`}
				previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div style="color:#6a9955;">// シンプルで覚えやすい</div><div style="color:#6a9955;">// 小〜中規模チームに最適</div></div>`}
			/>
		</div>

		<!-- Git Flow -->
		<div class="mb-8">
			<h3 class="text-lg font-semibold mb-4 flex items-center gap-2">
				<span class="w-8 h-8 bg-purple-600 text-white rounded-full flex items-center justify-center text-sm">2</span>
				Git Flow（大規模向け）
			</h3>

			<div class="p-4 rounded-lg bg-gray-50 dark:bg-gray-800 mb-4">
				<div class="space-y-2 font-mono text-xs">
					<div class="flex items-center gap-3">
						<div class="w-24 px-2 py-1 bg-blue-600 text-white rounded text-center">main</div>
						<span class="text-gray-500">本番環境</span>
					</div>
					<div class="flex items-center gap-3">
						<div class="w-24 px-2 py-1 bg-purple-600 text-white rounded text-center">develop</div>
						<span class="text-gray-500">開発の統合ブランチ</span>
					</div>
					<div class="flex items-center gap-3">
						<div class="w-24 px-2 py-1 bg-green-600 text-white rounded text-center">feature/*</div>
						<span class="text-gray-500">機能開発</span>
					</div>
					<div class="flex items-center gap-3">
						<div class="w-24 px-2 py-1 bg-yellow-600 text-white rounded text-center">release/*</div>
						<span class="text-gray-500">リリース準備</span>
					</div>
					<div class="flex items-center gap-3">
						<div class="w-24 px-2 py-1 bg-red-600 text-white rounded text-center">hotfix/*</div>
						<span class="text-gray-500">緊急バグ修正</span>
					</div>
				</div>
			</div>

			<div class="p-4 rounded-lg bg-amber-50 dark:bg-amber-900/20 border border-amber-200 dark:border-amber-800">
				<p class="font-semibold text-amber-800 dark:text-amber-200 mb-2">使い分け</p>
				<p class="text-sm text-amber-700 dark:text-amber-300">
					<strong>GitHub Flow</strong>：スタートアップ、アジャイル開発、頻繁にデプロイするチーム<br>
					<strong>Git Flow</strong>：大企業、リリースサイクルが決まっているプロジェクト
				</p>
			</div>
		</div>

		<!-- コミットメッセージ -->
		<div class="mb-8">
			<h3 class="text-lg font-semibold mb-4">コミットメッセージの規約</h3>

			<CodePreview
				title="Conventional Commits"
				description="意味のあるコミット履歴を作る"
				language="text"
				code={`# フォーマット
<type>: <description>

# type の種類
feat:     新機能
fix:      バグ修正
docs:     ドキュメント変更
style:    フォーマット変更（動作に影響なし）
refactor: リファクタリング
test:     テスト追加・修正
chore:    ビルド設定等の変更

# 例
feat: ユーザー登録機能を追加
fix: ログイン時のエラーハンドリングを修正
docs: READMEにインストール手順を追加
refactor: 認証ロジックを共通化`}
				previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div style="color:#6a9955;">// 履歴を見るだけで何をしたかわかる</div><div style="color:#6a9955;">// 自動でCHANGELOG生成も可能</div></div>`}
			/>
		</div>
	</section>

	<!-- CI/CD -->
	<section class="mb-12">
		<h2 id="cicd" class="text-xl font-bold mb-4">CI/CD（継続的インテグレーション/デプロイ）</h2>

		<div class="p-4 rounded-lg bg-blue-50 dark:bg-blue-900/20 border border-blue-200 dark:border-blue-800 mb-6">
			<p class="font-semibold text-blue-800 dark:text-blue-200 mb-2">CI/CDとは？</p>
			<p class="text-sm text-blue-700 dark:text-blue-300">
				<strong>CI（継続的インテグレーション）</strong>：コードをプッシュするたびに自動でテスト・ビルド<br>
				<strong>CD（継続的デプロイ）</strong>：テストに通ったら自動で本番環境にデプロイ
			</p>
		</div>

		<!-- CI/CDの流れ -->
		<div class="mb-8">
			<h3 class="text-lg font-semibold mb-4">CI/CDパイプラインの流れ</h3>

			<div class="p-4 rounded-lg bg-gray-50 dark:bg-gray-800 mb-4">
				<div class="flex flex-wrap items-center justify-center gap-2 text-sm">
					<div class="px-3 py-2 bg-blue-500 text-white rounded">コードをプッシュ</div>
					<span class="text-gray-400">→</span>
					<div class="px-3 py-2 bg-yellow-500 text-white rounded">自動ビルド</div>
					<span class="text-gray-400">→</span>
					<div class="px-3 py-2 bg-purple-500 text-white rounded">自動テスト</div>
					<span class="text-gray-400">→</span>
					<div class="px-3 py-2 bg-orange-500 text-white rounded">セキュリティスキャン</div>
					<span class="text-gray-400">→</span>
					<div class="px-3 py-2 bg-green-500 text-white rounded">自動デプロイ</div>
				</div>
			</div>
		</div>

		<!-- GitHub Actions -->
		<div class="mb-8">
			<h3 class="text-lg font-semibold mb-4">GitHub Actions の例</h3>

			<CodePreview
				title=".github/workflows/deploy.yml"
				description="SvelteKitのCI/CD設定例"
				language="yaml"
				code={`name: Deploy to Cloudflare Pages

on:
  push:
    branches: [main]  # mainにプッシュされたら実行
  pull_request:
    branches: [main]  # PRが作られたら実行

jobs:
  build-and-test:
    runs-on: ubuntu-latest

    steps:
      # 1. コードを取得
      - name: Checkout
        uses: actions/checkout@v4

      # 2. Node.jsをセットアップ
      - name: Setup Node.js
        uses: actions/setup-node@v4
        with:
          node-version: '20'
          cache: 'npm'

      # 3. 依存関係をインストール
      - name: Install dependencies
        run: npm ci

      # 4. Lintチェック（コード品質）
      - name: Lint
        run: npm run lint

      # 5. 型チェック（TypeScript）
      - name: Type check
        run: npm run check

      # 6. テスト実行
      - name: Run tests
        run: npm run test

      # 7. ビルド
      - name: Build
        run: npm run build

      # 8. Cloudflare Pagesにデプロイ（mainブランチのみ）
      - name: Deploy to Cloudflare Pages
        if: github.ref == 'refs/heads/main'
        uses: cloudflare/pages-action@v1
        with:
          apiToken: \${{ secrets.CLOUDFLARE_API_TOKEN }}
          accountId: \${{ secrets.CLOUDFLARE_ACCOUNT_ID }}
          projectName: my-sveltekit-app
          directory: .svelte-kit/cloudflare`}
			/>

			<div class="mt-4 p-4 rounded-lg bg-green-50 dark:bg-green-900/20 border border-green-200 dark:border-green-800">
				<p class="font-semibold text-green-800 dark:text-green-200 mb-2">自動化のメリット</p>
				<ul class="text-sm text-green-700 dark:text-green-300 space-y-1">
					<li>・人的ミスを防ぐ（手動デプロイでのミスがなくなる）</li>
					<li>・高速なフィードバック（プッシュ後すぐにエラーがわかる）</li>
					<li>・一貫性のある品質（毎回同じチェックが走る）</li>
				</ul>
			</div>
		</div>

		<!-- CI/CDツール -->
		<div class="mb-8">
			<h3 class="text-lg font-semibold mb-4">人気のCI/CDツール（2025年）</h3>

			<div class="grid md:grid-cols-2 gap-4">
				<div class="p-4 rounded-lg border border-gray-200 dark:border-gray-700">
					<p class="font-semibold text-gray-800 dark:text-gray-200 mb-2">GitHub Actions</p>
					<p class="text-sm text-gray-600 dark:text-gray-400">
						GitHubと完全統合。YAMLで設定。個人〜大規模まで対応。無料枠も充実。
					</p>
				</div>
				<div class="p-4 rounded-lg border border-gray-200 dark:border-gray-700">
					<p class="font-semibold text-gray-800 dark:text-gray-200 mb-2">GitLab CI/CD</p>
					<p class="text-sm text-gray-600 dark:text-gray-400">
						GitLabに組み込み。セルフホスト可能。エンタープライズ向け機能が充実。
					</p>
				</div>
				<div class="p-4 rounded-lg border border-gray-200 dark:border-gray-700">
					<p class="font-semibold text-gray-800 dark:text-gray-200 mb-2">CircleCI</p>
					<p class="text-sm text-gray-600 dark:text-gray-400">
						高速なビルド。Docker対応。GitHub/GitLab/Bitbucketと連携。
					</p>
				</div>
				<div class="p-4 rounded-lg border border-gray-200 dark:border-gray-700">
					<p class="font-semibold text-gray-800 dark:text-gray-200 mb-2">Jenkins</p>
					<p class="text-sm text-gray-600 dark:text-gray-400">
						オープンソース。高いカスタマイズ性。大企業での採用多数。
					</p>
				</div>
			</div>
		</div>
	</section>

	<!-- テスト -->
	<section class="mb-12">
		<h2 id="testing" class="text-xl font-bold mb-4">テスト戦略</h2>

		<p class="text-gray-700 dark:text-gray-300 mb-4">
			プロの開発では、テストは必須です。バグを早期に発見し、品質を保証します。
		</p>

		<!-- テストピラミッド -->
		<div class="mb-8">
			<h3 class="text-lg font-semibold mb-4">テストピラミッド</h3>

			<div class="p-4 rounded-lg bg-gray-50 dark:bg-gray-800 mb-4">
				<div class="flex flex-col items-center">
					<div class="w-32 h-16 bg-red-400 text-white flex items-center justify-center text-sm rounded-t-lg">
						E2Eテスト
					</div>
					<div class="w-48 h-16 bg-yellow-400 text-gray-800 flex items-center justify-center text-sm">
						統合テスト
					</div>
					<div class="w-64 h-16 bg-green-400 text-white flex items-center justify-center text-sm rounded-b-lg">
						ユニットテスト
					</div>
				</div>
				<p class="text-xs text-gray-500 text-center mt-3">
					下に行くほど数が多く、高速で、低コスト
				</p>
			</div>

			<div class="space-y-4">
				<div class="p-4 rounded-lg bg-green-50 dark:bg-green-900/20 border border-green-200 dark:border-green-800">
					<p class="font-semibold text-green-800 dark:text-green-200 mb-2">ユニットテスト（Unit Test）</p>
					<p class="text-sm text-green-700 dark:text-green-300">
						関数やコンポーネント単体のテスト。高速で大量に実行可能。
						テストの70-80%を占めるべき。
					</p>
					<p class="text-xs text-green-600 dark:text-green-400 mt-2">
						ツール: Vitest, Jest, Testing Library
					</p>
				</div>

				<div class="p-4 rounded-lg bg-yellow-50 dark:bg-yellow-900/20 border border-yellow-200 dark:border-yellow-800">
					<p class="font-semibold text-yellow-800 dark:text-yellow-200 mb-2">統合テスト（Integration Test）</p>
					<p class="text-sm text-yellow-700 dark:text-yellow-300">
						複数のモジュールやAPIとの連携をテスト。
						データベース接続やAPI呼び出しを含む。
					</p>
					<p class="text-xs text-yellow-600 dark:text-yellow-400 mt-2">
						ツール: Vitest, Supertest
					</p>
				</div>

				<div class="p-4 rounded-lg bg-red-50 dark:bg-red-900/20 border border-red-200 dark:border-red-800">
					<p class="font-semibold text-red-800 dark:text-red-200 mb-2">E2Eテスト（End-to-End Test）</p>
					<p class="text-sm text-red-700 dark:text-red-300">
						実際のブラウザでユーザーの操作をシミュレート。
						時間がかかるので、重要なフローのみテスト。
					</p>
					<p class="text-xs text-red-600 dark:text-red-400 mt-2">
						ツール: Playwright, Cypress
					</p>
				</div>
			</div>
		</div>

		<!-- テストコード例 -->
		<div class="mb-8">
			<h3 class="text-lg font-semibold mb-4">テストコードの例</h3>

			<CodePreview
				title="Vitestでユニットテスト"
				description="SvelteKitでの例"
				language="typescript"
				code={`// src/lib/utils.ts
export function formatPrice(price: number): string {
  return price.toLocaleString('ja-JP') + '円';
}

export function calculateTax(price: number, rate = 0.1): number {
  return Math.floor(price * rate);
}

// src/lib/utils.test.ts
import { describe, it, expect } from 'vitest';
import { formatPrice, calculateTax } from './utils';

describe('formatPrice', () => {
  it('数値を日本円形式にフォーマットする', () => {
    expect(formatPrice(1000)).toBe('1,000円');
    expect(formatPrice(1234567)).toBe('1,234,567円');
  });

  it('0の場合も正しくフォーマットする', () => {
    expect(formatPrice(0)).toBe('0円');
  });
});

describe('calculateTax', () => {
  it('デフォルト税率10%で計算する', () => {
    expect(calculateTax(1000)).toBe(100);
    expect(calculateTax(1234)).toBe(123);
  });

  it('税率を指定できる', () => {
    expect(calculateTax(1000, 0.08)).toBe(80);
  });
});`}
			/>

			<CodePreview
				title="Playwrightでe2eテスト"
				description="ブラウザ操作を自動化"
				language="typescript"
				code={`// tests/login.spec.ts
import { test, expect } from '@playwright/test';

test.describe('ログイン機能', () => {
  test('正しい認証情報でログインできる', async ({ page }) => {
    // ログインページにアクセス
    await page.goto('/login');

    // フォームに入力
    await page.fill('input[name="email"]', 'test@example.com');
    await page.fill('input[name="password"]', 'password123');

    // ログインボタンをクリック
    await page.click('button[type="submit"]');

    // ダッシュボードにリダイレクトされることを確認
    await expect(page).toHaveURL('/dashboard');
    await expect(page.locator('h1')).toContainText('ダッシュボード');
  });

  test('間違ったパスワードでエラーが表示される', async ({ page }) => {
    await page.goto('/login');
    await page.fill('input[name="email"]', 'test@example.com');
    await page.fill('input[name="password"]', 'wrongpassword');
    await page.click('button[type="submit"]');

    // エラーメッセージが表示されることを確認
    await expect(page.locator('.error-message')).toBeVisible();
  });
});`}
			/>
		</div>
	</section>

	<!-- セキュリティ -->
	<section class="mb-12">
		<h2 id="security" class="text-xl font-bold mb-4">セキュリティ（Shift-Left）</h2>

		<div class="p-4 rounded-lg bg-red-50 dark:bg-red-900/20 border border-red-200 dark:border-red-800 mb-6">
			<p class="font-semibold text-red-800 dark:text-red-200 mb-2">Shift-Left とは？</p>
			<p class="text-sm text-red-700 dark:text-red-300">
				セキュリティチェックを開発の「早い段階（左側）」で行うこと。
				リリース直前に脆弱性が見つかると修正コストが大きくなるため、
				開発初期から継続的にチェックします。
			</p>
		</div>

		<div class="space-y-4">
			<div class="p-4 rounded-lg bg-gray-50 dark:bg-gray-800">
				<p class="font-semibold text-gray-800 dark:text-gray-200 mb-2">依存関係の脆弱性チェック</p>
				<code class="text-sm bg-gray-200 dark:bg-gray-700 px-2 py-1 rounded">npm audit</code>
				<p class="text-sm text-gray-600 dark:text-gray-400 mt-2">
					npmパッケージに既知の脆弱性がないかチェック。CI/CDで自動実行。
				</p>
			</div>

			<div class="p-4 rounded-lg bg-gray-50 dark:bg-gray-800">
				<p class="font-semibold text-gray-800 dark:text-gray-200 mb-2">シークレット管理</p>
				<p class="text-sm text-gray-600 dark:text-gray-400">
					APIキーやパスワードはコードにハードコードしない。
					環境変数（<code>.env</code>）やCI/CDのSecretsを使用。
				</p>
			</div>

			<div class="p-4 rounded-lg bg-gray-50 dark:bg-gray-800">
				<p class="font-semibold text-gray-800 dark:text-gray-200 mb-2">コードスキャン</p>
				<p class="text-sm text-gray-600 dark:text-gray-400">
					GitHub Dependabot、Snyk、SonarQubeなどで自動スキャン。
					脆弱性が見つかると自動でPRを作成。
				</p>
			</div>
		</div>
	</section>

	<!-- コードレビュー -->
	<section class="mb-12">
		<h2 id="code-review" class="text-xl font-bold mb-4">コードレビュー</h2>

		<p class="text-gray-700 dark:text-gray-300 mb-4">
			Pull Requestを通じて、他のメンバーがコードをレビューします。
			品質向上だけでなく、知識共有の場にもなります。
		</p>

		<div class="grid md:grid-cols-2 gap-4">
			<div class="p-4 rounded-lg bg-green-50 dark:bg-green-900/20 border border-green-200 dark:border-green-800">
				<p class="font-semibold text-green-800 dark:text-green-200 mb-2">レビューで見るポイント</p>
				<ul class="text-sm text-green-700 dark:text-green-300 space-y-1">
					<li>・ロジックに問題はないか</li>
					<li>・コードは読みやすいか</li>
					<li>・テストは十分か</li>
					<li>・セキュリティ上の問題はないか</li>
					<li>・パフォーマンスに影響はないか</li>
				</ul>
			</div>
			<div class="p-4 rounded-lg bg-blue-50 dark:bg-blue-900/20 border border-blue-200 dark:border-blue-800">
				<p class="font-semibold text-blue-800 dark:text-blue-200 mb-2">良いレビューのコツ</p>
				<ul class="text-sm text-blue-700 dark:text-blue-300 space-y-1">
					<li>・批判ではなく改善提案をする</li>
					<li>・具体的に指摘する</li>
					<li>・良い点も褒める</li>
					<li>・小さなPRにする（レビューしやすい）</li>
					<li>・自動化できるチェックは自動化</li>
				</ul>
			</div>
		</div>
	</section>

	<!-- まとめ -->
	<section class="mb-10">
		<h2 id="summary" class="text-xl font-bold mb-4">まとめ</h2>

		<div class="space-y-4">
			<div class="p-4 rounded-lg bg-gray-100 dark:bg-gray-800">
				<p class="font-semibold text-gray-800 dark:text-gray-200">Git ワークフロー</p>
				<p class="text-sm text-gray-600 dark:text-gray-400">
					ブランチ戦略を決め、PRとコードレビューで品質を担保。
				</p>
			</div>
			<div class="p-4 rounded-lg bg-blue-50 dark:bg-blue-900/20 border border-blue-200 dark:border-blue-800">
				<p class="font-semibold text-blue-800 dark:text-blue-200">CI/CD</p>
				<p class="text-sm text-blue-700 dark:text-blue-300">
					プッシュするたびに自動でテスト・ビルド・デプロイ。
				</p>
			</div>
			<div class="p-4 rounded-lg bg-green-50 dark:bg-green-900/20 border border-green-200 dark:border-green-800">
				<p class="font-semibold text-green-800 dark:text-green-200">テスト</p>
				<p class="text-sm text-green-700 dark:text-green-300">
					ユニット → 統合 → E2E のピラミッド構造で品質保証。
				</p>
			</div>
			<div class="p-4 rounded-lg bg-red-50 dark:bg-red-900/20 border border-red-200 dark:border-red-800">
				<p class="font-semibold text-red-800 dark:text-red-200">セキュリティ</p>
				<p class="text-sm text-red-700 dark:text-red-300">
					Shift-Leftで早期発見。依存関係の脆弱性を常にチェック。
				</p>
			</div>
		</div>
	</section>

	<!-- ナビゲーション -->
	<div class="flex justify-between pt-6 border-t border-gray-200 dark:border-gray-700">
		<a href="/dev/my-workflow" class="inline-flex items-center gap-2 px-4 py-2 rounded-lg border border-gray-300 dark:border-gray-600 hover:bg-gray-100 dark:hover:bg-gray-800 transition-colors">
			<svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
				<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 19l-7-7 7-7" />
			</svg>
			前へ：私の開発フロー
		</a>
		<a href="/" class="inline-flex items-center gap-2 px-4 py-2 rounded-lg bg-primary-600 text-white hover:bg-primary-700 transition-colors">
			ホームに戻る
			<svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
				<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M3 12l2-2m0 0l7-7 7 7M5 10v10a1 1 0 001 1h3m10-11l2 2m-2-2v10a1 1 0 01-1 1h-3m-6 0a1 1 0 001-1v-4a1 1 0 011-1h2a1 1 0 011 1v4a1 1 0 001 1m-6 0h6" />
			</svg>
		</a>
	</div>
</article>
