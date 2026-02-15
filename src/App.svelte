<script>
	import "./app.css";
	let todos = $state([]);
	let filter = $state("all");

	let filteredTodos = $derived(filterTodos());

	function addTodo(event) {
		if (event.key !== "Enter") return;

		const todoEl = event.target;
		const text = todoEl.value;
		const done = false;

		todos = [...todos, { text, done }];
		todoEl.value = "";
	}
	function editTodo(event) {
		const inputEl = event.target;
		const index = +inputEl.dataset.index;
		todos[index].text = inputEl.value;
	}
	function toggleTodo(event) {
		const inputEl = event.target;
		const index = +inputEl.dataset.index;
		todos[index].done = !todos[index].done;
	}
	function setFilter(newFilter) {
		filter = newFilter;
	}
	function filterTodos() {
		switch (filter) {
			case "all":
				return todos;
			case "active":
				return todos.filter((todo) => !todo.done);
			case "completed":
				return todos.filter((todo) => todo.done);
		}
	}
</script>

<div class="todo-window w-180">
	<div class="todo-header w-full flex justify-between px-3">
		<h1 class="text-3xl text-[#F9FAFB]">My Tasks</h1>
		<div class="setting flex gap-1 justify-center">
			<svg
				class="h-7.5 text-[#9CA3AF]"
				xmlns="http://www.w3.org/2000/svg"
				width="24"
				height="24"
				viewBox="0 0 24 24"
				><path
					fill="currentColor"
					fill-rule="evenodd"
					d="M14.208 4.83q.68.21 1.3.54l1.833-1.1a1 1 0 0 1 1.221.15l1.018 1.018a1 1 0 0 1 .15 1.221l-1.1 1.833q.33.62.54 1.3l2.073.519a1 1 0 0 1 .757.97v1.438a1 1 0 0 1-.757.97l-2.073.519q-.21.68-.54 1.3l1.1 1.833a1 1 0 0 1-.15 1.221l-1.018 1.018a1 1 0 0 1-1.221.15l-1.833-1.1q-.62.33-1.3.54l-.519 2.073a1 1 0 0 1-.97.757h-1.438a1 1 0 0 1-.97-.757l-.519-2.073a7.5 7.5 0 0 1-1.3-.54l-1.833 1.1a1 1 0 0 1-1.221-.15L4.42 18.562a1 1 0 0 1-.15-1.221l1.1-1.833a7.5 7.5 0 0 1-.54-1.3l-2.073-.519A1 1 0 0 1 2 12.72v-1.438a1 1 0 0 1 .757-.97l2.073-.519q.21-.68.54-1.3L4.27 6.66a1 1 0 0 1 .15-1.221L5.438 4.42a1 1 0 0 1 1.221-.15l1.833 1.1q.62-.33 1.3-.54l.519-2.073A1 1 0 0 1 11.28 2h1.438a1 1 0 0 1 .97.757zM12 16a4 4 0 1 0 0-8a4 4 0 0 0 0 8"
				/></svg
			>
			<p class="text-xl text-[#9CA3AF]">Settings</p>
		</div>
	</div>
	<div
		class="add-todo-box w-full h-22 bg-[#252835]/30 backdrop-blur-md mt-6 rounded-2xl py-4 px-5 border border-[#3A3F4D]"
	>
		<div
			class="add-todo-input w-full h-full border border-[#3A3F4D] rounded-2xl bg-[#262A36] flex items-center p-3"
		>
			<div class="add-todo-icon bg-[#3268A5] rounded-2xl p-1">
				<svg
					class="text-[#F9FAFB]"
					xmlns="http://www.w3.org/2000/svg"
					width="24"
					height="24"
					viewBox="0 0 24 24"
					><path
						fill="currentColor"
						d="M18 12.998h-5v5a1 1 0 0 1-2 0v-5H6a1 1 0 0 1 0-2h5v-5a1 1 0 0 1 2 0v5h5a1 1 0 0 1 0 2"
					/></svg
				>
			</div>
			<input
				class="border-l border-[#535969] ml-3 w-full px-3 placeholder:text-[#9CA3AF] text-[#F9FAFB] text-xl"
				type="text"
				placeholder="Add new task..."
				onkeydown={addTodo}
			/>
		</div>
	</div>
	{#if todos.length != 0}
		<div
			class="tasks w-full bg-[#252835]/30 backdrop-blur-md mt-6 rounded-2xl py-4 px-5 border border-[#3A3F4D] flex flex-col gap-4"
		>
			{#each filteredTodos as todo, i}
				<div
					class="todo w-full h-full border border-[#3A3F4D] rounded-2xl bg-[#262A36] flex items-center p-5"
				>
					<input
						data-index={i}
						oninput={editTodo}
						type="text"
						value={todo.text}
						class="w-full px-3 placeholder:text-[#9CA3AF] text-[#F9FAFB] text-2xl {todo.done && 'done'}"
					/>
					<input
						data-index={i}
						type="checkbox"
						checked={todo.done}
						class="scale-200 accent-green-700"
						onchange={toggleTodo}
					/>
				</div>
			{/each}
			{#if filteredTodos.length == 0}
				<p class="text-[#F9FAFB] text-3xl">Nothing...</p>
			{/if}
		</div>
	{/if}
	<div class="filters mt-5 flex gap-3">
		{#if todos.length != 0}
			<button onclick={() => setFilter("all")} class="btn">All</button>
			<button onclick={() => setFilter("active")} class="btn">Active</button>
			<button onclick={() => setFilter("completed")} class="btn"
				>Completed</button
			>
		{/if}
	</div>
</div>

<style lang="postcss">
	@reference "tailwindcss";
	.btn {
		@apply bg-[#2B313E] px-3 py-1 rounded-lg text-[#9CA3AF];
	}
	.done{
		@apply blur-[1px];
	}
</style>
