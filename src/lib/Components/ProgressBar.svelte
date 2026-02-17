<script>
	let { todos, filterTodos } = $props();
	let progress = $derived((filterTodos(true).length / todos.length) * 100);
</script>

<div
	class="progress-bar-container h-8 w-full flex gap-3 items-center mt-5 px-2"
>
	<p class="text-2xl text-[#F9FAFB]">Progress:</p>
	<!-- use inline css because with tailwind dose not work because Tailwind generates classes at build time  -->
	<div class="w-full">
		<div
			class="progress bg-linear-to-r from-[#328AFC] via-[#38CBBE] to-[#E1DD9E] mt-2 h-4 rounded-2xl"
			style="width: {progress > 0 ? progress : 2}%;"
		></div>
	</div>
</div>

<style lang="postcss">
	@reference "tailwindcss";
	.progress {
		transition: 0.8s;
	}
</style>
