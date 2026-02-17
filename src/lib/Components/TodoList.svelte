<script>
	import { slide } from "svelte/transition";

    let {todos , editTodo , toggleTodo , filter} = $props()
</script>
<div
	class="tasks w-full bg-[#252835]/30 backdrop-blur-md mt-6 rounded-2xl py-4 px-5 border border-[#3A3F4D] flex flex-col gap-4"
>
	{#each todos as todo (todo.id)}
		<div
			transition:slide
			class="todo w-full h-full border border-[#3A3F4D] rounded-2xl bg-[#262A36] flex items-center p-5"
		>
			<input
				data-index={todo.id}
				oninput={editTodo}
				type="text"
				value={todo.text}
				class="w-full px-3 placeholder:text-[#9CA3AF] text-[#F9FAFB] text-2xl {todo.done &&
				filter != 'completed'
					? 'done'
					: ''}"
			/>
			<input
				data-index={todo.id}
				type="checkbox"
				checked={todo.done}
				class="scale-200 accent-green-700"
				onchange={toggleTodo}
			/>
		</div>
	{/each}
	{#if todos.length == 0}
		<p class="text-[#F9FAFB] text-3xl">Nothing...</p>
	{/if}
</div>
<style lang="postcss">
	@reference "tailwindcss";
	.done{
		@apply blur-[1px];
	}
</style>