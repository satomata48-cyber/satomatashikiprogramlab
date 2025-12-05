<script>
	import CodePreview from '$lib/components/CodePreview.svelte';
</script>

<svelte:head>
	<title>オブジェクト指向 | さとまたラボ</title>
</svelte:head>

<article>
	<h1 class="text-3xl font-bold mb-2">オブジェクト指向</h1>
	<p class="text-lg text-gray-600 dark:text-gray-400 mb-8">
		プログラミングの基本的な考え方を学ぼう
	</p>

	<!-- オブジェクト指向とは -->
	<section class="mb-12">
		<h2 id="what-is-oop" class="text-xl font-bold mb-4">オブジェクト指向って何？</h2>

		<div class="p-6 rounded-xl bg-gradient-to-r from-yellow-50 to-orange-50 dark:from-yellow-900/20 dark:to-orange-900/20 border border-yellow-200 dark:border-yellow-800 mb-6">
			<p class="text-lg text-yellow-800 dark:text-yellow-200 mb-4">
				<strong>オブジェクト指向</strong> = 「モノ」を中心にプログラムを考える方法
			</p>
			<p class="text-sm text-yellow-700 dark:text-yellow-300">
				英語では Object-Oriented Programming（OOP）と呼びます。
				現実世界のモノや概念をプログラムで表現する考え方です。
			</p>
		</div>

		<div class="p-4 rounded-lg bg-blue-50 dark:bg-blue-900/20 border border-blue-200 dark:border-blue-800 mb-6">
			<p class="font-semibold text-blue-800 dark:text-blue-200 mb-3">身近な例で考えてみよう</p>
			<p class="text-sm text-blue-700 dark:text-blue-300 mb-3">
				「車」をプログラムで表現するとしたら？
			</p>
			<div class="grid md:grid-cols-2 gap-4">
				<div class="bg-white dark:bg-gray-800 p-3 rounded">
					<p class="font-semibold text-gray-800 dark:text-gray-200 mb-2">車の「属性」（データ）</p>
					<ul class="text-sm text-gray-600 dark:text-gray-400 space-y-1">
						<li>・色（赤、青、白...）</li>
						<li>・メーカー（トヨタ、ホンダ...）</li>
						<li>・速度（0km/h、60km/h...）</li>
						<li>・燃料の量</li>
					</ul>
				</div>
				<div class="bg-white dark:bg-gray-800 p-3 rounded">
					<p class="font-semibold text-gray-800 dark:text-gray-200 mb-2">車の「動作」（機能）</p>
					<ul class="text-sm text-gray-600 dark:text-gray-400 space-y-1">
						<li>・走る</li>
						<li>・止まる</li>
						<li>・曲がる</li>
						<li>・クラクションを鳴らす</li>
					</ul>
				</div>
			</div>
		</div>

		<p class="text-gray-700 dark:text-gray-300">
			このように、<strong>「データ」と「機能」をセットにしたもの</strong>を「オブジェクト」と呼びます。
		</p>
	</section>

	<!-- なぜオブジェクト指向？ -->
	<section class="mb-12">
		<h2 id="why-oop" class="text-xl font-bold mb-4">なぜオブジェクト指向を使うの？</h2>

		<div class="space-y-4 mb-6">
			<div class="p-4 rounded-lg bg-green-50 dark:bg-green-900/20 border border-green-200 dark:border-green-800">
				<div class="flex items-start gap-3">
					<span class="text-2xl">1</span>
					<div>
						<p class="font-semibold text-green-800 dark:text-green-200">コードの整理がしやすい</p>
						<p class="text-sm text-green-700 dark:text-green-300 mt-1">
							関連するデータと機能がまとまっているので、どこに何があるかわかりやすい。
						</p>
					</div>
				</div>
			</div>

			<div class="p-4 rounded-lg bg-blue-50 dark:bg-blue-900/20 border border-blue-200 dark:border-blue-800">
				<div class="flex items-start gap-3">
					<span class="text-2xl">2</span>
					<div>
						<p class="font-semibold text-blue-800 dark:text-blue-200">再利用しやすい</p>
						<p class="text-sm text-blue-700 dark:text-blue-300 mt-1">
							一度作った「設計図」から、いくつでも同じ種類のモノを作れる。
						</p>
					</div>
				</div>
			</div>

			<div class="p-4 rounded-lg bg-purple-50 dark:bg-purple-900/20 border border-purple-200 dark:border-purple-800">
				<div class="flex items-start gap-3">
					<span class="text-2xl">3</span>
					<div>
						<p class="font-semibold text-purple-800 dark:text-purple-200">変更に強い</p>
						<p class="text-sm text-purple-700 dark:text-purple-300 mt-1">
							一箇所を変更すれば、それを使っている全ての場所に反映される。
						</p>
					</div>
				</div>
			</div>
		</div>
	</section>

	<!-- クラスとオブジェクト -->
	<section class="mb-12">
		<h2 id="class-object" class="text-xl font-bold mb-4">クラスとオブジェクト</h2>

		<div class="p-4 rounded-lg bg-amber-50 dark:bg-amber-900/20 border border-amber-200 dark:border-amber-800 mb-6">
			<p class="font-semibold text-amber-800 dark:text-amber-200 mb-2">重要な用語</p>
			<div class="text-sm text-amber-700 dark:text-amber-300 space-y-2">
				<p><strong>クラス（Class）</strong> = 設計図。「こういうモノを作りますよ」という定義。</p>
				<p><strong>オブジェクト（Object）</strong> = 設計図から作った実物。「インスタンス」とも呼ぶ。</p>
			</div>
		</div>

		<div class="bg-gray-100 dark:bg-gray-800 rounded-lg p-4 mb-6">
			<p class="font-semibold text-gray-800 dark:text-gray-200 mb-3">たい焼きで例えると...</p>
			<div class="flex items-center gap-4 justify-center">
				<div class="text-center">
					<div class="text-4xl mb-2">📋</div>
					<p class="text-sm text-gray-600 dark:text-gray-400">たい焼きの型（金型）</p>
					<p class="text-xs text-blue-600 dark:text-blue-400">= クラス</p>
				</div>
				<div class="text-2xl text-gray-400">→</div>
				<div class="text-center">
					<div class="text-4xl mb-2">🐟🐟🐟</div>
					<p class="text-sm text-gray-600 dark:text-gray-400">焼き上がったたい焼き</p>
					<p class="text-xs text-blue-600 dark:text-blue-400">= オブジェクト</p>
				</div>
			</div>
			<p class="text-xs text-gray-500 text-center mt-3">
				1つの型（クラス）から、たくさんのたい焼き（オブジェクト）を作れる
			</p>
		</div>

		<CodePreview
			title="クラスの基本"
			description="classキーワードで定義する"
			language="javascript"
			code={`// クラス = 設計図を定義
class Car {
  // コンストラクタ = 初期設定
  constructor(color, maker) {
    this.color = color;    // 色
    this.maker = maker;    // メーカー
    this.speed = 0;        // 速度（最初は0）
  }

  // メソッド = 動作・機能
  run() {
    this.speed = 60;
    console.log(this.color + 'の車が走り出しました！');
  }

  stop() {
    this.speed = 0;
    console.log('車が止まりました');
  }
}

// オブジェクト = 設計図から実物を作る
const myCar = new Car('赤', 'トヨタ');
const yourCar = new Car('青', 'ホンダ');

console.log(myCar.color);   // "赤"
console.log(yourCar.color); // "青"

myCar.run();  // "赤の車が走り出しました！"`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div style="color:#6a9955;">// 実行結果:</div><div>赤</div><div>青</div><div>赤の車が走り出しました！</div></div>`}
		/>

		<div class="mt-6 space-y-4">
			<div class="p-4 rounded-lg bg-gray-50 dark:bg-gray-800">
				<p class="font-semibold text-gray-800 dark:text-gray-200 mb-2">constructor って何？</p>
				<p class="text-sm text-gray-600 dark:text-gray-400">
					「コンストラクタ」は、オブジェクトを作るとき（<code>new</code>するとき）に自動で実行される特別な関数です。
					初期値を設定するのに使います。
				</p>
			</div>

			<div class="p-4 rounded-lg bg-gray-50 dark:bg-gray-800">
				<p class="font-semibold text-gray-800 dark:text-gray-200 mb-2">this って何？</p>
				<p class="text-sm text-gray-600 dark:text-gray-400">
					「this」は「このオブジェクト自身」を指します。
					<code>this.color</code> は「このオブジェクトの color」という意味です。
				</p>
			</div>

			<div class="p-4 rounded-lg bg-gray-50 dark:bg-gray-800">
				<p class="font-semibold text-gray-800 dark:text-gray-200 mb-2">new って何？</p>
				<p class="text-sm text-gray-600 dark:text-gray-400">
					「new」はクラスから新しいオブジェクトを作るキーワードです。
					<code>new Car('赤', 'トヨタ')</code> で、赤いトヨタの車オブジェクトができます。
				</p>
			</div>
		</div>
	</section>

	<!-- プロパティとメソッド -->
	<section class="mb-12">
		<h2 id="property-method" class="text-xl font-bold mb-4">プロパティとメソッド</h2>

		<div class="grid md:grid-cols-2 gap-4 mb-6">
			<div class="p-4 rounded-lg bg-blue-50 dark:bg-blue-900/20 border border-blue-200 dark:border-blue-800">
				<p class="font-semibold text-blue-800 dark:text-blue-200 mb-2">プロパティ（Property）</p>
				<p class="text-sm text-blue-700 dark:text-blue-300 mb-2">
					オブジェクトが持つ「データ」のこと。
				</p>
				<div class="bg-white dark:bg-gray-800 p-2 rounded font-mono text-sm">
					<p>myCar.<span class="text-blue-600">color</span> = '赤'</p>
					<p>myCar.<span class="text-blue-600">speed</span> = 60</p>
				</div>
			</div>
			<div class="p-4 rounded-lg bg-green-50 dark:bg-green-900/20 border border-green-200 dark:border-green-800">
				<p class="font-semibold text-green-800 dark:text-green-200 mb-2">メソッド（Method）</p>
				<p class="text-sm text-green-700 dark:text-green-300 mb-2">
					オブジェクトが持つ「機能」のこと。関数と同じ。
				</p>
				<div class="bg-white dark:bg-gray-800 p-2 rounded font-mono text-sm">
					<p>myCar.<span class="text-green-600">run()</span></p>
					<p>myCar.<span class="text-green-600">stop()</span></p>
				</div>
			</div>
		</div>

		<CodePreview
			title="プロパティとメソッドの使い方"
			description="ドット（.）でアクセス"
			language="javascript"
			code={`class User {
  constructor(name, age) {
    // プロパティ
    this.name = name;
    this.age = age;
    this.isLoggedIn = false;
  }

  // メソッド
  login() {
    this.isLoggedIn = true;
    console.log(this.name + 'さんがログインしました');
  }

  logout() {
    this.isLoggedIn = false;
    console.log(this.name + 'さんがログアウトしました');
  }

  // プロパティを変更するメソッド
  birthday() {
    this.age = this.age + 1;
    console.log('お誕生日おめでとう！' + this.age + '歳になりました');
  }
}

const user = new User('田中', 25);

// プロパティにアクセス
console.log(user.name);  // "田中"
console.log(user.age);   // 25

// メソッドを実行
user.login();     // "田中さんがログインしました"
user.birthday();  // "お誕生日おめでとう！26歳になりました"`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div style="color:#6a9955;">// 実行結果:</div><div>田中</div><div>25</div><div>田中さんがログインしました</div><div>お誕生日おめでとう！26歳になりました</div></div>`}
		/>
	</section>

	<!-- 継承 -->
	<section class="mb-12">
		<h2 id="inheritance" class="text-xl font-bold mb-4">継承（けいしょう）</h2>

		<div class="p-4 rounded-lg bg-purple-50 dark:bg-purple-900/20 border border-purple-200 dark:border-purple-800 mb-6">
			<p class="font-semibold text-purple-800 dark:text-purple-200 mb-2">継承とは？</p>
			<p class="text-sm text-purple-700 dark:text-purple-300">
				既存のクラスを「親」として、その機能を引き継いだ「子」クラスを作ること。
				共通部分を親クラスにまとめることで、コードの重複を減らせます。
			</p>
		</div>

		<div class="bg-gray-100 dark:bg-gray-800 rounded-lg p-4 mb-6">
			<p class="font-semibold text-gray-800 dark:text-gray-200 mb-3">動物で例えると...</p>
			<div class="flex flex-col items-center gap-2">
				<div class="p-3 bg-blue-100 dark:bg-blue-900 rounded-lg text-center">
					<p class="font-semibold text-blue-800 dark:text-blue-200">Animal（動物）</p>
					<p class="text-xs text-blue-600 dark:text-blue-400">name, eat(), sleep()</p>
				</div>
				<div class="text-gray-400">↓ 継承</div>
				<div class="flex gap-4">
					<div class="p-3 bg-green-100 dark:bg-green-900 rounded-lg text-center">
						<p class="font-semibold text-green-800 dark:text-green-200">Dog（犬）</p>
						<p class="text-xs text-green-600 dark:text-green-400">+ bark()</p>
					</div>
					<div class="p-3 bg-orange-100 dark:bg-orange-900 rounded-lg text-center">
						<p class="font-semibold text-orange-800 dark:text-orange-200">Cat（猫）</p>
						<p class="text-xs text-orange-600 dark:text-orange-400">+ meow()</p>
					</div>
					<div class="p-3 bg-purple-100 dark:bg-purple-900 rounded-lg text-center">
						<p class="font-semibold text-purple-800 dark:text-purple-200">Bird（鳥）</p>
						<p class="text-xs text-purple-600 dark:text-purple-400">+ fly()</p>
					</div>
				</div>
			</div>
			<p class="text-xs text-gray-500 text-center mt-3">
				犬も猫も鳥も「動物」の機能（食べる、寝る）を持ちつつ、独自の機能も持てる
			</p>
		</div>

		<CodePreview
			title="継承の書き方"
			description="extendsキーワードを使う"
			language="javascript"
			code={`// 親クラス
class Animal {
  constructor(name) {
    this.name = name;
  }

  eat() {
    console.log(this.name + 'がご飯を食べています');
  }

  sleep() {
    console.log(this.name + 'が寝ています');
  }
}

// 子クラス（Animalを継承）
class Dog extends Animal {
  constructor(name, breed) {
    super(name);  // 親のconstructorを呼び出す
    this.breed = breed;  // 犬種（子クラス独自のプロパティ）
  }

  // 子クラス独自のメソッド
  bark() {
    console.log('ワンワン！');
  }
}

class Cat extends Animal {
  meow() {
    console.log('ニャーニャー！');
  }
}

// 使ってみる
const pochi = new Dog('ポチ', '柴犬');
pochi.eat();   // "ポチがご飯を食べています" ← 親の機能
pochi.bark();  // "ワンワン！" ← 子の独自機能

const tama = new Cat('タマ');
tama.sleep();  // "タマが寝ています" ← 親の機能
tama.meow();   // "ニャーニャー！" ← 子の独自機能`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div style="color:#6a9955;">// 実行結果:</div><div>ポチがご飯を食べています</div><div>ワンワン！</div><div>タマが寝ています</div><div>ニャーニャー！</div></div>`}
		/>

		<div class="mt-6 space-y-4">
			<div class="p-4 rounded-lg bg-gray-50 dark:bg-gray-800">
				<p class="font-semibold text-gray-800 dark:text-gray-200 mb-2">extends って何？</p>
				<p class="text-sm text-gray-600 dark:text-gray-400">
					「〜を拡張する」という意味です。
					<code>class Dog extends Animal</code> は「Animal を拡張して Dog を作る」という意味です。
				</p>
			</div>

			<div class="p-4 rounded-lg bg-gray-50 dark:bg-gray-800">
				<p class="font-semibold text-gray-800 dark:text-gray-200 mb-2">super() って何？</p>
				<p class="text-sm text-gray-600 dark:text-gray-400">
					親クラスのコンストラクタを呼び出すものです。
					子クラスのコンストラクタでは、最初に <code>super()</code> を呼ぶ必要があります。
				</p>
			</div>
		</div>
	</section>

	<!-- カプセル化 -->
	<section class="mb-12">
		<h2 id="encapsulation" class="text-xl font-bold mb-4">カプセル化</h2>

		<div class="p-4 rounded-lg bg-amber-50 dark:bg-amber-900/20 border border-amber-200 dark:border-amber-800 mb-6">
			<p class="font-semibold text-amber-800 dark:text-amber-200 mb-2">カプセル化とは？</p>
			<p class="text-sm text-amber-700 dark:text-amber-300">
				データを外から直接変更できないように「隠す」こと。
				想定外の値が入ることを防ぎ、プログラムの安全性を高めます。
			</p>
		</div>

		<CodePreview
			title="プライベートプロパティ"
			description="#をつけると外からアクセスできなくなる"
			language="javascript"
			code={`class BankAccount {
  #balance = 0;  // #をつけるとプライベート（外から見えない）

  constructor(initialBalance) {
    if (initialBalance > 0) {
      this.#balance = initialBalance;
    }
  }

  // 残高を確認する方法（読み取り専用）
  getBalance() {
    return this.#balance;
  }

  // 入金する方法（チェック付き）
  deposit(amount) {
    if (amount > 0) {
      this.#balance += amount;
      console.log(amount + '円入金しました');
    } else {
      console.log('正しい金額を入力してください');
    }
  }

  // 出金する方法（チェック付き）
  withdraw(amount) {
    if (amount > 0 && amount <= this.#balance) {
      this.#balance -= amount;
      console.log(amount + '円出金しました');
    } else {
      console.log('出金できません');
    }
  }
}

const account = new BankAccount(10000);

// メソッドを通じてアクセス（安全）
console.log(account.getBalance());  // 10000
account.deposit(5000);              // "5000円入金しました"
console.log(account.getBalance());  // 15000

// 直接アクセスはできない（エラー）
// console.log(account.#balance);   // SyntaxError!
// account.#balance = 1000000;      // 勝手に変更できない！`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div style="color:#6a9955;">// 実行結果:</div><div>10000</div><div>5000円入金しました</div><div>15000</div></div>`}
		/>

		<div class="mt-6 p-4 rounded-lg bg-blue-50 dark:bg-blue-900/20 border border-blue-200 dark:border-blue-800">
			<p class="font-semibold text-blue-800 dark:text-blue-200 mb-2">なぜカプセル化が大事？</p>
			<p class="text-sm text-blue-700 dark:text-blue-300">
				銀行口座の例で考えてみてください。<br>
				もし残高を自由に変更できたら、<code>account.balance = -1000000</code> なんて書けてしまいます。<br>
				カプセル化することで、「入金」「出金」という正しい方法でしか残高を変更できなくなります。
			</p>
		</div>
	</section>

	<!-- 実践例 -->
	<section class="mb-12">
		<h2 id="practical" class="text-xl font-bold mb-4">実践例：Todoリスト</h2>

		<p class="text-gray-700 dark:text-gray-300 mb-4">
			実際のアプリでオブジェクト指向を使う例を見てみましょう。
		</p>

		<CodePreview
			title="TodoリストをOOPで実装"
			description="クラスを使って整理"
			language="javascript"
			code={`// Todo1件を表すクラス
class Todo {
  constructor(title) {
    this.id = Date.now();  // ユニークなID
    this.title = title;
    this.completed = false;
    this.createdAt = new Date();
  }

  toggle() {
    this.completed = !this.completed;
  }
}

// Todoリスト全体を管理するクラス
class TodoList {
  #todos = [];

  // Todoを追加
  add(title) {
    const todo = new Todo(title);
    this.#todos.push(todo);
    console.log('追加: ' + title);
    return todo;
  }

  // Todoを削除
  remove(id) {
    this.#todos = this.#todos.filter(todo => todo.id !== id);
    console.log('削除しました');
  }

  // 完了/未完了を切り替え
  toggle(id) {
    const todo = this.#todos.find(todo => todo.id === id);
    if (todo) {
      todo.toggle();
      console.log(todo.title + ': ' + (todo.completed ? '完了' : '未完了'));
    }
  }

  // 全てのTodoを取得
  getAll() {
    return [...this.#todos];  // コピーを返す（直接変更を防ぐ）
  }

  // 未完了のTodoだけ取得
  getActive() {
    return this.#todos.filter(todo => !todo.completed);
  }

  // 完了済みのTodoだけ取得
  getCompleted() {
    return this.#todos.filter(todo => todo.completed);
  }
}

// 使ってみる
const myTodos = new TodoList();

const todo1 = myTodos.add('牛乳を買う');
const todo2 = myTodos.add('メールを返信');
const todo3 = myTodos.add('部屋を掃除');

myTodos.toggle(todo1.id);  // "牛乳を買う: 完了"

console.log('未完了:', myTodos.getActive().length + '件');
console.log('完了済み:', myTodos.getCompleted().length + '件');`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div style="color:#6a9955;">// 実行結果:</div><div>追加: 牛乳を買う</div><div>追加: メールを返信</div><div>追加: 部屋を掃除</div><div>牛乳を買う: 完了</div><div>未完了: 2件</div><div>完了済み: 1件</div></div>`}
		/>
	</section>

	<!-- OOPの3つの柱 -->
	<section class="mb-12">
		<h2 id="pillars" class="text-xl font-bold mb-4">オブジェクト指向の3つの柱</h2>

		<p class="text-gray-700 dark:text-gray-300 mb-4">
			オブジェクト指向には「3つの柱」と呼ばれる重要な概念があります。
		</p>

		<div class="space-y-4">
			<div class="p-5 rounded-xl bg-blue-50 dark:bg-blue-900/20 border border-blue-200 dark:border-blue-800">
				<div class="flex items-start gap-3">
					<span class="w-10 h-10 bg-blue-500 text-white rounded-full flex items-center justify-center font-bold text-lg">1</span>
					<div>
						<p class="font-bold text-blue-800 dark:text-blue-200 text-lg">カプセル化（Encapsulation）</p>
						<p class="text-sm text-blue-700 dark:text-blue-300 mt-2">
							データを隠して、メソッドを通じてのみアクセスさせる。
							想定外の変更を防ぎ、安全性を高める。
						</p>
						<p class="text-xs text-blue-600 dark:text-blue-400 mt-2">
							例: #balance を直接変更できなくする
						</p>
					</div>
				</div>
			</div>

			<div class="p-5 rounded-xl bg-green-50 dark:bg-green-900/20 border border-green-200 dark:border-green-800">
				<div class="flex items-start gap-3">
					<span class="w-10 h-10 bg-green-500 text-white rounded-full flex items-center justify-center font-bold text-lg">2</span>
					<div>
						<p class="font-bold text-green-800 dark:text-green-200 text-lg">継承（Inheritance）</p>
						<p class="text-sm text-green-700 dark:text-green-300 mt-2">
							親クラスの機能を子クラスが引き継ぐ。
							共通部分をまとめて、コードの重複を減らす。
						</p>
						<p class="text-xs text-green-600 dark:text-green-400 mt-2">
							例: Animal → Dog, Cat
						</p>
					</div>
				</div>
			</div>

			<div class="p-5 rounded-xl bg-purple-50 dark:bg-purple-900/20 border border-purple-200 dark:border-purple-800">
				<div class="flex items-start gap-3">
					<span class="w-10 h-10 bg-purple-500 text-white rounded-full flex items-center justify-center font-bold text-lg">3</span>
					<div>
						<p class="font-bold text-purple-800 dark:text-purple-200 text-lg">ポリモーフィズム（Polymorphism）</p>
						<p class="text-sm text-purple-700 dark:text-purple-300 mt-2">
							同じ名前のメソッドでも、オブジェクトによって違う動作をする。
							「多態性」とも呼ばれる。
						</p>
						<p class="text-xs text-purple-600 dark:text-purple-400 mt-2">
							例: animal.speak() → 犬なら「ワン」、猫なら「ニャー」
						</p>
					</div>
				</div>
			</div>
		</div>
	</section>

	<!-- まとめ -->
	<section class="mb-10">
		<h2 id="summary" class="text-xl font-bold mb-4">まとめ</h2>

		<div class="space-y-4">
			<div class="p-4 rounded-lg bg-yellow-50 dark:bg-yellow-900/20 border border-yellow-200 dark:border-yellow-800">
				<p class="font-semibold text-yellow-800 dark:text-yellow-200">オブジェクト指向 = モノ中心の考え方</p>
				<p class="text-sm text-yellow-700 dark:text-yellow-300">
					データと機能をセットにした「オブジェクト」でプログラムを構成する。
				</p>
			</div>
			<div class="p-4 rounded-lg bg-blue-50 dark:bg-blue-900/20 border border-blue-200 dark:border-blue-800">
				<p class="font-semibold text-blue-800 dark:text-blue-200">クラス = 設計図、オブジェクト = 実物</p>
				<p class="text-sm text-blue-700 dark:text-blue-300">
					classで定義し、newで作成する。
				</p>
			</div>
			<div class="p-4 rounded-lg bg-green-50 dark:bg-green-900/20 border border-green-200 dark:border-green-800">
				<p class="font-semibold text-green-800 dark:text-green-200">プロパティ = データ、メソッド = 機能</p>
				<p class="text-sm text-green-700 dark:text-green-300">
					ドット（.）でアクセスする。
				</p>
			</div>
			<div class="p-4 rounded-lg bg-purple-50 dark:bg-purple-900/20 border border-purple-200 dark:border-purple-800">
				<p class="font-semibold text-purple-800 dark:text-purple-200">3つの柱: カプセル化、継承、ポリモーフィズム</p>
				<p class="text-sm text-purple-700 dark:text-purple-300">
					これらを理解すると、より良い設計ができるようになる。
				</p>
			</div>
		</div>
	</section>

	<!-- ナビゲーション -->
	<div class="flex justify-between pt-6 border-t border-gray-200 dark:border-gray-700">
		<a href="/js/async" class="inline-flex items-center gap-2 px-4 py-2 rounded-lg border border-gray-300 dark:border-gray-600 hover:bg-gray-100 dark:hover:bg-gray-800 transition-colors">
			<svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
				<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 19l-7-7 7-7" />
			</svg>
			前へ：非同期処理
		</a>
		<a href="/ts/basics" class="inline-flex items-center gap-2 px-4 py-2 rounded-lg bg-primary-600 text-white hover:bg-primary-700 transition-colors">
			次へ：TypeScript はじめに
			<svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
				<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 5l7 7-7 7" />
			</svg>
		</a>
	</div>
</article>
