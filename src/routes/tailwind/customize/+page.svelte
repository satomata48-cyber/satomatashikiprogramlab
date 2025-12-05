<script>
	import CodePreview from '$lib/components/CodePreview.svelte';
</script>

<svelte:head>
	<title>Tailwind カスタマイズ | さとまたラボ</title>
</svelte:head>

<article>
	<h1 class="text-3xl font-bold mb-2">カスタマイズ</h1>
	<p class="text-lg text-gray-600 dark:text-gray-400 mb-8">
		tailwind.config.jsでプロジェクトに合わせて設定
	</p>

	<section class="mb-10">
		<h2 id="config" class="text-xl font-bold mb-4">設定ファイル</h2>

		<CodePreview
			title="tailwind.config.js"
			description="基本的な設定ファイル構造"
			language="javascript"
			code={`/** @type {import('tailwindcss').Config} */
export default {
  // スキャン対象のファイル
  content: [
    './src/**/*.{html,js,svelte,ts}',
  ],

  // ダークモードの方式
  darkMode: 'class',

  // テーマのカスタマイズ
  theme: {
    extend: {
      // ここに追加
    }
  },

  // プラグイン
  plugins: [],
}`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div><span style="color:#9cdcfe;">content</span>: スキャン対象</div><div><span style="color:#9cdcfe;">darkMode</span>: ダークモード設定</div><div><span style="color:#9cdcfe;">theme</span>: テーマカスタマイズ</div><div><span style="color:#9cdcfe;">plugins</span>: プラグイン追加</div></div>`}
		/>
	</section>

	<section class="mb-10">
		<h2 id="colors" class="text-xl font-bold mb-4">カスタムカラー</h2>

		<CodePreview
			title="色の追加"
			description="独自のブランドカラーを定義"
			language="javascript"
			code={`// tailwind.config.js
export default {
  theme: {
    extend: {
      colors: {
        // シンプルな追加
        brand: '#ff6b35',

        // パレット形式
        primary: {
          50: '#f0f9ff',
          100: '#e0f2fe',
          200: '#bae6fd',
          300: '#7dd3fc',
          400: '#38bdf8',
          500: '#0ea5e9',
          600: '#0284c7',
          700: '#0369a1',
          800: '#075985',
          900: '#0c4a6e',
        },
      },
    },
  },
}

// 使用例
// <div class="bg-brand">ブランドカラー</div>
// <div class="text-primary-500">プライマリ500</div>`}
			previewHtml={`<div style="display:flex;gap:8px;flex-wrap:wrap;"><div style="padding:12px;background:#ff6b35;color:white;border-radius:4px;">bg-brand</div><div style="display:flex;border-radius:4px;overflow:hidden;"><div style="width:30px;height:30px;background:#f0f9ff;"></div><div style="width:30px;height:30px;background:#bae6fd;"></div><div style="width:30px;height:30px;background:#38bdf8;"></div><div style="width:30px;height:30px;background:#0284c7;"></div><div style="width:30px;height:30px;background:#0c4a6e;"></div></div></div>`}
		/>
	</section>

	<section class="mb-10">
		<h2 id="fonts" class="text-xl font-bold mb-4">フォント</h2>

		<CodePreview
			title="フォントファミリー"
			description="カスタムフォントを追加"
			language="javascript"
			code={`// tailwind.config.js
export default {
  theme: {
    extend: {
      fontFamily: {
        // カスタムフォント
        sans: ['Inter', 'sans-serif'],
        display: ['Poppins', 'sans-serif'],
        mono: ['JetBrains Mono', 'monospace'],
        jp: ['Noto Sans JP', 'sans-serif'],
      },
    },
  },
}

// 使用例
// <p class="font-sans">基本フォント</p>
// <h1 class="font-display">見出し用</h1>
// <code class="font-mono">コード</code>`}
			previewHtml={`<div style="display:flex;flex-direction:column;gap:8px;"><p style="font-family:sans-serif;">font-sans: 本文テキスト</p><h1 style="font-family:sans-serif;font-weight:bold;font-size:20px;">font-display: 見出し</h1><code style="font-family:monospace;background:#f3f4f6;padding:4px 8px;border-radius:4px;">font-mono: コード</code></div>`}
		/>
	</section>

	<section class="mb-10">
		<h2 id="spacing" class="text-xl font-bold mb-4">スペーシング</h2>

		<CodePreview
			title="カスタムスペーシング"
			description="独自の値を追加"
			language="javascript"
			code={`// tailwind.config.js
export default {
  theme: {
    extend: {
      spacing: {
        '18': '4.5rem',    // 72px
        '88': '22rem',     // 352px
        '128': '32rem',    // 512px
      },
    },
  },
}

// 使用例
// <div class="p-18">padding 72px</div>
// <div class="w-88">width 352px</div>
// <div class="mt-128">margin-top 512px</div>`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div>p-18 → 4.5rem (72px)</div><div>w-88 → 22rem (352px)</div><div>mt-128 → 32rem (512px)</div></div>`}
		/>
	</section>

	<section class="mb-10">
		<h2 id="breakpoints" class="text-xl font-bold mb-4">ブレークポイント</h2>

		<CodePreview
			title="カスタムブレークポイント"
			description="独自の画面幅を設定"
			language="javascript"
			code={`// tailwind.config.js
export default {
  theme: {
    // 完全に上書き
    screens: {
      'sm': '640px',
      'md': '768px',
      'lg': '1024px',
      'xl': '1280px',
      '2xl': '1536px',
    },

    // または extend で追加
    extend: {
      screens: {
        'xs': '475px',      // 追加
        '3xl': '1920px',    // 追加
      },
    },
  },
}

// 使用例
// <div class="xs:text-sm">475px以上で適用</div>`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div>xs: 475px <span style="color:#6a9955;">// カスタム追加</span></div><div>sm: 640px</div><div>md: 768px</div><div>lg: 1024px</div><div>xl: 1280px</div><div>2xl: 1536px</div><div>3xl: 1920px <span style="color:#6a9955;">// カスタム追加</span></div></div>`}
		/>
	</section>

	<section class="mb-10">
		<h2 id="animation" class="text-xl font-bold mb-4">アニメーション</h2>

		<CodePreview
			title="カスタムアニメーション"
			description="独自のアニメーションを追加"
			language="javascript"
			code={`// tailwind.config.js
export default {
  theme: {
    extend: {
      animation: {
        'fade-in': 'fadeIn 0.5s ease-out',
        'slide-up': 'slideUp 0.3s ease-out',
        'bounce-slow': 'bounce 2s infinite',
      },
      keyframes: {
        fadeIn: {
          '0%': { opacity: '0' },
          '100%': { opacity: '1' },
        },
        slideUp: {
          '0%': { transform: 'translateY(20px)', opacity: '0' },
          '100%': { transform: 'translateY(0)', opacity: '1' },
        },
      },
    },
  },
}

// 使用例
// <div class="animate-fade-in">フェードイン</div>`}
			previewHtml={`<div style="display:flex;gap:16px;"><div style="padding:16px;background:#3b82f6;color:white;border-radius:8px;animation:pulse 2s infinite;">animate-pulse</div><div style="padding:16px;background:#22c55e;color:white;border-radius:8px;">animate-fade-in</div></div>`}
		/>
	</section>

	<section class="mb-10">
		<h2 id="plugins" class="text-xl font-bold mb-4">プラグイン</h2>

		<CodePreview
			title="公式プラグイン"
			description="追加機能を有効化"
			language="javascript"
			code={`// インストール
// npm install @tailwindcss/typography
// npm install @tailwindcss/forms

// tailwind.config.js
export default {
  plugins: [
    require('@tailwindcss/typography'),
    require('@tailwindcss/forms'),
    require('@tailwindcss/aspect-ratio'),
  ],
}

// Typography プラグインの使用例
// <article class="prose lg:prose-xl">
//   <h1>見出し</h1>
//   <p>本文...</p>
// </article>`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div>@tailwindcss/<span style="color:#4ec9b0;">typography</span></div><div style="color:#6a9955;">// 記事スタイル（prose）</div><div style="margin-top:8px;">@tailwindcss/<span style="color:#4ec9b0;">forms</span></div><div style="color:#6a9955;">// フォーム要素のリセット</div></div>`}
		/>
	</section>

	<section class="mb-10">
		<h2 id="safelist" class="text-xl font-bold mb-4">セーフリスト</h2>

		<CodePreview
			title="動的クラスを保持"
			description="JSで生成するクラスを削除しない"
			language="javascript"
			code={`// tailwind.config.js
export default {
  // 常に含めるクラス
  safelist: [
    'bg-red-500',
    'bg-green-500',
    'bg-blue-500',
    // パターンマッチ
    {
      pattern: /bg-(red|green|blue)-(100|500|900)/,
    },
  ],
}

// これで動的クラスも動作する
// const color = 'red';
// <div class={\`bg-\${color}-500\`}>動的カラー</div>`}
			previewHtml={`<div style="font-family:monospace;background:#1e1e1e;color:#d4d4d4;padding:12px;border-radius:6px;font-size:13px;"><div style="color:#6a9955;">// Tailwindは使用されていないクラスを削除</div><div style="color:#6a9955;">// safelistで常に残すクラスを指定</div></div>`}
		/>
	</section>

	<div class="flex justify-between pt-6 border-t border-gray-200 dark:border-gray-700">
		<a href="/tailwind/responsive" class="inline-flex items-center gap-2 px-4 py-2 rounded-lg border border-gray-300 dark:border-gray-600 hover:bg-gray-100 dark:hover:bg-gray-800 transition-colors">
			<svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
				<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 19l-7-7 7-7" />
			</svg>
			前へ：レスポンシブ
		</a>
		<a href="/" class="inline-flex items-center gap-2 px-4 py-2 rounded-lg bg-primary-600 text-white hover:bg-primary-700 transition-colors">
			ホームに戻る
			<svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
				<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M3 12l2-2m0 0l7-7 7 7M5 10v10a1 1 0 001 1h3m10-11l2 2m-2-2v10a1 1 0 01-1 1h-3m-6 0a1 1 0 001-1v-4a1 1 0 011-1h2a1 1 0 011 1v4a1 1 0 001 1m-6 0h6" />
			</svg>
		</a>
	</div>
</article>
