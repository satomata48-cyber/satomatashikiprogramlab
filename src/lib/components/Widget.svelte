<script>
	import { onMount } from 'svelte';
	import { page } from '$app/stores';

	let headings = $state([]);
	let activeId = $state('');

	onMount(() => {
		updateHeadings();
		setupObserver();
	});

	function updateHeadings() {
		const elements = document.querySelectorAll('main h2, main h3');
		headings = Array.from(elements).map((el, index) => ({
			id: el.id || `heading-${index}`,
			text: el.textContent || '',
			level: el.tagName === 'H2' ? 2 : 3
		}));

		// IDがない見出しにIDを付与
		elements.forEach((el, index) => {
			if (!el.id) {
				el.id = `heading-${index}`;
			}
		});
	}

	function setupObserver() {
		const observer = new IntersectionObserver(
			(entries) => {
				entries.forEach((entry) => {
					if (entry.isIntersecting) {
						activeId = entry.target.id;
					}
				});
			},
			{ rootMargin: '-80px 0px -80% 0px' }
		);

		document.querySelectorAll('main h2, main h3').forEach((el) => {
			observer.observe(el);
		});

		return () => observer.disconnect();
	}

	// ページ変更時に見出しを更新
	$effect(() => {
		$page.url.pathname;
		setTimeout(updateHeadings, 100);
	});

	// 関連リンク
	const relatedLinks = [
		{ title: 'MDN Web Docs', url: 'https://developer.mozilla.org/ja/', icon: '📚' },
		{ title: 'W3Schools', url: 'https://www.w3schools.com/', icon: '🎓' },
		{ title: 'Can I Use', url: 'https://caniuse.com/', icon: '✅' }
	];
</script>

<div class="p-4">
	<!-- 目次 -->
	{#if headings.length > 0}
		<div class="mb-6">
			<h3 class="text-sm font-semibold text-gray-500 dark:text-gray-400 uppercase tracking-wider mb-3">
				目次
			</h3>
			<nav>
				<ul class="space-y-1">
					{#each headings as heading}
						<li>
							<a
								href="#{heading.id}"
								class="block py-1 text-sm transition-colors border-l-2
								{heading.level === 3 ? 'pl-4' : 'pl-2'}
								{activeId === heading.id
									? 'border-primary-500 text-primary-600 dark:text-primary-400 font-medium'
									: 'border-transparent text-gray-600 dark:text-gray-400 hover:text-gray-900 dark:hover:text-gray-200'}"
							>
								{heading.text}
							</a>
						</li>
					{/each}
				</ul>
			</nav>
		</div>
	{/if}

	<!-- 関連リンク -->
	<div>
		<h3 class="text-sm font-semibold text-gray-500 dark:text-gray-400 uppercase tracking-wider mb-3">
			関連リンク
		</h3>
		<ul class="space-y-2">
			{#each relatedLinks as link}
				<li>
					<a
						href={link.url}
						target="_blank"
						rel="noopener noreferrer"
						class="flex items-center gap-2 text-sm text-gray-600 dark:text-gray-400 hover:text-primary-600 dark:hover:text-primary-400 transition-colors"
					>
						<span>{link.icon}</span>
						<span>{link.title}</span>
						<svg class="w-3 h-3" fill="none" stroke="currentColor" viewBox="0 0 24 24">
							<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M10 6H6a2 2 0 00-2 2v10a2 2 0 002 2h10a2 2 0 002-2v-4M14 4h6m0 0v6m0-6L10 14" />
						</svg>
					</a>
				</li>
			{/each}
		</ul>
	</div>
</div>
