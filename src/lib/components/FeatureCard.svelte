<script>
	let { icon = '', title = '', description = '', tag = '' } = $props();
</script>

<div class="p-3 sm:p-4 rounded-lg border border-gray-200 dark:border-gray-700 bg-white dark:bg-gray-800 hover:border-primary-300 dark:hover:border-primary-600 transition-colors">
	<div class="flex items-start gap-2 sm:gap-3">
		<span class="text-xl sm:text-2xl flex-shrink-0">{icon}</span>
		<div class="flex-1 min-w-0">
			<div class="flex items-center gap-1.5 sm:gap-2 flex-wrap">
				<h4 class="font-semibold text-sm sm:text-base text-gray-900 dark:text-white">{title}</h4>
				{#if tag}
					<span class="px-1.5 sm:px-2 py-0.5 text-xs rounded-full bg-primary-100 dark:bg-primary-900 text-primary-700 dark:text-primary-300 flex-shrink-0">
						{tag}
					</span>
				{/if}
			</div>
			<p class="text-xs sm:text-sm text-gray-600 dark:text-gray-400 mt-1">{description}</p>
		</div>
	</div>
</div>
