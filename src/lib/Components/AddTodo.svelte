<script>
	let { addTodo } = $props();
</script>

<div
	class="add-todo-box w-full h-22 bg-[#252835]/30 backdrop-blur-md mt-6 rounded-2xl py-4 px-5 border border-[#3A3F4D]"
>
	<div
		class="add-todo-input w-full h-full border border-[#3A3F4D] rounded-2xl bg-[#262A36] flex items-center p-3"
	>
		<button title="add-icon" class="add-todo-icon bg-[#3268A5] rounded-2xl p-1">
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
		</button>
		<input
			class="border-l border-[#535969] ml-3 w-full px-3 placeholder:text-[#9CA3AF] text-[#F9FAFB] text-xl"
			type="text"
			placeholder="Add new task..."
			onkeydown={addTodo}
		/>
	</div>
</div>
