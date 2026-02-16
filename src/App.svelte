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
		
		const todoEl = event.target;
		const text = todoEl.value;
		const done = false;

		if(text !== ''){
			todos = [...todos, { text, done }];
		}
		todoEl.value = "";
	}
	function addTodoWithclick(){
		AddTodo
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
</script>

<div class="todo-window w-180">
	<TodoHeader />
	<AddTodo {addTodo} />
	{#if todos.length > 0}
		<ProgressBar {todos} {filterTodos} />
	{/if}
	<TodoList {filter} {editTodo} {toggleTodo} todos={filteredTodos} />
	<FilterBtn {setFilter} {todos} {filter} {filterTodos}/>
</div>

<style lang="postcss">
	@reference "tailwindcss";
</style>
