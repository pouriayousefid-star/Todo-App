<script>
    let {setFilter , todos} = $props();
</script>
<div class="filters mt-5 flex gap-3">
	{#if todos.length != 0}
		<button onclick={() => setFilter("all")} class="btn">All</button>
		<button onclick={() => setFilter("active")} class="btn">Active</button>
		<button onclick={() => setFilter("completed")} class="btn">Completed</button
		>
	{/if}
</div>
<style lang="postcss">
	@reference "tailwindcss";
	.btn {
		@apply bg-[#2B313E] px-3 py-1 rounded-lg text-[#9CA3AF];
	}
</style>