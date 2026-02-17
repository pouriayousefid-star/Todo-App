<script>
	import { slide } from "svelte/transition";

	let { todos, editTodo, toggleTodo, filter, removeTodo } = $props();
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
				class="todo-text w-full px-3 placeholder:text-[#9CA3AF] text-[#F9FAFB] text-2xl {todo.done &&
				filter != 'completed'
					? 'done'
					: ''}"
			/>
			<input
				type="checkbox"
				checked={todo.done}
				class="scale-200 accent-green-700"
				onchange={() => toggleTodo(todo.id)}
			/>
			<button
				onclick={() => removeTodo(todo.id)}
				title="remove"
				class="delete-icon ml-3 text-red-400 cursor-pointer"
			>
				<svg
					xmlns="http://www.w3.org/2000/svg"
					width="34"
					height="34"
					viewBox="0 0 24 24"
					><path
						fill="currentColor"
						d="M7 21q-.825 0-1.412-.587T5 19V6q-.425 0-.712-.288T4 5t.288-.712T5 4h4q0-.425.288-.712T10 3h4q.425 0 .713.288T15 4h4q.425 0 .713.288T20 5t-.288.713T19 6v13q0 .825-.587 1.413T17 21zM17 6H7v13h10zm-6.287 10.713Q11 16.425 11 16V9q0-.425-.288-.712T10 8t-.712.288T9 9v7q0 .425.288.713T10 17t.713-.288m4 0Q15 16.426 15 16V9q0-.425-.288-.712T14 8t-.712.288T13 9v7q0 .425.288.713T14 17t.713-.288M7 6v13z"
					/></svg
				>
			</button>
		</div>
	{/each}
	{#if todos.length == 0}
		<p class="text-[#F9FAFB] text-3xl">Nothing...</p>
	{/if}
</div>

<style lang="postcss">
	@reference "tailwindcss";
	.done {
		@apply blur-[1px];
	}
</style>
