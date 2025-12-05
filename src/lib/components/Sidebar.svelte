<script>
	import { page } from '$app/stores';

	// メニュー構造の定義
	const menuItems = [
		{
			title: 'はじめに',
			icon: '📖',
			color: 'text-purple-500',
			items: [
				{ title: 'このサイトについて', href: '/intro' },
				{ title: '著者について', href: '/profile' }
			]
		},
		{
			title: 'HTML',
			icon: '🌐',
			color: 'text-orange-500',
			items: [
				{ title: '基本構造', href: '/html/basics' },
				{ title: '要素とタグ', href: '/html/elements' },
				{ title: 'フォーム', href: '/html/forms' },
				{ title: 'セマンティクス', href: '/html/semantics' }
			]
		},
		{
			title: 'CSS',
			icon: '🎨',
			color: 'text-blue-500',
			items: [
				{ title: 'セレクタ', href: '/css/selectors' },
				{ title: 'ボックスモデル', href: '/css/box-model' },
				{ title: 'Flexbox', href: '/css/flexbox' },
				{ title: 'Grid', href: '/css/grid' }
			]
		},
		{
			title: 'JavaScript',
			icon: '⚡',
			color: 'text-yellow-500',
			items: [
				{ title: '変数と型', href: '/js/variables' },
				{ title: '関数', href: '/js/functions' },
				{ title: '配列とオブジェクト', href: '/js/arrays-objects' },
				{ title: '非同期処理', href: '/js/async' },
				{ title: 'オブジェクト指向', href: '/js/oop' }
			]
		},
		{
			title: 'TypeScript',
			icon: '📘',
			color: 'text-blue-600',
			items: [
				{ title: 'はじめに', href: '/ts/basics' },
				{ title: '型の種類', href: '/ts/types' },
				{ title: 'インターフェース', href: '/ts/interfaces' },
				{ title: 'ジェネリクス', href: '/ts/generics' }
			]
		},
		{
			title: 'Next.js',
			icon: '▲',
			color: 'text-gray-900 dark:text-white',
			items: [
				{ title: 'はじめに', href: '/nextjs/intro' },
				{ title: 'ルーティング', href: '/nextjs/routing' },
				{ title: 'データ取得', href: '/nextjs/data-fetching' },
				{ title: 'API Routes', href: '/nextjs/api-routes' }
			]
		},
		{
			title: 'SvelteKit',
			icon: '🔥',
			color: 'text-orange-600',
			items: [
				{ title: 'はじめに', href: '/sveltekit/intro' },
				{ title: 'Svelteとは', href: '/sveltekit/svelte' },
				{ title: 'Viteとは', href: '/sveltekit/vite' },
				{ title: 'Tailwind導入', href: '/sveltekit/setup' },
				{ title: 'ルーティング', href: '/sveltekit/routing' },
				{ title: 'データ読み込み', href: '/sveltekit/loading' },
				{ title: 'フォームアクション', href: '/sveltekit/forms' },
				{ title: 'Hooks', href: '/sveltekit/hooks' },
				{ title: '状態管理', href: '/sveltekit/state' },
				{ title: 'レイアウト', href: '/sveltekit/layouts' },
				{ title: 'APIエンドポイント', href: '/sveltekit/api' },
				{ title: 'Supabase連携', href: '/sveltekit/supabase' },
				{ title: 'D1連携', href: '/sveltekit/d1' },
				{ title: 'ライブラリ', href: '/sveltekit/libraries' }
			]
		},
		{
			title: 'Tailwind CSS',
			icon: '💨',
			color: 'text-cyan-500',
			items: [
				{ title: 'はじめに', href: '/tailwind/intro' },
				{ title: 'ユーティリティ', href: '/tailwind/utilities' },
				{ title: 'レスポンシブ', href: '/tailwind/responsive' },
				{ title: 'モダンレイアウト', href: '/tailwind/layouts' },
				{ title: 'カスタマイズ', href: '/tailwind/customize' }
			]
		},
		{
			title: 'Supabase',
			icon: '⚡',
			color: 'text-emerald-500',
			items: [
				{ title: 'はじめに', href: '/supabase/intro' },
				{ title: 'セットアップ', href: '/supabase/setup' },
				{ title: 'データベース操作', href: '/supabase/database' },
				{ title: '認証', href: '/supabase/auth' },
				{ title: 'ストレージ', href: '/supabase/storage' }
			]
		},
		{
			title: 'Cloudflare',
			icon: '☁️',
			color: 'text-orange-500',
			items: [
				{ title: 'はじめに', href: '/cloudflare/intro' },
				{ title: 'D1 データベース', href: '/cloudflare/d1' },
				{ title: 'D1 セットアップ', href: '/cloudflare/d1-setup' },
				{ title: 'D1 SQLの基本', href: '/cloudflare/d1-sql' },
				{ title: 'D1 SvelteKit連携', href: '/cloudflare/d1-sveltekit' },
				{ title: 'R2 ストレージ', href: '/cloudflare/r2' },
				{ title: 'Pages デプロイ', href: '/cloudflare/pages' }
			]
		},
		{
			title: '開発方法',
			icon: '🛠️',
			color: 'text-gray-600 dark:text-gray-400',
			items: [
				{ title: '私の開発フロー', href: '/dev/my-workflow' },
				{ title: 'ベストプラクティス', href: '/dev/best-practices' },
				{ title: '個人開発 SvelteKit+D1', href: '/dev/sveltekit-d1-practices' }
			]
		}
	];

	// 展開状態を管理
	let expanded = $state({});

	function toggleSection(title) {
		expanded[title] = !expanded[title];
	}

	function isActive(href) {
		return $page.url.pathname === href;
	}

	function isSectionActive(items) {
		return items.some(item => $page.url.pathname.startsWith(item.href.split('/').slice(0, 2).join('/')));
	}
</script>

<nav class="p-4">
	<ul class="space-y-1">
		{#each menuItems as section}
			<li>
				<button
					onclick={() => toggleSection(section.title)}
					class="w-full flex items-center justify-between px-3 py-2 rounded-lg hover:bg-gray-100 dark:hover:bg-gray-700 transition-colors
					{isSectionActive(section.items) ? 'bg-gray-100 dark:bg-gray-700' : ''}"
				>
					<span class="flex items-center gap-2">
						<span class={section.color}>{section.icon}</span>
						<span class="font-medium">{section.title}</span>
					</span>
					<svg
						class="w-4 h-4 transition-transform {expanded[section.title] ? 'rotate-180' : ''}"
						fill="none"
						stroke="currentColor"
						viewBox="0 0 24 24"
					>
						<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M19 9l-7 7-7-7" />
					</svg>
				</button>

				{#if expanded[section.title]}
					<ul class="mt-1 ml-4 space-y-1">
						{#each section.items as item}
							<li>
								<a
									href={item.href}
									class="block px-3 py-1.5 rounded-lg text-sm transition-colors
									{isActive(item.href)
										? 'bg-primary-100 dark:bg-primary-900 text-primary-700 dark:text-primary-300 font-medium'
										: 'text-gray-600 dark:text-gray-400 hover:bg-gray-100 dark:hover:bg-gray-700'}"
								>
									{item.title}
								</a>
							</li>
						{/each}
					</ul>
				{/if}
			</li>
		{/each}
	</ul>
</nav>
