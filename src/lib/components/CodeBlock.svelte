<script>
	import Prism from 'prismjs';
	import 'prismjs/components/prism-javascript';
	import 'prismjs/components/prism-typescript';
	import 'prismjs/components/prism-css';
	import 'prismjs/components/prism-markup';
	import 'prismjs/components/prism-jsx';
	import 'prismjs/components/prism-json';
	import 'prismjs/components/prism-bash';

	let { code = '', language = 'javascript', filename = '' } = $props();
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

<div class="relative group rounded-lg overflow-hidden bg-gray-900 dark:bg-gray-950 my-3 sm:my-4 -mx-3 sm:mx-0">
	<!-- ファイル名 -->
	{#if filename}
		<div class="flex items-center justify-between px-3 sm:px-4 py-2 bg-gray-800 dark:bg-gray-900 border-b border-gray-700">
			<span class="text-xs sm:text-sm text-gray-400 truncate mr-2">{filename}</span>
			<span class="text-xs text-gray-500 uppercase flex-shrink-0">{language}</span>
		</div>
	{/if}

	<!-- コピーボタン -->
	<button
		onclick={copyCode}
		class="absolute top-2 right-2 p-1.5 sm:p-2 rounded-lg bg-gray-700 hover:bg-gray-600 text-gray-300 opacity-0 group-hover:opacity-100 transition-opacity z-10"
		aria-label="コードをコピー"
	>
		{#if copied}
			<svg class="w-3.5 h-3.5 sm:w-4 sm:h-4 text-green-400" fill="none" stroke="currentColor" viewBox="0 0 24 24">
				<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M5 13l4 4L19 7" />
			</svg>
		{:else}
			<svg class="w-3.5 h-3.5 sm:w-4 sm:h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
				<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M8 16H6a2 2 0 01-2-2V6a2 2 0 012-2h8a2 2 0 012 2v2m-6 12h8a2 2 0 002-2v-8a2 2 0 00-2-2h-8a2 2 0 00-2 2v8a2 2 0 002 2z" />
			</svg>
		{/if}
	</button>

	<!-- コード -->
	<pre class="p-3 sm:p-4 overflow-x-auto text-xs sm:text-sm {filename ? '' : 'pt-8 sm:pt-10'}"><code class="language-{language}">{@html getHighlightedCode()}</code></pre>
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
