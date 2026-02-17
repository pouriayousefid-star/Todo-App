<script>
	import "./app.css";
	import AddTodo from "./lib/Components/AddTodo.svelte";
	import TodoHeader from "./lib/Components/TodoHeader.svelte";
	import TodoList from "./lib/Components/TodoList.svelte";
	import FilterBtn from "./lib/Components/FilterBtn.svelte";
	import ProgressBar from "./lib/Components/ProgressBar.svelte";

	let todos = $state([]);
	let filter = $state("all");
	let filteredTodos = $derived(filterTodos());

	function addTodo(event) {
		if (event.key !== "Enter") return;
		const id = crypto.randomUUID();
		const todoEl = event.target;
		const text = todoEl.value;
		const done = false;

		if (text !== "") {
			todos = [...todos, { text, done, id }];
		}
		todoEl.value = "";
	}
	function editTodo(event) {
		const inputEl = event.target;
		const index = +inputEl.dataset.index;
		todos = todos.map((todo) =>
			todo.id === index ? { ...todo, text: inputEl.value } : todo,
		);
	}
	function toggleTodo(id) {
		todos = todos.map((todo) =>
			todo.id === id ? { ...todo, done: !todo.done } : todo,
		);
	}
	function setFilter(newFilter) {
		filter = newFilter;
	}
	function filterTodos(progress = false) {
		if (progress) {
			return todos.filter((todo) => todo.done);
		} else {
			switch (filter) {
				case "all":
					return todos;
				case "active":
					return todos.filter((todo) => !todo.done);
				case "completed":
					return todos.filter((todo) => todo.done);
			}
		}
	}
	function removeTodo(id) {
		todos = todos.filter((todo) => todo.id !== id);
	}
</script>

<div class="todo-window w-180">
	<TodoHeader />
	<AddTodo {addTodo} />
	{#if todos.length > 0}
		<ProgressBar {todos} {filterTodos} />
	{/if}
	<TodoList
		{filter}
		{editTodo}
		{toggleTodo}
		todos={filteredTodos}
		{removeTodo}
	/>
	<FilterBtn {setFilter} {todos} {filter} {filterTodos} />
</div>

<style lang="postcss">
	@reference "tailwindcss";
</style>
