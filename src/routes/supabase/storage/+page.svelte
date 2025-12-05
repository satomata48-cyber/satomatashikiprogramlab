<script>
	import CodePreview from '$lib/components/CodePreview.svelte';
</script>

<svelte:head>
	<title>Supabase ストレージ | さとまたラボ</title>
</svelte:head>

<article>
	<h1 class="text-3xl font-bold mb-2">ストレージ</h1>
	<p class="text-lg text-gray-600 dark:text-gray-400 mb-8">
		画像やファイルをSupabaseに保存する
	</p>

	<!-- ストレージとは -->
	<section class="mb-10">
		<h2 id="overview" class="text-xl font-bold mb-4">Supabase Storageとは</h2>

		<div class="p-6 rounded-xl bg-emerald-50 dark:bg-emerald-900/20 border border-emerald-200 dark:border-emerald-800 mb-6">
			<p class="text-emerald-800 dark:text-emerald-200 mb-4">
				<strong>S3互換のオブジェクトストレージ</strong>
			</p>
			<ul class="text-sm text-emerald-700 dark:text-emerald-300 space-y-1">
				<li>・画像、動画、PDFなどあらゆるファイルを保存</li>
				<li>・バケット単位でアクセス制御</li>
				<li>・CDN経由で高速配信</li>
				<li>・画像のリサイズ・変換機能</li>
			</ul>
		</div>
	</section>

	<!-- バケット作成 -->
	<section class="mb-10">
		<h2 id="bucket" class="text-xl font-bold mb-4">バケットを作成</h2>

		<div class="p-4 rounded-lg bg-gray-50 dark:bg-gray-800 mb-4">
			<p class="font-semibold text-gray-800 dark:text-gray-200 mb-2">ダッシュボードで作成</p>
			<p class="text-sm text-gray-600 dark:text-gray-400">
				Storage → New Bucket で作成できます。
			</p>
			<ul class="text-sm text-gray-600 dark:text-gray-400 mt-2 space-y-1">
				<li>・<strong>Public</strong>：誰でもアクセス可能（プロフィール画像など）</li>
				<li>・<strong>Private</strong>：認証が必要（個人ファイルなど）</li>
			</ul>
		</div>

		<CodePreview
			title="コードでバケットを作成"
			description="APIでバケットを作成（オプション）"
			language="typescript"
			code={`// 公開バケットを作成
const { data, error } = await supabase.storage.createBucket('avatars', {
  public: true,
  fileSizeLimit: 1024 * 1024 * 2,  // 2MB制限
  allowedMimeTypes: ['image/png', 'image/jpeg', 'image/gif']
})

// プライベートバケットを作成
const { data, error } = await supabase.storage.createBucket('documents', {
  public: false
})`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div style="color:#6a9955;">// 通常はダッシュボードで作成</div></div>`}
		/>
	</section>

	<!-- アップロード -->
	<section class="mb-10">
		<h2 id="upload" class="text-xl font-bold mb-4">ファイルをアップロード</h2>

		<CodePreview
			title="ファイルをアップロード"
			description="upload() でファイルを保存"
			language="typescript"
			code={`// ファイルをアップロード
const file = event.target.files[0]  // inputから取得

const { data, error } = await supabase.storage
  .from('avatars')  // バケット名
  .upload(\`public/\${file.name}\`, file, {
    cacheControl: '3600',  // キャッシュ時間（秒）
    upsert: false  // 同名ファイルがあればエラー（trueで上書き）
  })

if (error) {
  console.error('アップロードエラー:', error.message)
} else {
  console.log('アップロード成功:', data.path)
}

// ユニークなファイル名で保存
const fileName = \`\${Date.now()}_\${file.name}\`
await supabase.storage
  .from('avatars')
  .upload(\`users/\${userId}/\${fileName}\`, file)`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div><span style="color:#dcdcaa;">.upload(path, file)</span></div><div style="color:#6a9955;">// pathはバケット内のパス</div></div>`}
		/>

		<CodePreview
			title="SvelteKitでのアップロードフォーム"
			description="ファイル選択とアップロード"
			language="svelte"
			code={`<script lang="ts">
  import { supabase } from '$lib/supabase'

  let uploading = $state(false)
  let avatarUrl = $state('')

  async function handleUpload(event: Event) {
    const input = event.target as HTMLInputElement
    const file = input.files?.[0]
    if (!file) return

    uploading = true

    // ファイルをアップロード
    const fileName = \`\${Date.now()}_\${file.name}\`
    const { data, error } = await supabase.storage
      .from('avatars')
      .upload(fileName, file)

    if (error) {
      alert('アップロードエラー: ' + error.message)
    } else {
      // 公開URLを取得
      const { data: urlData } = supabase.storage
        .from('avatars')
        .getPublicUrl(data.path)

      avatarUrl = urlData.publicUrl
    }

    uploading = false
  }
</script>

<input type="file" accept="image/*" onchange={handleUpload} />
{#if uploading}
  <p>アップロード中...</p>
{/if}
{#if avatarUrl}
  <img src={avatarUrl} alt="avatar" />
{/if}`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div style="color:#6a9955;">// ファイル選択→アップロード→表示</div></div>`}
		/>
	</section>

	<!-- URLの取得 -->
	<section class="mb-10">
		<h2 id="get-url" class="text-xl font-bold mb-4">URLを取得</h2>

		<CodePreview
			title="公開URLを取得"
			description="publicバケットの場合"
			language="typescript"
			code={`// 公開URLを取得（publicバケット）
const { data } = supabase.storage
  .from('avatars')
  .getPublicUrl('public/image.png')

console.log(data.publicUrl)
// https://xxx.supabase.co/storage/v1/object/public/avatars/public/image.png

// 画像変換オプション付き
const { data } = supabase.storage
  .from('avatars')
  .getPublicUrl('public/image.png', {
    transform: {
      width: 200,
      height: 200,
      resize: 'cover'  // 'contain', 'fill' なども可
    }
  })`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div style="color:#6a9955;">// 自動でリサイズしてくれる</div></div>`}
		/>

		<CodePreview
			title="署名付きURLを取得"
			description="privateバケットの場合"
			language="typescript"
			code={`// 署名付きURL（有効期限付き）を取得
const { data, error } = await supabase.storage
  .from('documents')
  .createSignedUrl('private/document.pdf', 60)  // 60秒間有効

if (data) {
  console.log(data.signedUrl)
  // 一定時間だけアクセス可能なURL
}

// 複数ファイルの署名付きURLを一括取得
const { data } = await supabase.storage
  .from('documents')
  .createSignedUrls(['file1.pdf', 'file2.pdf'], 60)`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div style="color:#6a9955;">// 期限付きでセキュア</div></div>`}
		/>
	</section>

	<!-- ダウンロード・削除 -->
	<section class="mb-10">
		<h2 id="download-delete" class="text-xl font-bold mb-4">ダウンロード・削除</h2>

		<CodePreview
			title="ファイルをダウンロード"
			description="download() でBlobを取得"
			language="typescript"
			code={`// ファイルをダウンロード
const { data, error } = await supabase.storage
  .from('documents')
  .download('private/document.pdf')

if (data) {
  // Blobとして取得
  const url = URL.createObjectURL(data)
  // ダウンロードリンクを作成
  const a = document.createElement('a')
  a.href = url
  a.download = 'document.pdf'
  a.click()
}`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div style="color:#6a9955;">// Blobとして取得</div></div>`}
		/>

		<CodePreview
			title="ファイルを削除"
			description="remove() でファイルを削除"
			language="typescript"
			code={`// 1ファイルを削除
const { error } = await supabase.storage
  .from('avatars')
  .remove(['public/old-image.png'])

// 複数ファイルを削除
const { error } = await supabase.storage
  .from('avatars')
  .remove([
    'public/image1.png',
    'public/image2.png',
    'public/image3.png'
  ])`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div style="color:#f14c4c;">⚠️ 削除は取り消せない</div></div>`}
		/>
	</section>

	<!-- ファイル一覧 -->
	<section class="mb-10">
		<h2 id="list" class="text-xl font-bold mb-4">ファイル一覧を取得</h2>

		<CodePreview
			title="ファイル一覧を取得"
			description="list() でファイル一覧を取得"
			language="typescript"
			code={`// フォルダ内のファイル一覧を取得
const { data, error } = await supabase.storage
  .from('avatars')
  .list('public', {
    limit: 100,
    offset: 0,
    sortBy: { column: 'name', order: 'asc' }
  })

if (data) {
  data.forEach(file => {
    console.log(file.name)       // ファイル名
    console.log(file.id)         // ファイルID
    console.log(file.created_at) // 作成日時
    console.log(file.metadata)   // メタデータ
  })
}`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div style="color:#6a9955;">// フォルダ内のファイルを列挙</div></div>`}
		/>
	</section>

	<!-- ナビゲーション -->
	<div class="flex justify-between pt-6 border-t border-gray-200 dark:border-gray-700">
		<a href="/supabase/auth" class="inline-flex items-center gap-2 px-4 py-2 rounded-lg border border-gray-300 dark:border-gray-600 hover:bg-gray-100 dark:hover:bg-gray-800 transition-colors">
			<svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
				<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 19l-7-7 7-7" />
			</svg>
			前へ：認証
		</a>
		<a href="/cloudflare/intro" class="inline-flex items-center gap-2 px-4 py-2 rounded-lg bg-primary-600 text-white hover:bg-primary-700 transition-colors">
			次へ：Cloudflare
			<svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
				<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 5l7 7-7 7" />
			</svg>
		</a>
	</div>
</article>
