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
		explanations = []
	} = $props();

	let copied = $state(false);

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

<div class="my-4 sm:my-6 rounded-xl border border-gray-200 dark:border-gray-700 overflow-hidden bg-white dark:bg-gray-800 -mx-3 sm:mx-0">
	{#if title}
		<div class="px-3 sm:px-4 py-2 sm:py-3 border-b border-gray-200 dark:border-gray-700 bg-gray-50 dark:bg-gray-900">
			<h3 class="font-semibold text-sm sm:text-base text-gray-900 dark:text-white">{title}</h3>
		</div>
	{/if}

	<div class="flex flex-col md:grid md:grid-cols-2">
		<!-- コード部分 -->
		<div class="relative border-b md:border-b-0 md:border-r border-gray-200 dark:border-gray-700 order-2 md:order-1">
			<div class="flex items-center justify-between px-2 sm:px-3 py-2 bg-gray-100 dark:bg-gray-900 border-b border-gray-200 dark:border-gray-700">
				<span class="text-xs font-medium text-gray-500 dark:text-gray-400 uppercase">{language}</span>
				<button
					onclick={copyCode}
					class="p-1.5 rounded hover:bg-gray-200 dark:hover:bg-gray-700 text-gray-500 dark:text-gray-400 transition-colors flex-shrink-0"
					aria-label="コピー"
				>
					{#if copied}
						<svg class="w-3.5 h-3.5 sm:w-4 sm:h-4 text-green-500" fill="none" stroke="currentColor" viewBox="0 0 24 24">
							<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M5 13l4 4L19 7" />
						</svg>
					{:else}
						<svg class="w-3.5 h-3.5 sm:w-4 sm:h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
							<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M8 16H6a2 2 0 01-2-2V6a2 2 0 012-2h8a2 2 0 012 2v2m-6 12h8a2 2 0 002-2v-8a2 2 0 00-2-2h-8a2 2 0 00-2 2v8a2 2 0 002 2z" />
						</svg>
					{/if}
				</button>
			</div>
			<pre class="p-3 sm:p-4 overflow-x-auto text-xs sm:text-sm bg-gray-900 dark:bg-gray-950"><code class="language-{language} font-mono">{@html getHighlightedCode()}</code></pre>
		</div>

		<!-- 解説部分 -->
		<div class="p-3 sm:p-4 bg-gray-50 dark:bg-gray-800/50 order-1 md:order-2">
			<h4 class="text-xs sm:text-sm font-semibold text-gray-700 dark:text-gray-300 mb-3 flex items-center gap-2">
				<svg class="w-3.5 h-3.5 sm:w-4 sm:h-4 flex-shrink-0" fill="none" stroke="currentColor" viewBox="0 0 24 24">
					<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M13 16h-1v-4h-1m1-4h.01M21 12a9 9 0 11-18 0 9 9 0 0118 0z" />
				</svg>
				コードの解説
			</h4>
			<div class="space-y-2 sm:space-y-3">
				{#each explanations as exp}
					<div class="flex gap-2 sm:gap-3">
						<div class="flex-shrink-0 w-5 h-5 sm:w-6 sm:h-6 rounded-full bg-primary-100 dark:bg-primary-900 text-primary-700 dark:text-primary-300 flex items-center justify-center text-xs font-bold">
							{exp.line || '•'}
						</div>
						<div class="min-w-0">
							{#if exp.code}
								<code class="text-xs bg-gray-200 dark:bg-gray-700 px-1 sm:px-1.5 py-0.5 rounded text-primary-600 dark:text-primary-400 break-all">{exp.code}</code>
							{/if}
							<p class="text-xs sm:text-sm text-gray-600 dark:text-gray-400 mt-0.5">{exp.text}</p>
						</div>
					</div>
				{/each}
			</div>
		</div>
	</div>
</div>

<style>
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
