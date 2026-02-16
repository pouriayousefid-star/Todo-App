<script>
	let { todos, filteredTodos, filter } = $props();
	let progress = $state(0);
	// svelte-ignore state_referenced_locally
		if (filter == "completed" && todos.length > 0) {
		progress = filteredTodos.length / todos.length / 100;
	}
</script>

<div class="progress-bar-container w-full flex">
	<p>Progress</p>
	<div class="w-full">
		<div class="progress-bar bg-amber-300 w-[{progress}%] h-full"></div>
	</div>
</div>

<style>

</style>
