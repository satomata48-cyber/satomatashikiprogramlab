<script>
	import CodePreview from '$lib/components/CodePreview.svelte';
</script>

<svelte:head>
	<title>HTML フォーム | さとまたラボ</title>
</svelte:head>

<article>
	<h1 class="text-3xl font-bold mb-2">フォーム</h1>
	<p class="text-lg text-gray-600 dark:text-gray-400 mb-8">
		ユーザーからの入力を受け取る仕組み
	</p>

	<!-- フォームとは何か -->
	<section class="mb-10">
		<h2 id="what-is" class="text-xl font-bold mb-4">フォームとは？</h2>

		<div class="p-6 rounded-xl bg-blue-50 dark:bg-blue-900/20 border border-blue-200 dark:border-blue-800 mb-6">
			<p class="text-blue-800 dark:text-blue-200 mb-4">
				<strong>日常での例え：</strong>紙のアンケート用紙
			</p>
			<div class="grid grid-cols-1 md:grid-cols-2 gap-4 text-sm">
				<div class="p-3 bg-white dark:bg-gray-800 rounded-lg">
					<div class="font-semibold text-blue-700 dark:text-blue-300 mb-2">紙のアンケート</div>
					<p class="text-gray-600 dark:text-gray-400">
						名前を書く欄<br>
						選択肢にチェック<br>
						「提出」ボタンを押す
					</p>
				</div>
				<div class="p-3 bg-white dark:bg-gray-800 rounded-lg">
					<div class="font-semibold text-blue-700 dark:text-blue-300 mb-2">Webフォーム</div>
					<p class="text-gray-600 dark:text-gray-400">
						テキスト入力欄（input）<br>
						チェックボックス・ラジオボタン<br>
						「送信」ボタン
					</p>
				</div>
			</div>
		</div>

		<div class="p-4 rounded-lg bg-amber-50 dark:bg-amber-900/20 border border-amber-200 dark:border-amber-800 mb-6">
			<p class="font-semibold text-amber-800 dark:text-amber-200">なぜフォームが必要？</p>
			<p class="text-sm text-amber-700 dark:text-amber-300 mt-2">
				Webページは通常「一方通行」で情報を見るだけ。<br>
				フォームがあると、ユーザーが<strong>情報を送信</strong>できる。<br>
				→ ログイン、会員登録、問い合わせ、検索など
			</p>
		</div>
	</section>

	<!-- 基本構造 -->
	<section class="mb-10">
		<h2 id="basic" class="text-xl font-bold mb-4">フォームの基本構造</h2>

		<CodePreview
			title="フォームの3つの要素"
			description="form、入力欄、送信ボタン"
			language="html"
			code={`<!-- form: フォーム全体を囲む「箱」 -->
<!-- action: 送信先のURL -->
<!-- method: 送信方法（POST/GET） -->
<form action="/submit" method="POST">

  <!-- label: 入力欄の説明（「名前:」の部分） -->
  <!-- for: どのinputと紐づくか（idと同じ値） -->
  <label for="name">名前:</label>

  <!-- input: 実際の入力欄 -->
  <!-- id: labelと紐づける識別子 -->
  <!-- name: サーバーに送る時のデータ名 -->
  <input type="text" id="name" name="name">

  <!-- button type="submit": 送信ボタン -->
  <button type="submit">送信</button>

</form>`}
			previewHtml={`<form style="display:flex;flex-direction:column;gap:8px;max-width:250px;">
<label>名前:</label>
<input type="text" style="padding:8px;border:1px solid #d1d5db;border-radius:4px;">
<button style="padding:8px 16px;background:#3b82f6;color:white;border:none;border-radius:4px;cursor:pointer;">送信</button>
</form>`}
		/>

		<div class="grid grid-cols-1 md:grid-cols-2 gap-4 mb-6">
			<div class="p-4 rounded-lg bg-gray-100 dark:bg-gray-800">
				<p class="text-sm text-gray-700 dark:text-gray-300">
					<strong>label と for/id はなぜ必要？</strong><br>
					ラベルをクリックすると入力欄にフォーカスが移る。<br>
					視覚障害者用の読み上げソフトも正しく動作する。
				</p>
			</div>
			<div class="p-4 rounded-lg bg-gray-100 dark:bg-gray-800">
				<p class="text-sm text-gray-700 dark:text-gray-300">
					<strong>name属性はなぜ必要？</strong><br>
					サーバーが受け取るデータの「項目名」になる。<br>
					例: <code class="bg-gray-200 dark:bg-gray-700 px-1 rounded">name="email"</code> → サーバーは「email」という名前でデータを受け取る
				</p>
			</div>
		</div>
	</section>

	<!-- inputの種類 -->
	<section class="mb-10">
		<h2 id="input-types" class="text-xl font-bold mb-4">inputの種類（type属性）</h2>

		<div class="p-4 rounded-lg bg-blue-50 dark:bg-blue-900/20 border border-blue-200 dark:border-blue-800 mb-6">
			<p class="text-sm text-blue-700 dark:text-blue-300">
				<strong>type属性で入力欄の「種類」を指定</strong><br>
				適切なtypeを選ぶと、スマホで専用キーボードが出たり、入力チェックが自動で行われる。
			</p>
		</div>

		<CodePreview
			title="テキスト系の入力"
			description="文字を入力する"
			language="html"
			code={`<!-- type="text": 普通のテキスト -->
<input type="text" placeholder="お名前">

<!-- type="email": メールアドレス -->
<!-- スマホでは@キーが表示される -->
<input type="email" placeholder="example@mail.com">

<!-- type="password": パスワード -->
<!-- 入力内容が●●●で隠れる -->
<input type="password" placeholder="パスワード">

<!-- type="tel": 電話番号 -->
<!-- スマホでは数字キーボードが出る -->
<input type="tel" placeholder="090-1234-5678">`}
			previewHtml={`<div style="display:flex;flex-direction:column;gap:8px;">
<input type="text" placeholder="お名前" style="padding:8px;border:1px solid #d1d5db;border-radius:4px;">
<input type="email" placeholder="example@mail.com" style="padding:8px;border:1px solid #d1d5db;border-radius:4px;">
<input type="password" placeholder="パスワード" value="secret" style="padding:8px;border:1px solid #d1d5db;border-radius:4px;">
<input type="tel" placeholder="090-1234-5678" style="padding:8px;border:1px solid #d1d5db;border-radius:4px;">
</div>`}
		/>

		<CodePreview
			title="数値・日付の入力"
			description="数字や日付を専用UIで入力"
			language="html"
			code={`<!-- type="number": 数値（上下ボタン付き） -->
<input type="number" min="0" max="100" value="50">

<!-- type="range": スライダー -->
<input type="range" min="0" max="100" value="50">

<!-- type="date": 日付（カレンダーが出る） -->
<input type="date">

<!-- type="time": 時刻 -->
<input type="time">`}
			previewHtml={`<div style="display:flex;flex-direction:column;gap:12px;">
<div><span style="font-size:12px;color:#6b7280;">数値:</span><input type="number" min="0" max="100" value="50" style="margin-left:8px;padding:4px;border:1px solid #d1d5db;border-radius:4px;width:80px;"></div>
<div><span style="font-size:12px;color:#6b7280;">範囲:</span><input type="range" min="0" max="100" value="50" style="margin-left:8px;width:150px;"></div>
<div><span style="font-size:12px;color:#6b7280;">日付:</span><input type="date" style="margin-left:8px;padding:4px;border:1px solid #d1d5db;border-radius:4px;"></div>
</div>`}
		/>

		<CodePreview
			title="選択系の入力"
			description="選択肢から選ぶ"
			language="html"
			code={`<!-- checkbox: 複数選択可能 -->
<p>好きな果物（複数選択可）</p>
<label>
  <input type="checkbox" name="fruits" value="apple"> りんご
</label>
<label>
  <input type="checkbox" name="fruits" value="banana"> バナナ
</label>

<!-- radio: 1つだけ選択 -->
<!-- 同じname属性で「グループ」を作る -->
<p>性別（1つ選択）</p>
<label>
  <input type="radio" name="gender" value="male"> 男性
</label>
<label>
  <input type="radio" name="gender" value="female"> 女性
</label>`}
			previewHtml={`<div style="display:flex;flex-direction:column;gap:12px;">
<div>
<p style="margin:0 0 4px 0;font-size:13px;">好きな果物（複数選択可）</p>
<label style="display:inline-flex;align-items:center;gap:4px;margin-right:12px;"><input type="checkbox"> りんご</label>
<label style="display:inline-flex;align-items:center;gap:4px;"><input type="checkbox"> バナナ</label>
</div>
<div>
<p style="margin:0 0 4px 0;font-size:13px;">性別（1つ選択）</p>
<label style="display:inline-flex;align-items:center;gap:4px;margin-right:12px;"><input type="radio" name="gender-demo"> 男性</label>
<label style="display:inline-flex;align-items:center;gap:4px;"><input type="radio" name="gender-demo"> 女性</label>
</div>
</div>`}
		/>

		<div class="p-4 rounded-lg bg-gray-100 dark:bg-gray-800 mb-6">
			<p class="text-sm text-gray-700 dark:text-gray-300">
				<strong>checkbox と radio の違い</strong><br>
				• <code class="bg-gray-200 dark:bg-gray-700 px-1 rounded">checkbox</code>：複数選べる（「りんごとバナナ両方好き」）<br>
				• <code class="bg-gray-200 dark:bg-gray-700 px-1 rounded">radio</code>：1つだけ選ぶ（「男性か女性か」）<br>
				radioは同じ<code class="bg-gray-200 dark:bg-gray-700 px-1 rounded">name</code>を付けて「グループ」にする必要がある
			</p>
		</div>
	</section>

	<!-- その他の要素 -->
	<section class="mb-10">
		<h2 id="other-elements" class="text-xl font-bold mb-4">その他のフォーム要素</h2>

		<CodePreview
			title="textarea（テキストエリア）"
			description="長い文章を入力する欄"
			language="html"
			code={`<!-- textarea: 複数行のテキスト入力 -->
<!-- rows: 表示する行数 -->
<!-- placeholder: 入力前に表示するヒント -->
<textarea
  rows="4"
  placeholder="お問い合わせ内容を入力してください..."
></textarea>`}
			previewHtml={`<textarea rows="3" placeholder="お問い合わせ内容を入力してください..." style="padding:8px;border:1px solid #d1d5db;border-radius:4px;width:100%;resize:vertical;"></textarea>`}
		/>

		<CodePreview
			title="select（セレクトボックス）"
			description="ドロップダウンで選択"
			language="html"
			code={`<!-- select: ドロップダウンリスト -->
<!-- option: 選択肢 -->
<!-- value: サーバーに送られる値 -->
<select name="country">
  <option value="">選択してください</option>
  <option value="jp">日本</option>
  <option value="us">アメリカ</option>
  <option value="uk">イギリス</option>
</select>`}
			previewHtml={`<select style="padding:8px;border:1px solid #d1d5db;border-radius:4px;min-width:200px;">
<option>選択してください</option>
<option>日本</option>
<option>アメリカ</option>
<option>イギリス</option>
</select>`}
		/>

		<div class="p-4 rounded-lg bg-gray-100 dark:bg-gray-800 mb-6">
			<p class="text-sm text-gray-700 dark:text-gray-300">
				<strong>input と textarea と select の使い分け</strong><br>
				• <code class="bg-gray-200 dark:bg-gray-700 px-1 rounded">input</code>：短い入力（名前、メールなど）<br>
				• <code class="bg-gray-200 dark:bg-gray-700 px-1 rounded">textarea</code>：長い入力（メッセージ、コメント）<br>
				• <code class="bg-gray-200 dark:bg-gray-700 px-1 rounded">select</code>：決まった選択肢から選ぶ（国、カテゴリ）
			</p>
		</div>
	</section>

	<!-- バリデーション -->
	<section class="mb-10">
		<h2 id="validation" class="text-xl font-bold mb-4">入力チェック（バリデーション）</h2>

		<div class="p-4 rounded-lg bg-amber-50 dark:bg-amber-900/20 border border-amber-200 dark:border-amber-800 mb-6">
			<p class="font-semibold text-amber-800 dark:text-amber-200">バリデーションとは？</p>
			<p class="text-sm text-amber-700 dark:text-amber-300 mt-2">
				ユーザーが正しい形式で入力しているかチェックすること。<br>
				例：メールアドレス欄に「abc」と入力 → 「@が必要です」とエラー表示
			</p>
		</div>

		<CodePreview
			title="HTML5のバリデーション属性"
			description="属性を付けるだけで自動チェック"
			language="html"
			code={`<!-- required: 必須入力（空欄だと送信できない） -->
<input type="text" required placeholder="必須項目 *">

<!-- minlength/maxlength: 文字数制限 -->
<input type="text" minlength="3" maxlength="20"
       placeholder="3〜20文字">

<!-- min/max: 数値の範囲制限 -->
<input type="number" min="1" max="100"
       placeholder="1〜100の数値">

<!-- pattern: 正規表現でパターン指定 -->
<!-- 例: 郵便番号形式（123-4567） -->
<input type="text" pattern="[0-9]{3}-[0-9]{4}"
       placeholder="123-4567">`}
			previewHtml={`<div style="display:flex;flex-direction:column;gap:8px;">
<input type="text" required placeholder="必須項目 *" style="padding:8px;border:1px solid #d1d5db;border-radius:4px;">
<input type="text" minlength="3" maxlength="20" placeholder="3〜20文字" style="padding:8px;border:1px solid #d1d5db;border-radius:4px;">
<input type="number" min="1" max="100" placeholder="1〜100の数値" style="padding:8px;border:1px solid #d1d5db;border-radius:4px;">
<input type="text" pattern="[0-9]{3}-[0-9]{4}" placeholder="123-4567（郵便番号）" style="padding:8px;border:1px solid #d1d5db;border-radius:4px;">
</div>`}
		/>
	</section>

	<!-- 完成例 -->
	<section class="mb-10">
		<h2 id="complete-form" class="text-xl font-bold mb-4">完成例：お問い合わせフォーム</h2>

		<CodePreview
			title="実用的なフォーム"
			description="学んだ要素を組み合わせる"
			language="html"
			code={`<form action="/contact" method="POST">
  <!-- 名前（必須） -->
  <div>
    <label for="name">お名前 *</label>
    <input type="text" id="name" name="name" required>
  </div>

  <!-- メール（必須、形式チェック） -->
  <div>
    <label for="email">メールアドレス *</label>
    <input type="email" id="email" name="email" required>
  </div>

  <!-- カテゴリ（選択） -->
  <div>
    <label for="category">カテゴリ</label>
    <select id="category" name="category">
      <option value="general">一般</option>
      <option value="support">サポート</option>
      <option value="sales">営業</option>
    </select>
  </div>

  <!-- メッセージ（必須、複数行） -->
  <div>
    <label for="message">メッセージ *</label>
    <textarea id="message" name="message"
              rows="5" required></textarea>
  </div>

  <!-- チェックボックス -->
  <div>
    <label>
      <input type="checkbox" name="newsletter">
      ニュースレターを受け取る
    </label>
  </div>

  <button type="submit">送信</button>
</form>`}
			previewHtml={`<form style="display:flex;flex-direction:column;gap:12px;max-width:300px;">
<div><label style="display:block;font-size:14px;margin-bottom:4px;">お名前 *</label><input type="text" required style="width:100%;padding:8px;border:1px solid #d1d5db;border-radius:4px;"></div>
<div><label style="display:block;font-size:14px;margin-bottom:4px;">メールアドレス *</label><input type="email" required style="width:100%;padding:8px;border:1px solid #d1d5db;border-radius:4px;"></div>
<div><label style="display:block;font-size:14px;margin-bottom:4px;">カテゴリ</label><select style="width:100%;padding:8px;border:1px solid #d1d5db;border-radius:4px;"><option>一般</option><option>サポート</option><option>営業</option></select></div>
<div><label style="display:block;font-size:14px;margin-bottom:4px;">メッセージ *</label><textarea rows="3" style="width:100%;padding:8px;border:1px solid #d1d5db;border-radius:4px;resize:vertical;"></textarea></div>
<label style="display:flex;align-items:center;gap:4px;font-size:14px;"><input type="checkbox"> ニュースレターを受け取る</label>
<button style="padding:10px 16px;background:#3b82f6;color:white;border:none;border-radius:4px;cursor:pointer;font-weight:500;">送信</button>
</form>`}
		/>
	</section>

	<!-- まとめ -->
	<section class="mb-10">
		<h2 id="summary" class="text-xl font-bold mb-4">まとめ</h2>

		<div class="grid grid-cols-1 md:grid-cols-2 gap-4">
			<div class="p-4 rounded-lg bg-green-50 dark:bg-green-900/20 border border-green-200 dark:border-green-800">
				<h3 class="font-semibold text-green-800 dark:text-green-200 mb-2">覚えておくこと</h3>
				<ul class="text-sm text-green-700 dark:text-green-300 space-y-1">
					<li>• formで全体を囲む</li>
					<li>• labelとinputはfor/idで紐づけ</li>
					<li>• typeで入力の種類を指定</li>
					<li>• requiredで必須入力に</li>
				</ul>
			</div>
			<div class="p-4 rounded-lg bg-blue-50 dark:bg-blue-900/20 border border-blue-200 dark:border-blue-800">
				<h3 class="font-semibold text-blue-800 dark:text-blue-200 mb-2">よく使うtype</h3>
				<ul class="text-sm text-blue-700 dark:text-blue-300 space-y-1">
					<li>• text, email, password</li>
					<li>• checkbox, radio</li>
					<li>• number, date</li>
					<li>• submit（送信ボタン）</li>
				</ul>
			</div>
		</div>
	</section>

	<div class="flex justify-between pt-6 border-t border-gray-200 dark:border-gray-700">
		<a href="/html/elements" class="inline-flex items-center gap-2 px-4 py-2 rounded-lg border border-gray-300 dark:border-gray-600 hover:bg-gray-100 dark:hover:bg-gray-800 transition-colors">
			<svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
				<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 19l-7-7 7-7" />
			</svg>
			前へ：要素とタグ
		</a>
		<a href="/html/semantics" class="inline-flex items-center gap-2 px-4 py-2 rounded-lg bg-primary-600 text-white hover:bg-primary-700 transition-colors">
			次へ：セマンティクス
			<svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
				<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 5l7 7-7 7" />
			</svg>
		</a>
	</div>
</article>
