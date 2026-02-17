<script>
	let { setFilter, todos, filter, filterTodos } = $props();
</script>

<div class="filters mt-5 flex gap-3 items-center">
	{#if todos.length != 0}
		<button
			onclick={() => setFilter("all")}
			class="btn {filter == 'all' ? 'bg-blue-900' : 'bg-[#2B313E]'}">All</button
		>
		<button
			onclick={() => setFilter("active")}
			class="btn {filter == 'active' ? 'bg-blue-900' : 'bg-[#2B313E]'}"
			>Active</button
		>
		<button
			onclick={() => setFilter("completed")}
			class="btn {filter == 'completed' ? 'bg-blue-900' : 'bg-[#2B313E]'}"
			>Completed</button
		>
		<p class="text-xl text-[#F9FAFB]">
			Remaining: {todos.length - filterTodos(true).length}
		</p>
	{/if}
</div>

<style lang="postcss">
	@reference "tailwindcss";
	.btn {
		@apply px-3 py-1 rounded-lg text-[#9CA3AF];
	}
</style>
