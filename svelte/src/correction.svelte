<script>
	let todos = [
		{
			name: "Ma première tâche",
			completed: false,
		},
		{
			name: "Ma deuxième tâche",
			completed: true,
		},
	];
	let newTodo = "";
	function addTodo() {
		todos = [
			...todos,
			{
				name: newTodo,
				completed: false,
			},
		];
		newTodo = "";
	}
	let showCompleted = true;
	$: filterdTodos = todos.filter((t) =>
		showCompleted === true ? true : t.completed === false
	);

	function changeTodo(todo) {
		todos = todos.map((t) => {
			if (t === todo) {
				return { ...todo, completed: !t.completed };
			}
			return t;
		});
	}
</script>

<h1>Ma liste de tâches</h1>
<label><input type="checkbox" bind:checked={showCompleted} /> Afficher les tâches
	finies
</label>

<ul>
	{#each filterdTodos as todo}
		<li>
			<input
				type="checkbox"
				checked={todo.completed}
				on:change={() => changeTodo(todo)} />
			{todo.name}
		</li>
	{/each}
</ul>
<input
	type="text"
	bind:value={newTodo}
	on:keydown={(event) => event.key === 'Enter' && addTodo()} />
<button on:click|preventDefault={addTodo}> Ajouter </button>
