<script>
	import Prism from 'prismjs';
	import 'prismjs/components/prism-javascript';
	import 'prismjs/components/prism-typescript';
	import 'prismjs/components/prism-css';
	import 'prismjs/components/prism-markup';
	import 'prismjs/components/prism-jsx';
	import 'prismjs/components/prism-json';
	import 'prismjs/components/prism-bash';

	let {
		code = '',
		language = 'html',
		title = '',
		description = '',
		previewHtml = ''
	} = $props();

	let copied = $state(false);
	let activeTab = $state('preview');

	// Prismの言語マッピング
	const languageMap = {
		'html': 'markup',
		'svelte': 'markup',
		'js': 'javascript',
		'ts': 'typescript'
	};

	function getHighlightedCode() {
		const lang = languageMap[language] || language;
		const grammar = Prism.languages[lang] || Prism.languages.javascript;
		return Prism.highlight(code, grammar, lang);
	}

	async function copyCode() {
		try {
			await navigator.clipboard.writeText(code);
			copied = true;
			setTimeout(() => copied = false, 2000);
		} catch (err) {
			console.error('コピーに失敗しました:', err);
		}
	}
</script>

<div class="my-6 rounded-xl border border-gray-200 dark:border-gray-700 overflow-hidden bg-white dark:bg-gray-800">
	<!-- ヘッダー -->
	{#if title}
		<div class="px-4 py-3 border-b border-gray-200 dark:border-gray-700 bg-gray-50 dark:bg-gray-900">
			<h3 class="font-semibold text-gray-900 dark:text-white">{title}</h3>
			{#if description}
				<p class="text-sm text-gray-600 dark:text-gray-400 mt-1">{description}</p>
			{/if}
		</div>
	{/if}

	<!-- previewHtmlがある場合は2カラム、ない場合は1カラム -->
	{#if previewHtml}
		<div class="grid grid-cols-1 lg:grid-cols-2">
			<!-- コード部分 -->
			<div class="relative border-b lg:border-b-0 lg:border-r border-gray-200 dark:border-gray-700">
				<div class="flex items-center justify-between px-3 py-2 bg-gray-100 dark:bg-gray-900 border-b border-gray-200 dark:border-gray-700">
					<span class="text-xs font-medium text-gray-500 dark:text-gray-400 uppercase">{language}</span>
					<button
						onclick={copyCode}
						class="p-1.5 rounded hover:bg-gray-200 dark:hover:bg-gray-700 text-gray-500 dark:text-gray-400 transition-colors"
						aria-label="コピー"
					>
						{#if copied}
							<svg class="w-4 h-4 text-green-500" fill="none" stroke="currentColor" viewBox="0 0 24 24">
								<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M5 13l4 4L19 7" />
							</svg>
						{:else}
							<svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
								<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M8 16H6a2 2 0 01-2-2V6a2 2 0 012-2h8a2 2 0 012 2v2m-6 12h8a2 2 0 002-2v-8a2 2 0 00-2-2h-8a2 2 0 00-2 2v8a2 2 0 002 2z" />
							</svg>
						{/if}
					</button>
				</div>
				<pre class="p-4 overflow-x-auto text-sm bg-gray-900 dark:bg-gray-950 max-h-80"><code class="language-{language} font-mono">{@html getHighlightedCode()}</code></pre>
			</div>

			<!-- プレビュー部分 -->
			<div class="flex flex-col">
				<div class="flex items-center gap-2 px-3 py-2 bg-gray-100 dark:bg-gray-900 border-b border-gray-200 dark:border-gray-700">
					<span class="text-xs font-medium text-gray-500 dark:text-gray-400 uppercase">プレビュー</span>
				</div>
				<div class="flex-1 p-4 bg-white dark:bg-gray-800 min-h-32">
					<div class="preview-container">
						{@html previewHtml}
					</div>
				</div>
			</div>
		</div>
	{:else}
		<!-- previewHtmlがない場合はコードのみ表示 -->
		<div class="relative">
			<div class="flex items-center justify-between px-3 py-2 bg-gray-100 dark:bg-gray-900 border-b border-gray-200 dark:border-gray-700">
				<span class="text-xs font-medium text-gray-500 dark:text-gray-400 uppercase">{language}</span>
				<button
					onclick={copyCode}
					class="p-1.5 rounded hover:bg-gray-200 dark:hover:bg-gray-700 text-gray-500 dark:text-gray-400 transition-colors"
					aria-label="コピー"
				>
					{#if copied}
						<svg class="w-4 h-4 text-green-500" fill="none" stroke="currentColor" viewBox="0 0 24 24">
							<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M5 13l4 4L19 7" />
						</svg>
					{:else}
						<svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
							<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M8 16H6a2 2 0 01-2-2V6a2 2 0 012-2h8a2 2 0 012 2v2m-6 12h8a2 2 0 002-2v-8a2 2 0 00-2-2h-8a2 2 0 00-2 2v8a2 2 0 002 2z" />
						</svg>
					{/if}
				</button>
			</div>
			<pre class="p-4 overflow-x-auto text-sm bg-gray-900 dark:bg-gray-950 max-h-96"><code class="language-{language} font-mono">{@html getHighlightedCode()}</code></pre>
		</div>
	{/if}
</div>

<style>
	.preview-container :global(*) {
		all: revert;
	}
	.preview-container {
		font-family: system-ui, sans-serif;
	}

	/* Prism.js カスタムテーマ（ダークモード） */
	:global(.token.comment),
	:global(.token.prolog),
	:global(.token.doctype),
	:global(.token.cdata) {
		color: #6a9955;
	}

	:global(.token.punctuation) {
		color: #d4d4d4;
	}

	:global(.token.property),
	:global(.token.tag),
	:global(.token.boolean),
	:global(.token.number),
	:global(.token.constant),
	:global(.token.symbol),
	:global(.token.deleted) {
		color: #b5cea8;
	}

	:global(.token.selector),
	:global(.token.attr-name),
	:global(.token.string),
	:global(.token.char),
	:global(.token.builtin),
	:global(.token.inserted) {
		color: #ce9178;
	}

	:global(.token.operator),
	:global(.token.entity),
	:global(.token.url),
	:global(.language-css .token.string),
	:global(.style .token.string) {
		color: #d4d4d4;
	}

	:global(.token.atrule),
	:global(.token.attr-value),
	:global(.token.keyword) {
		color: #569cd6;
	}

	:global(.token.function),
	:global(.token.class-name) {
		color: #dcdcaa;
	}

	:global(.token.regex),
	:global(.token.important),
	:global(.token.variable) {
		color: #d16969;
	}
</style>
